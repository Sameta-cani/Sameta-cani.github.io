---
layout: single
title:  "구조화된 배열과 레코드 배열, 정렬, 고급 배열 입출력, 성능 팁"
categories: NumPy
tag: [python, NumPy]
toc: true
author_profile: false
toc_sticky: true
---

<head>
  <style>
    table.dataframe {
      white-space: normal;
      width: 100%;
      height: 240px;
      display: block;
      overflow: auto;
      font-family: Arial, sans-serif;
      font-size: 0.9rem;
      line-height: 20px;
      text-align: center;
      border: 0px !important;
    }

    table.dataframe th {
      text-align: center;
      font-weight: bold;
      padding: 8px;
    }

    table.dataframe td {
      text-align: center;
      padding: 8px;
    }

    table.dataframe tr:hover {
      background: #b8d1f3; 
    }

    .output_prompt {
      overflow: auto;
      font-size: 0.9rem;
      line-height: 1.45;
      border-radius: 0.3rem;
      -webkit-overflow-scrolling: touch;
      padding: 0.8rem;
      margin-top: 0;
      margin-bottom: 15px;
      font: 1rem Consolas, "Liberation Mono", Menlo, Courier, monospace;
      color: $code-text-color;
      border: solid 1px $border-color;
      border-radius: 0.3rem;
      word-break: normal;
      white-space: pre;
    }

  .dataframe tbody tr th:only-of-type {
      vertical-align: middle;
  }

  .dataframe tbody tr th {
      vertical-align: top;
  }

  .dataframe thead th {
      text-align: center !important;
      padding: 8px;
  }

  .page__content p {
      margin: 0 0 0px !important;
  }

  .page__content p > strong {
    font-size: 0.8rem !important;
  }

  </style>
</head>


# 구조화된 배열과 레코드 배열

ndarray는 <strong>단일</strong> 데이터 저장소이다. 이 말은 각 원소가 dtype에 의해 결정된 같은 크기의 메모리를 차지하고 있다는 뜻이다. 표면적으로는 다중 데이터나 표 형식의 데이터를 표현할 수 없는 것처럼 보인다. <strong>구조화된</strong> 배열은 배열의 각 원소가 C의 <strong>구조체</strong> 혹은 다양한 이름의 필드를 갖는 SQL 테이블의 한 로우로 표현되는 것으로 생각할 수 있는 ndarray다(그래서 구조화된 배열이라고 한다).



```python
dtype = [('x', np.float64), ('y', np.int32)]

sarr = np.array([(1.5, 6), (np.pi, -2)], dtype=dtype)

sarr
```

<pre>
array([(1.5       ,  6), (3.14159265, -2)],
      dtype=[('x', '< f8'), ('y', '< i4')])
</pre>
구조화된 dtype을 지정하는 방법은 여러 가지다(NumPy 문서를 참고하자). 한 가지 일반적인 방법은 튜플 (field_name, field_data_type)을 이용하는 것이다. 이제 배열의 원소는 사전처럼 접근할 수 있는 튜플 같은 객체다.



```python
sarr[0]
```

<pre>
(1.5, 6)
</pre>

```python
sarr[0]['y']
```

<pre>
6
</pre>
필드 이름은 dtype.names 속성에 저장된다. 



```python
sarr.dtype.names
```

<pre>
('x', 'y')
</pre>
구조화된 배열의 필드에 접근하면 데이터의 뷰가 반환되므로 아무것도 복사되지 않는다.



```python
sarr['x']
```

<pre>
array([1.5       , 3.14159265])
</pre>
## 중첩된 dtype과 다차원 필드

구조화된 dtype을 지정할 때 추가적으로 그 모양(정수나 튜플로)을 전달할 수 있다.



```python
dtype = [('x', np.int64, 3), ('y', np.int32)]

arr = np.zeros(4, dtype=dtype)

arr
```

<pre>
array([([0, 0, 0], 0), ([0, 0, 0], 0), ([0, 0, 0], 0), ([0, 0, 0], 0)],
      dtype=[('x', '< i8', (3,)), ('y', '< i4')])
</pre>
이 경우 x 필드는 각 원소에 대해 길이가 3인 배열을 참조하게 된다. 따라서 값의 변화가 있을 시 원본에도 변화가 있다.



```python
arr[0]['x']
```

<pre>
array([0, 0, 0], dtype=int64)
</pre>

```python
ar = arr[0]['x']
ar[:] = [1, 2, 3]

arr
```

<pre>
array([([1, 2, 3], 0), ([0, 0, 0], 0), ([0, 0, 0], 0), ([0, 0, 0], 0)],
      dtype=[('x', '< i8', (3,)), ('y', '< i4')])
</pre>
arr['x']로 접근하면 1차원 배열 대신 2차원 배열이 반환된다.



```python
arr['x']
```

<pre>
array([[1, 2, 3],
       [0, 0, 0],
       [0, 0, 0],
       [0, 0, 0]], dtype=int64)
</pre>
이를 통해 좀 더 복잡한 중첩 구조를 하나의 배열 안에서 단일 메모리로 표현할 수 있게 된다.<br>

dtype을 무한히 복잡하게 만들 수 있는데 중첩된 dtype도 가능하다.



```python
dtype = [('x', [('a', 'f8'), ('b', 'f4')]), ('y', np.int32)]

data = np.array([((1, 2), 5), ((3, 4), 6)], dtype=dtype)

data['x']
```

<pre>
array([(1., 2.), (3., 4.)], dtype=[('a', '< f8'), ('b', '< f4')])
</pre>

```python
data['y']
```

<pre>
array([5, 6])
</pre>

```python
data['x']['a']
```

<pre>
array([1., 3.])
</pre>
pandas DataFrame의 계층적 색인은 이와 유사하긴 하지만 이런 기능을 직접 지원하지는 않는다.


## 구조화된 배열을 써야 하는 이유

pandas DataFrame과 비교해보면 NumPy의 구조화된 배열은 상대적으로 저수준 도구다. 메모리 블록을 복잡하게 중첩된 칼럼이 있는 표 형식처럼 해석할 수 있는 방법을 제공한다. 배열의 각 원소는 메모리상에서 고정된 크기의 바이트로 표현되기 때문에 구조화된 배열은 데이터를 디스크에서 읽거나 쓰고(나중에 살펴볼 메모리 맵을 포함하여) 네트워크를 통해 전송할 때 매우 빠르고 효과적인 방법을 제공한다.<br><br>

구조화된 배열의 또 다른 일반적인 사용 방법이 있다. 데이터 파일을 고정된 크기의 레코드 바이트 스트림으로 기록하는 것인데 이는 C나 C++ 코드에서 데이터를 직렬화하는 일반적인 방법이다. 파일의 포맷을 알고 있다면(즉, 각 레코드의 크기와 순서, 바이트 크기 그리고 각 원소의 자료형을 알고 있다면) `np.fromfile`을 사용해서 데이터를 메모리로 읽어 들일 수 있다.


# 정렬

파이썬의 내장 리스트와 마찬가지로 ndarray의 `sort` 인스턴스 메서드는 새로운 배열을 생성하지 않고 직접 해당 배열의 내용을 정렬한다.



```python
arr = np.random.randn(6)

arr.sort()
```


```python
arr
```

<pre>
array([-1.68134226, -0.63606351,  0.2373469 ,  0.36144108,  0.4493243 ,
        1.13749473])
</pre>
배열을 그대로 정렬할 때는 그 배열이 다른 ndarray의 뷰일 경우 원본 배열의 값이 변경된다.



```python
arr = np.random.randn(3, 5)

arr
```

<pre>
array([[-0.62892708,  1.151293  , -1.36398417,  1.01977508, -0.9672169 ],
       [-0.02247658, -0.47572291,  0.284057  , -1.34721628, -1.05052891],
       [ 0.03018182, -1.02199626,  0.06044721, -2.06092573, -0.85059529]])
</pre>

```python
arr[:, 0].sort() # 첫 번째 칼럼의 값을 정렬
```


```python
arr
```

<pre>
array([[-0.62892708,  1.151293  , -1.36398417,  1.01977508, -0.9672169 ],
       [-0.02247658, -0.47572291,  0.284057  , -1.34721628, -1.05052891],
       [ 0.03018182, -1.02199626,  0.06044721, -2.06092573, -0.85059529]])
</pre>
다른 한편으로는 `numpy.sort`를 사용해서 정렬된 배열의 복사본을 생성할 수 있다. 그 외에는 `ndarray.sort`와 똑같은 인자(kind 같은)를 받는다.



```python
arr = np.random.randn(5)

arr
```

<pre>
array([-1.23542121,  2.18355299,  1.39842771,  1.95628808,  1.09050461])
</pre>

```python
np.sort(arr)
```

<pre>
array([-1.23542121,  1.09050461,  1.39842771,  1.95628808,  2.18355299])
</pre>

```python
arr # 원본 배열은 그대로인 모습
```

<pre>
array([-1.23542121,  2.18355299,  1.39842771,  1.95628808,  1.09050461])
</pre>
모든 정렬 메서드는 전달된 축에 독립적으로 정렬을 수행하기 위해 axis 인자를 받는다.



```python
arr = np.random.randn(3, 5)

arr
```

<pre>
array([[-0.12239045, -0.10027588, -1.00220285,  0.26039025, -0.22014135],
       [ 0.33949034,  0.81205641, -0.31321379, -0.67707339,  0.04874022],
       [-0.49431639,  1.16428137, -0.38020551,  1.14940036, -1.33619368]])
</pre>

```python
arr.sort(axis=1) # 칼럼에 대해 정렬
```


```python
arr
```

<pre>
array([[-1.00220285, -0.22014135, -0.12239045, -0.10027588,  0.26039025],
       [-0.67707339, -0.31321379,  0.04874022,  0.33949034,  0.81205641],
       [-1.33619368, -0.49431639, -0.38020551,  1.14940036,  1.16428137]])
</pre>
정렬 메서드는 내림차순 정렬을 위한 옵션이 없으므로 values[::-1]을 이용하자.



```python
arr[:][::-1] 
```

<pre>
array([[-1.33619368, -0.49431639, -0.38020551,  1.14940036,  1.16428137],
       [-0.67707339, -0.31321379,  0.04874022,  0.33949034,  0.81205641],
       [-1.00220285, -0.22014135, -0.12239045, -0.10027588,  0.26039025]])
</pre>
## 간접 정렬: argsort와 lexsort

데이터 분석에서 하나 이상의 키를 기준으로 데이터를 정렬하는 것은 아주 흔한 일이다. 주어딘 단일 키 혹은 여러 개의 키(배열이나 여러 개의 값)로 데이터를 정렬하려면 어떤 순서로 나열해야 하는지 알려주는 정수 인덱스가 담긴 배열을 얻고자 할 경우가 있다. 이를 위해 NumPy는 `argsort`와 `numpy.lexsort`를 제공한다.



```python
values = np.array([5, 0, 1, 3, 2])

indexer = values.argsort()

indexer
```

<pre>
array([1, 2, 4, 3, 0], dtype=int64)
</pre>
팬시 인덱싱과 유사하다.



```python
values[indexer] 
```

<pre>
array([0, 1, 2, 3, 5])
</pre>
다음은 2차원 배열을 첫 번째 로우 순서대로 정렬하는 코드다.



```python
arr = np.random.randn(3, 5)

arr[0] = values

arr
```

<pre>
array([[ 5.        ,  0.        ,  1.        ,  3.        ,  2.        ],
       [-1.48589746, -0.84250269, -0.57369373, -1.415149  ,  0.39090081],
       [-1.58603823,  0.17990872, -1.4638404 ,  2.1820587 , -0.60312445]])
</pre>

```python
arr.argsort()
```

<pre>
array([[1, 2, 4, 3, 0],
       [0, 3, 1, 2, 4],
       [0, 2, 4, 1, 3]], dtype=int64)
</pre>

```python
arr[:, arr[0].argsort()]
```

<pre>
array([[ 0.        ,  1.        ,  2.        ,  3.        ,  5.        ],
       [-0.84250269, -0.57369373,  0.39090081, -1.415149  , -1.48589746],
       [ 0.17990872, -1.4638404 , -0.60312445,  2.1820587 , -1.58603823]])
</pre>
lexsort는 argsort와 유사하지만 다중 키 배열에 대해 간접 사전순 정렬을 수행한다.



```python
first_name = np.array(['Bob', 'Jane', 'Steve', 'Bill', 'Barbara'])
last_name = np.array(['Jones', 'Arnold', 'Arnold', 'Jones', 'Walters'])

sorter = np.lexsort((first_name, last_name))
```


```python
sorter
```

<pre>
array([1, 2, 3, 0, 4], dtype=int64)
</pre>

```python
[(first_name[i], last_name[i]) for i in sorter]
```

<pre>
[('Jane', 'Arnold'),
 ('Steve', 'Arnold'),
 ('Bill', 'Jones'),
 ('Bob', 'Jones'),
 ('Barbara', 'Walters')]
</pre>

```python
ten_digit = np.random.randint(0, 10, size=5)
one_digit = np.random.randint(0, 10, size=5)

print('ten_digit:', ten_digit)
print('one_digit:', one_digit)

sorter = np.lexsort((one_digit, ten_digit))
```

<pre>
ten_digit: [1 5 1 6 7]
one_digit: [3 7 8 4 6]
</pre>

```python
sorter
```

<pre>
array([0, 2, 1, 3, 4], dtype=int64)
</pre>

```python
[(ten_digit[i]*10 + one_digit[i]) for i in sorter]
```

<pre>
[13, 18, 57, 64, 76]
</pre>
lexsort는 <strong>나중에</strong> 넘겨준 배열이 데이터를 정렬하는데 먼저 사용되어서 첫번째 예시에서는 last_name이 first_name보다 먼저, 두번째 예시에서는 ten_digit이 one_digit보다 먼저 정렬되었다.


## 대안 정렬 알고리즘

<strong>견고한</strong><sup>stable</sup>정렬 알고리즘은 동일한 원소의 상대적인 위치를 그대로 둔다. 이는 상대적인 순서가 의미를 가지는 간접 정렬의 경우 특히 중요한 기능이다.



```python
values = np.array(['2:first', '2:second', '1:first', '1:second', '1:third'])

key = np.array([2, 2, 1, 1, 1])

indexer = key.argsort(kind='mergesort')

indexer
```

<pre>
array([2, 3, 4, 0, 1], dtype=int64)
</pre>

```python
values.take(indexer)
```

<pre>
array(['1:first', '1:second', '1:third', '2:first', '2:second'],
      dtype='< U8')
</pre>
이런 경우 사용 가능한 정렬 알고리즘은 0(n log n)의 시간 복잡도를 가지는 mergesort가 유일하다. 하지만 성능은 기본값인 quicksort보다 떨어진다. 다음은 배열 정렬 메서드의 종류이다.



|kind|speed|worst case|work space|stable|
|:---|:---|:---|:---|:---|
|'quicksort'|1|O(n<sup>2</sup>)|0|no|
|'heapsort'|3|O(n\*log(n))|0|no|
|'mergesort'|2|O(n\*log(n))|~n/2|yes|
|'timsort'|2|O(n\*log(n))|~n/2|yes|


## 배열 일부만 정렬하기

NumPy는 k번째 작은 원소를 기준으로 배열을 나누기 위해 최적화된 메서드인 `numpy.partition`과 `np.argpartition`을 제공한다.



```python
arr = np.random.randint(0, 20, size=20)

arr
```

<pre>
array([16,  3, 17, 16, 12, 11,  7,  4, 15,  5, 19,  3,  9,  9, 11, 14,  4,
        9, 16, 10])
</pre>

```python
np.partition(arr, 3)
```

<pre>
array([ 3,  3,  4,  4,  5,  9,  7,  9,  9, 10, 19, 15, 11, 12, 11, 14, 16,
       17, 16, 16])
</pre>
`partition(arr, 3)`을 호출하면 왼쪽에는 3개의 가장 작은 값이 있고 오른쪽에는 나머지 값이 임의의 순서로 채워져 있다. `numpy.argpartition`은 numpy.argsort와 유사하게 해당 원소의 위치를 반환한다.



```python
indices = np.argpartition(arr, 3)

indices
```

<pre>
array([11,  1, 16,  7,  9, 12,  6, 17, 13, 19, 10,  8,  5,  4, 14, 15,  3,
        2, 18,  0], dtype=int64)
</pre>

```python
arr.take(indices)
```

<pre>
array([ 3,  3,  4,  4,  5,  9,  7,  9,  9, 10, 19, 15, 11, 12, 11, 14, 16,
       17, 16, 16])
</pre>
## numpy.searchsorted: 정렬된 배열에서 원소 찾기

`searchsorted`는 정렬된 배열에서 이진 탐색을 수행해 새로운 값을 삽입할 때 정렬된 상태를 계속 유지하기 위한 위치를 반환하는 메서드다.



```python
arr = np.array([0, 1, 7, 12, 15]) # 정렬된 배열

arr.searchsorted(9) # 9가 들어갈 인덱스 위치는 3
```

<pre>
3
</pre>
값이 담긴 배열을 넘기면 해당 원소별로 알맞은 위치를 담고 있는 배열을 반환한다.



```python
arr.searchsorted([0, 8, 11, 16])
```

<pre>
array([0, 3, 3, 5], dtype=int64)
</pre>
`searchsorted`메서드는 기본적으로 동일한 값의 그룹의 왼쪽에서부터 인덱스를 반환한다.



```python
arr = np.array([0, 0, 0, 1, 1, 1, 1])

arr.searchsorted([0, 1])
```

<pre>
array([0, 3], dtype=int64)
</pre>

```python
arr.searchsorted([0, 1], side='right')
```

<pre>
array([3, 7], dtype=int64)
</pre>
`searchsorted`의 다른 활용법으로, 0부터 10,000까지의 값을 특정 구간별로 나눈 배열을 살펴보자.



```python
data = np.floor(np.random.uniform(0, 10000, size=50))

bins = np.array([0, 100, 1000, 5000, 10000])

data
```

<pre>
array([7189., 2360., 3115., 3256., 9175., 1320., 7413., 3957., 7385.,
       8349., 8016.,  132.,  777., 3023., 9255., 8572., 4943., 1310.,
       2878.,  738., 3253., 6858., 4394., 8195., 9761., 2164., 8665.,
       4880., 5240., 9479., 2652., 9516.,  319., 1468., 1202., 4993.,
       9811., 4295., 1715.,  384., 2402., 1514., 2881., 7338., 9250.,
       2646., 1691., 3669., 2429., 7677.])
</pre>
그리고 각 데이터가 어떤 구간에 속해야 하는지 알아보기 위해 `searchsorted` 메서드를 사용하자(여기서 1은 [0, 100) 구간을 의미한다).



```python
labels = bins.searchsorted(data)

labels
```

<pre>
array([4, 3, 3, 3, 4, 3, 4, 3, 4, 4, 4, 2, 2, 3, 4, 4, 3, 3, 3, 2, 3, 4,
       3, 4, 4, 3, 4, 3, 4, 4, 3, 4, 2, 3, 3, 3, 4, 3, 3, 2, 3, 3, 3, 4,
       4, 3, 3, 3, 3, 4], dtype=int64)
</pre>
이 외에도 데이터를 동등한 크기로 분할하는 함수인 `np.quantile`, `np.percentile` 도 찾아보자.


간단하게 설명하자면, `np.quantile`은 주어진 데이터를 동등한 크기로 분할하는 지점을 구해준다. 다음은 0부터 100까지의 수에서 하위 20%, 40%, 60%, 80% 지점을 구하는 예시다.



```python
arr = np.arange(101)

np.quantile(arr, [0.2, 0.4, 0.6, 0.8])
```

<pre>
array([20., 40., 60., 80.])
</pre>
`np.percentile`은 주어진 데이터를 100등분하는 지점을 구해준다.



```python
np.percentile(arr, 40)
```

<pre>
40.0
</pre>
# 고급 배열 입출력

`np.save`와 `np.load`를 사용해서 배열을 이진 형식으로 디스크에 저장할 수 있다. 이를 좀 더 우아하게 사용할 수 있는 몇 가지 부가적인 옵션이 존재하는데 특히 메모리 맵은 RAM에 적재할 수 없는 데이터를 다룰 때 추가적인 이점을 얻을 수 있다.


## 메모리 맵 파일

<strong>메모리 맵 파일</strong><sup>memory-mapped file</sup>은 디스크에 저장된 아주 큰 이진 데이터를 메모리에 적재된 배열처럼 취급할 수 있다. NumPy에는 ndarray와 유사한 memmap 객체가 있는데, 배열 전체를 메모리에 적재하지 않고 큰 파일의 작은 부분을 읽고 쓸 수 있도록 해준다. 게다가 memmap 객체는 메모리에 적재된 배열에서 제공하는 것과 동일한 메서드를 제공하기 때문에 ndarray를 사용해야 하는 많은 알고리즘에서 ndarray의 대체제로 사용할 수 있다.


새로운 memmap 객체를 생성하려면 `np.memmap` 함수에 파일 경로, dtype, 모양 그리고 파일 모드를 전달한다.



```python
mmap = np.memmap('mymmap', dtype='float64', mode='w+',
                 shape=(10000, 10000))

mmap
```

<pre>
memmap([[0., 0., 0., ..., 0., 0., 0.],
        [0., 0., 0., ..., 0., 0., 0.],
        [0., 0., 0., ..., 0., 0., 0.],
        ...,
        [0., 0., 0., ..., 0., 0., 0.],
        [0., 0., 0., ..., 0., 0., 0.],
        [0., 0., 0., ..., 0., 0., 0.]])
</pre>
memmap 객체의 슬라이스는 디스크에 있는 데이터에 대한 뷰를 반환한다.



```python
section = mmap[:5]
```

여기에 데이터를 대입하면 (파이썬의 파일 객체처럼) 메모리에 잠시 보관되어 있다가 `flush`를 호출하면 디스크에 기록한다.



```python
section[:] = np.random.randn(5, 10000)

mmap.flush()
```


```python
mmap
```

<pre>
memmap([[-0.06134446, -0.32647758,  0.83778199, ...,  0.31465339,
          2.43194256, -0.75797056],
        [ 0.53693815, -1.7499983 ,  0.99600396, ...,  1.85265697,
          0.32907461, -0.12743858],
        [-0.13575939,  0.09543895, -0.83802965, ..., -0.0556586 ,
         -2.11716781,  0.57758809],
        ...,
        [ 0.        ,  0.        ,  0.        , ...,  0.        ,
          0.        ,  0.        ],
        [ 0.        ,  0.        ,  0.        , ...,  0.        ,
          0.        ,  0.        ],
        [ 0.        ,  0.        ,  0.        , ...,  0.        ,
          0.        ,  0.        ]])
</pre>
해당 경로에 mmap 파일이 생성되었다. 
<img src="../../images/2022_07_31_image/mmap.png">

<br>
```python
del mmap # mamp 삭제
```


```python
mmap
```

메모리 맵은 스코프를 벗어나서 메모리가 회수되면 디스크에 변경 사항이 기록된다. <strong>기존의 메모리 맵 파일을 열 때</strong> 메타데이터 없이 디스크에 저장된 이진 데이터 파일처럼 dtype과 모양을 지정할 수 있다.



```python
mmap = np.memmap('mymmap', dtype='float64', shape=(10000, 10000))

mmap
```

<pre>
memmap([[-0.06134446, -0.32647758,  0.83778199, ...,  0.31465339,
          2.43194256, -0.75797056],
        [ 0.53693815, -1.7499983 ,  0.99600396, ...,  1.85265697,
          0.32907461, -0.12743858],
        [-0.13575939,  0.09543895, -0.83802965, ..., -0.0556586 ,
         -2.11716781,  0.57758809],
        ...,
        [ 0.        ,  0.        ,  0.        , ...,  0.        ,
          0.        ,  0.        ],
        [ 0.        ,  0.        ,  0.        , ...,  0.        ,
          0.        ,  0.        ],
        [ 0.        ,  0.        ,  0.        , ...,  0.        ,
          0.        ,  0.        ]])
</pre>
메모리 맵은 디스크상의 ndarray이므로 위에서 설명한 것처럼 구조화된 dtype을 사용해도 된다.


## HDF5 및 기타 배열 저장 옵션

PyTables와 h5py는 효율적이고 HDF5[^1] 형식으로 압축이 가능하도록 배열 데이터를 저장할 수 있게 하는 NumPy 친화적인 인처페이스의 파이썬 프로젝트다. 수백 기가 혹은 수 테라바이트의 데이터를 HDF5 형식으로 안전하게 저장할 수 있다.

[^1]: Hierarchical Data Format의 약어로 계층적 데이터 포맷을 의미한다.

<br>
# 성능 팁

NumPy를 활용하는 코드에서 좋은 성능을 이끌어내는 방법은 꽤 직관적인데, 순수 파이썬 반복문은 상대적으로 매우 느리므로 일반적으로 배열 연산으로 대체한다. 다음은 염두에 두면 좋은 간략한 팁이다.



- 파이썬 반복문과 조건문을 배열 연산과 불리언 배열 연산으로 변환한다.

- 가능하면 브로드캐스팅을 사용한다.

- 배열의 뷰(슬라이스)를 사용해서 데이터를 복사하는 것을 피한다.

- ufunc 메서드를 활용한다.



NumPy만으로 원하는 성능을 이끌어내지 못한다면 코드를 C나 포트란으로 작성하거나 Cython을 사용해서 성능을 높일 수 있다.

<h2>관련 포스트 더 보기</h2>
<li> <a href='https://sameta-cani.github.io/numpy/NumPy01/' target='blank'>NumPy01: NumPy는 무엇인가?</a></li>
<li> <a href='https://sameta-cani.github.io/numpy/NumPy02/' target='blank'>NumPy02: ndarray, 인덱싱, 축</a></li>
<li> <a href='https://sameta-cani.github.io/numpy/NumPy03/' target='blank'>NumPy03: 유니버셜 함수, 배열지향 프로그래밍, 파일 입출력, 선형대수, 난수 생성</a></li>
<li> <a href='https://sameta-cani.github.io/numpy/Advanced-NumPy01/' target='blank'>Advanced NumPy01: ndarray 객체 구조, 고급 배열 조작 기법, 브로드캐스팅, 고급 ufunc 사용법</a></li>
<li> <a href='https://sameta-cani.github.io/numpy/Example-of-going-up-and-down-stairs/' target='blank'>Example of going up and down stairs: 간단한 NumPy 실습</a></li>