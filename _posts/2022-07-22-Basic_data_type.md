---
layout: single
title:  "Basic data type"
categories: 
tag: [python]
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


pandas나 NumPy 같은 애드온 라이브러리는 대규모 데이터 계산을 위한 진보된 기능을 제공하지만, 내장되어 있는 기능은 파이썬 내장 자료 처리 도구와 함께 사용해야 한다.



먼저 파이썬의 기본 자료구조인 튜플<sup>tuple</sup>, 리스트<sup>list</sup>, 사전<sup>dict</sup> 그리고 집합<sup>set</sup>부터 알아보고 재사용 가능한 파이썬 함수<sup>function</sup>를 작성하는 방법을 살펴본다. 마지막으로 파이썬의 file 객체의 원리를 살펴보고 하드디스크에 직접 파일을 읽고 쓰는 방식을 알아볼 것이다.


# 자료구조와 순차 자료형


## 튜플

튜플은 1차원의 고정된 크기를 가지는 변경 불가능한 순차 자료형이다. 튜플을 생성하는 가장 쉬운 방법은 쉼표로 구분된 값을 대입하는 것이다.

> <center>[ 변경이 불가능한 자료형이 왜 필요할까? ]</center> <br>"변경이 불가능한 자료형은 변경 가능한 자료형에 비해 소프트웨어의 성능을 향상하는데 도움을 줍니다. 변경 가능한 자료형과는 달리 데이터를 할당할 공간의 내용이나 크기가 달라지지 않기 때문에 생성 과정이 간단하고, 데이터가 오염되지 않을 것이라는 보장이 있기 때문에 복사본을 만드는 대신 그냥 원본을 사용해도 되기 때문입니다.  <br><br>사실 이런 성능보다도, 프로그래머가 자기 코드를 신뢰할 수 있다는 것이 변경이 불가능한 자료형의 가장 큰 장점입니다. 프로그래머가 수천~수만 줄의 코드를 작성하다보면 변경되지 않아야 할 데이터를 오염시키는 버그를 만들 가능성이 높습니다. 이런 실수를 몇 군데 해놓으면 어디에서 문제가 생겼는지를 찾아내기가 상당히 어렵습니다. 그래서 코드를 설계할 때부터 변경이 가능한 데이터와 그렇지 않은 데이터를 정리해서 코드에 반영하는 것이 필요합니다.<br><br>* 출처 : '뇌를 자극하는 파이썬 3', 박상현 지음, 한빛미디어[^tuple_re]


[^tuple_re]: 출처: https://rfriend.tistory.com/331?category=695562 [R, Python 분석과 프로그래밍의 친구 (by R Friend):티스토리]



```python
tup = 4, 5, 6

tup
```

<pre>
(4, 5, 6)
</pre>
괄호를 사용해서 값을 묶어주면 중첩된 튜플을 정의할 수 있다.



```python
nested_tup = (4, 5, 6), (7, 8)

nested_tup
```

<pre>
((4, 5, 6), (7, 8))
</pre>
모든 순차 자료형이나 이터레이터는 `tuple` 메서드를 호출해 튜플로 변환할 수 있다.



```python
tuple([4, 0, 2])
```

<pre>
(4, 0, 2)
</pre>

```python
tup = tuple('string')

tup
```

<pre>
('s', 't', 'r', 'i', 'n', 'g')
</pre>
튜플의 각 원소는 대괄호 []를 이용해 다른 순차 자료형처럼 접근할 수 있다. C, C++, Java 그리고 다른 많은 언어처럼 순차 자료형의 색인은 0부터 시작한다.



```python
tup[0]
```

<pre>
's'
</pre>
튜플에 저장된 객체 자체는 변경이 가능하지만 한 번 생성되면 각 슬롯에 저장된 객체를 변경하는 것은 불가능하다.



```python
tup = tuple(['foo', [1, 2], [True]])

tup
```

<pre>
('foo', [1, 2], [True])
</pre>

```python
tup[2] = False
```

튜플 내에 저장된 객체는 그 위치에서 바로 변경이 가능하다.



```python
tup[1].append(3)

tup
```

<pre>
('foo', [1, 2, 3], [True])
</pre>
`+` 연산자를 이용해서 튜플을 이어붙일 수 있다.



```python
(4, None, 'foo') + (6, 0) + ('bar',) 
# 요소가 하나만 들어간 튜플을 생성하고 싶은 경우 ('string',) 이런 식으로 생성
```

<pre>
(4, None, 'foo', 6, 0, 'bar')
</pre>
튜플에 정수를 곱하면 리스트와 마찬가지로 튜플의 복사본이 반복되어 늘어난다.



```python
('foo', 'bar') * 4
```

<pre>
('foo', 'bar', 'foo', 'bar', 'foo', 'bar', 'foo', 'bar')
</pre>
튜플 안에 있는 객체는 복사되지 않고 그 객체에 대한 참조만 복사된다는 점을 기억하자.


파이썬 튜플 내장함수인 `len`은 튜플의 길이를 반환한다.



```python
print(tup)
print('tup의 길이는', len(tup))
```

<pre>
(4, 5, (6, 7))
tup의 길이는 3
</pre>
파이썬 튜플 내장함수인 `max`와 `min`은 각각 튜플 내 최대값과 최소값을 반환한다.



```python
values = 2, 1, 3, 5, 4, 7, 10
print('최대값: %d, 최소값: %d' %(max(values), min(values)))
```

<pre>
최대값: 10, 최소값: 1
</pre>
### 튜플에서 값 분리하기

만일 튜플과 같은 표현의 변수에 튜플을 <strong>대입</strong>하면 파이썬은 등호(=) 오른쪽에 있는 변수에서 값을 <strong>분리</strong>한다.



```python
tup = (4, 5, 6)
a, b, c = tup
b
```

<pre>
5
</pre>
중첩된 튜플을 포함하는 순차 자료형에서도 값을 분리해낼 수 있다.



```python
tup = 4, 5, (6, 7)
a, b, (c, d) = tup
d
```

<pre>
7
</pre>
튜플을 사용하면 변수의 이름을 서로 바꿀 수 있다.



```python
a, b = 1, 2
b, a = a, b
b
```

<pre>
1
</pre>

```python
seq = [(1, 2, 3), (4, 5, 6), (7, 8, 9)]

for a, b, c in seq:
    print('a={0}, b={1}, c={2}'.format(a, b, c))
```

<pre>
a=1, b=2, c=3
a=4, b=5, c=6
a=7, b=8, c=9
</pre>
튜플의 처음 몇몇 값을 '끄집어내야'하는 상황을 위해 튜플에서 값을 분리하는 특수한 문법인 \*rest를 사용하는데 함수의 시그니처에서 길이를 알 수 없는 긴 인자를 담기 위한 방법으로도 사용된다.



```python
values = 1, 2, 3, 4, 5
a, b, *rest = values # 불필요한 변수라는 것을 나타내기 위해 _를 사용하는 관습도 있다.
a, b
```

<pre>
(1, 2)
</pre>

```python
rest
```

<pre>
[3, 4, 5]
</pre>
### 튜플 메서드

튜플의 크기와 내용은 변경 불가능한 이뮤터블 객체이므로 인스턴스 메서드가 많지 않다.


주어진 값과 같은 값이 몇 개 있는지 반환하는 `count` 메서드다(리스트에서도 사용 가능하다).



```python
a = (1, 2, 2, 2, 3, 4, 2)

a.count(2)
```

<pre>
4
</pre>
주어진 값의 위치를 반환하는 `index` 메서드다(값이 2개인 경우 처음 위치만 반환한다).



```python
a.index(2) # 2의 위치는 1, 2, 3, 6이지만 처음 위치인 1만 반환
```

<pre>
1
</pre>
## 리스트

튜플과는 대조적으로 리스트는 크기나 내용의 변경이 가능하다. 리스트는 대괄호 []나 `list` 함수를 사용해서 생성할 수 있다.



```python
a_list = [2, 3, 7, None]

tup = ('foo', 'bar', 'baz')

b_list = list(tup)

b_list
```

<pre>
['foo', 'bar', 'baz']
</pre>

```python
b_list[1] = 'peekaboo' # 변경 가능!
b_list
```

<pre>
['foo', 'peekaboo', 'baz']
</pre>
리스트와 튜플은 의미적으로 비슷한(비록 튜플은 수정할 수 없지만) 객체의 1차원 순차 자료형이며 많은 함수에서 교차적으로 사용할 수 있다.



`list` 함수는 이터레이터나 제너레이터 표현에서 실제 값을 모두 담기 위한 용도로도 자주 사용된다.



```python
gen = range(10)

gen
```

<pre>
range(0, 10)
</pre>

```python
list(gen)
```

<pre>
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
</pre>
크기가 N이고, 모든 값이 0인 1차원 리스트를 초기화하는 방법이다.



```python
n = 10
a = [0] * n
print(a)
```

<pre>
[0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
</pre>

### 원소 추가하고 삭제하기

`append` 메서드를 사용해서 리스트의 끝에 새로운 값을 추가할 수 있다.



```python
b_list.append('dwarf')
b_list
```

<pre>
['foo', 'peekaboo', 'baz', 'dwarf']
</pre>
`insert` 메서드는 리스트의 특정 위치에 값을 추가할 수 있다.



```python
b_list.insert(1, 'red')
b_list
```

<pre>
['foo', 'red', 'peekaboo', 'baz', 'dwarf']
</pre>
`insert`는 `append`에 비해 연산비용이 많이 든다. `insert`로 값을 추가하면 추가된 위치 이후의 원소들을 새로 추가될 원소를 위해 내부적으로 모두 자리를 옮겨야 하기 때문이다. 순차 자료형의 시작과 끝 지점에 원소를 추가하고 싶다면 이런 용도로 사용할 수 있는 양방향 큐인 `collections.deque`를 사용하자.


`pop` 메서드는 특정 위치의 값을 반환하고 해당 값을 리스트에서 삭제한다.



```python
b_list.pop(2)
```

<pre>
'peekaboo'
</pre>

```python
b_list
```

<pre>
['foo', 'red', 'baz', 'dwarf']
</pre>
`remove` 메서드는 리스트의 제일 앞에 위치한 해당 값의 원소부터 삭제할 수 있다.



```python
b_list.append('foo') # 리스트의 마지막에 'foo' 추가
```


```python
b_list
```

<pre>
['foo', 'red', 'baz', 'dwarf', 'foo']
</pre>

```python
b_list.remove('foo')
```


```python
b_list
```

<pre>
['red', 'baz', 'dwarf', 'foo']
</pre>
위 `insert` 메스드와 동일하게 `remove` 메서드는 연산비용이 많이 든다. 성능이 큰 문제가 되지 않는다면 `append`와 `remove` 메서드를 사용해서 파이썬의 리스트를 여러 종류의 데이터를 담을 수 있는 자료구조로 사용할 수 있다.


`in` 예약어를 사용해서 리스트에 어떤 값이 있는지 검사할 수 있다.



```python
'dwarf' in b_list
```

<pre>
True
</pre>
`not` 예약어를 사용해서 `in` 예약어를 반대 의미로 사용할 수도 있다.



```python
'dwarf' not in b_list
```

<pre>
False
</pre>
리스트에 어떤 값이 있는지 검사하는 것은 리스트의 모든 값을 일일이 검사해야 하므로 해시 테이블을 사용한 파이썬의 사전이나 집합 자료구조처럼 즉각적으로 반환하지 않고 많이 느리다는 점을 기억하자.


### 리스트 이어붙이기

튜플과 마찬가지로 `+`연산자를 이용하면 두 개의 리스트를 합칠 수 있다.



```python
[4, None, 'foo'] + [7, 8, (2, 3)]
```

<pre>
[4, None, 'foo', 7, 8, (2, 3)]
</pre>
만약 리스트를 미리 정의해두었다면 `extend` 메서드를 사용해서 여러 개의 값을 추가할 수 있다.



```python
x = [4, None, 'foo']

x.extend([7, 8, (2, 3)])

x
```

<pre>
[4, None, 'foo', 7, 8, (2, 3)]
</pre>
다만 리스트를 이어붙이면 새로운 리스트를 생성한 후 값을 복사하는 방식이라서 상대적으로 연산비용이 높다. 큰 리스트일수록 `extend` 메서드를 사용해서 기존의 리스트에 값을 추가하는 방식이 일반적으로 더 나은 선택이다.


### 정렬

`sort` 함수를 이용해서 새로운 리스트를 생성하지 않고 있는 그대로 리스트를 정렬할 수 있다.



```python
a = [7, 2, 5, 1, 3]

a.sort() # 보통 오름차순으로 정렬

a
```

<pre>
[1, 2, 3, 5, 7]
</pre>
`sort`는 정렬 기준을 함수로 정의할 수 있다. 예를 들어 문자열의 길이를 기준으로 정렬할 수 있다.



```python
b = ['saw', 'small', 'He', 'foxes', 'six']

b.sort(key=len) # len() 함수는 문자열의 길이를 반환

b
```

<pre>
['He', 'saw', 'six', 'small', 'foxes']
</pre>
`sort` 함수는 원본 리스트를 정렬하는 방식이고, `sorted` 함수는 정렬된 복사본을 생성한다.



```python
a = [7, 2, 5, 1, 3]

sorted(a) # 복사본을 반환
```

<pre>
[1, 2, 3, 5, 7]
</pre>

```python
a # 정렬을 했지만 원본은 그대로인 모습
```

<pre>
[7, 2, 5, 1, 3]
</pre>
### 이진 탐색과 정렬된 리스트 유지하기

내장 bisect 모듈은 이진 탐색과 정렬된 리스트에 값을 추가하는 기능을 제공한다. `bisect.bisect` 메서드는 값이 추가될 때 리스트가 정렬된 상태를 유지할 수 있는 위치를 반환하며 `bisect.insort`는 실제로 정렬된 상태를 유지한 채 값을 추가한다.



```python
import bisect # bisect 모듈 불러오기

c = [1, 2, 2, 2, 3, 4, 7]

bisect.bisect(c, 2) # 배열 c에서 2가 들어갈 색인 위치는 4이다. 중복된 값이 있을 경우 가장 마지막 색인
```

<pre>
4
</pre>

```python
bisect.bisect(c, 5)
```

<pre>
6
</pre>

```python
bisect.insort(c, 6) # 6을 정렬을 유지한 채로 추가
```


```python
c
```

<pre>
[1, 2, 2, 2, 3, 4, 6, 7]
</pre>
bisect 모듈 함수는 리스트가 정렬된 상태인지 검사하지 않으므로 연산비용이 높을 수 있다. 그리고 정렬되지 않은 리스트에 대해 모듈 함수를 수행하면 오류 없이 수행되지만 정확하지 않은 값을 반환하게 된다.


### 슬라이싱

리스트와 같은 자료형(배열, 튜플, ndarray)은 색인 연산자 [] 안에 start:stop을 지정해서 원하는 크기만큼 잘라낼 수 있다.



```python
seq = [7, 2, 3, 7, 5, 6, 0, 1]

seq[1:5]
```

<pre>
[2, 3, 7, 5]
</pre>
슬라이스에 다른 순차 자료형을 대입하는 것도 가능하다.



```python
seq[3:4] = [6, 3] # 7, 5 -> 6, 3

seq
```

<pre>
[7, 2, 3, 6, 3, 5, 6, 0, 1]
</pre>
색인의 시작(start) 위치에 있는 값은 포함되지만 끝(stop) 위치에 잇는 값은 포함되지 않으므로 슬라이싱 결과의 개수는 stop - start다.



색인의 시작(start)값이나 끝(stop)값은 생략할 수 있는데, 이 경우 생략된 값은 각각 순차 자료형의 처음 혹은 마지막 값이 된다.



```python
seq[:5] # seq[0:5] 와 동일
```

<pre>
[7, 2, 3, 6, 3]
</pre>

```python
seq[3:] # seq[3:9] 와 동일
```

<pre>
[6, 3, 5, 6, 0, 1]
</pre>
음수 색인은 순차 자료형의 끝에서부터의 위치를 나타낸다.



```python
seq[-4:]
```

<pre>
[5, 6, 0, 1]
</pre>

```python
seq[-6:-2]
```

<pre>
[6, 3, 5, 6]
</pre>
두 번째 콜론 다음에 간격(step)을 지정할 수 있는데, 하나 걸러 다음 원소를 선택하려면 다음과 같이 표현한다.



```python
seq[::2]
```

<pre>
[7, 3, 3, 6, 1]
</pre>
간격 값으로 -1을 사용하면 리스트나 튜플을 역순으로 반환한다.



```python
seq[::-1]
```

<pre>
[1, 0, 6, 5, 3, 6, 3, 2, 7]
</pre>
## 내장 순차 자료형 함수

순차 자료형에 공통적으로 적용되는 매우 유용한 함수다.


### enumerate

이 함수는 순차 자료형에서 현재 아이템의 색인을 함께 처리하고자 할 때 흔히 사용한다. `enumerate` 함수는 (i, value) 튜플을 반환한다.



```python
en = ['zero', 'one', 'two', 'three', 'four', 'five']

for i, value in enumerate(en):
    print('%d는 %s' %(i, value))
```

<pre>
0는 zero
1는 one
2는 two
3는 three
4는 four
5는 five
</pre>
색인을 통해 데이터에 접근할 때 `enumerate`를 사용하는 유용한 패턴은 순차 자료형에서의 값과 그 위치를 dict에 넘겨주는 것이다.



```python
mapping = {}

for i, v in enumerate(en):
    mapping[v] = i
    
mapping
```

<pre>
{'zero': 0, 'one': 1, 'two': 2, 'three': 3, 'four': 4, 'five': 5}
</pre>
### sorted

`sorted` 함수는 정렬된 새로운 순차 자료형을 반환하며 리스트의 `sort` 메서드와 같은 인자를 취한다.



```python
sorted([7, 1, 2, 6, 0, 3, 2])
```

<pre>
[0, 1, 2, 2, 3, 6, 7]
</pre>

```python
sorted('horse race')
```

<pre>
[' ', 'a', 'c', 'e', 'e', 'h', 'o', 'r', 'r', 's']
</pre>
### zip

`zip` 함수는 여러 개의 리스트나 튜플 또는 다른 순차 자료형을 서로 짝지어서 튜플의 리스트를 생성한다.



```python
seq1 = ['foo', 'bar', 'baz']
seq2 = ['one', 'two', 'three']

zipped = zip(seq1, seq2)

list(zipped)
```

<pre>
[('foo', 'one'), ('bar', 'two'), ('baz', 'three')]
</pre>
`zip` 함수는 여러 개의 순차 자료형을 받을 수 있으며 반환되는 리스트의 크기는 넘겨받은 순차 자료형 중 <strong>가장 짧은</strong> 크기로 정해진다.



```python
seq3 = [False, True]

list(zip(seq1, seq2, seq3)) # 가장 짧은 크기를 가진 seq3을 기준으로 반환
```

<pre>
[('foo', 'one', False), ('bar', 'two', True)]
</pre>
`zip` 함수의 아주 흔한 사용 예는 여러 개의 순차 자료형을 동시에 순회하는 경우인데 `enumerate`와 함께 사용되기도 한다.



```python
for i, (a, b) in enumerate(zip(seq1, seq2)):
    print('{0}: {1}, {2}'.format(i, a, b))
```

<pre>
0: foo, one
1: bar, two
2: baz, three
</pre>
`zip` 함수를 사용해서 이렇게 짝지어진 순차 자료형을 다시 풀어낼 수도 있다. 이를 이용해서 리스트의 <strong>로우</strong>를 리스트의 <strong>컬럼</strong>으로 변환하는 것도 가능하다.



```python
pitchers = [('Nolan', 'Ryan'), ('Roger', 'Clemens'),
            ('Schilling', 'Curt')]
first_names, last_names = zip(*pitchers) # 언패킹
```


```python
first_names
```

<pre>
('Nolan', 'Roger', 'Schilling')
</pre>

```python
last_names
```

<pre>
('Ryan', 'Clemens', 'Curt')
</pre>
### reversed

`reversed`는 순차 자료형을 역순으로 순회한다. 다만 `reversed`는 제네레이터라서 list()나 for문으로 모든 값을 다 받아오기 전에는 순차 자료형을 생성하지 않는다.



```python
list(reversed(range(10)))
```

<pre>
[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
</pre>
## 사전

일반적으로는 <strong>해시맵</strong> 또는 <strong>연관 배열</strong>이라고 널리 알려져 있다. 사전은 유연한 크기를 가지는 <strong>키-값</strong> 쌍으로, <strong>키</strong>와 <strong>값</strong>은 모두 파이썬 객체다. 사전을 생성하는 방법은 중괄호 {}를 사용하여 콜론으로 구분된 키와 값을 둘러싸는 것이다. 키는 변경 불가능하고 값은 변경 가능하다.



```python
empty_dict = {}

d1 = {'a': 'some value', 'b': [1, 2, 3, 4]}

d1
```

<pre>
{'a': 'some value', 'b': [1, 2, 3, 4]}
</pre>
리스트나 튜플을 사용하는 것처럼 사전의 값에 접근하거나 값을 입력할 수 있다.



```python
d1[7] = 'an integer'

d1
```

<pre>
{'a': 'some value', 'b': [1, 2, 3, 4], 7: 'an integer'}
</pre>

```python
d1['b']
```

<pre>
[1, 2, 3, 4]
</pre>
사전에 어떤 키가 있는지 확인하는 것도 리스트나 튜플과 같은 문법으로 확인할 수 있다.



```python
'b' in d1
```

<pre>
True
</pre>
`del` 예약어나 `pop` 메서드(값을 반환함과 동시에 해당 키를 삭제한다)를 사용해서 사전의 값을 삭제할 수 있다.



```python
d1[5] = 'some value'

d1
```

<pre>
{'a': 'some value', 'b': [1, 2, 3, 4], 7: 'an integer', 5: 'some value'}
</pre>

```python
d1['dummy'] = 'another value'

d1
```

<pre>
{'a': 'some value',
 'b': [1, 2, 3, 4],
 7: 'an integer',
 5: 'some value',
 'dummy': 'another value'}
</pre>

```python
del d1[5]
```


```python
d1
```

<pre>
{'a': 'some value',
 'b': [1, 2, 3, 4],
 7: 'an integer',
 'dummy': 'another value'}
</pre>

```python
ret = d1.pop('dummy')

ret
```

<pre>
'another value'
</pre>

```python
d1
```

<pre>
{'a': 'some value', 'b': [1, 2, 3, 4], 7: 'an integer'}
</pre>
`keys`와 `values` 메서드는 각각 키와 값이 담긴 이터레이터를 반환한다. 키-값 쌍은 일정한 기준으로 정렬되어 있진 않지만 `keys` 메서드와 `values` 메서드에서 반환하는 리스트는 같은 순서를 가진다.



```python
print(list(d1.keys()), list(d1.values()))
```

<pre>
['a', 'b', 7] ['some value', [1, 2, 3, 4], 'an integer']
</pre>
`update` 메서드는 하나의 사전을 다른 사전과 합칠 수 있고 이미 존재하는 키에 대해서는 이전 값은 사라진다.



```python
d1.update({'b': 'foo', 'c': 12})
```


```python
d1
```

<pre>
{'a': 'some value', 'b': 'foo', 7: 'an integer', 'c': 12}
</pre>
### 순차 자료형에서 사전 생성하기 



```python
mapping = dict(zip(range(5), reversed(range(5))))

mapping
```

<pre>
{0: 4, 1: 3, 2: 2, 3: 1, 4: 0}
</pre>
### 기본값

`get` 메서드는 기본적으로 해당 키가 존재하지 않을 경우 None을 반환하며, `pop` 메서드는 예외를 발생시킨다. 보통 사전에 값을 <strong>대입</strong>할 때는 리스트 같은 다른 컬렉션에 있는 값을 이용하는데, 예를 들어 여러 단어를 시작 글자에 따라 사전에 리스트에 저장하고 싶다면 다음처럼 할 수 있다.



```python
words = ['apple', 'bat', 'bar', 'atom', 'book']
by_letter = {}

for word in words:     # words 리스트에서 단어를 하나씩 가져온다
    letter = word[0]   # letter에는 단어의 첫번째 알파벳이 온다
    if letter not in by_letter: # 만약 첫번째 알파벳이 by_letter 사전의 키값에 없다면
        by_letter[letter] = [word] # dict에 새로운 letter-word 쌍을 생성
    else:                           # 첫번째 알파벳이 by_letter 사전의 키값에 있다면
        by_letter[letter].append(word) # 첫번째 알파벳을 key 값으로 하는 쌍의 값(리스트)에 word 추가

by_letter
```

<pre>
{'a': ['apple', 'atom'], 'b': ['bat', 'bar', 'book']}
</pre>
사전의 `setdefault` 메서드를 바로 이 목적으로 사용한다. 위 코드에서 `if-else` 블록은 다음처럼 작성할 수 있다.



```python
by_letter = {}

for word in words:
    letter = word[0]
    by_letter.setdefault(letter, []).append(word)
    
by_letter
```

<pre>
{'a': ['apple', 'atom'], 'b': ['bat', 'bar', 'book']}
</pre>
내장 collections 모듈은 `defaultdict`라는 유용한 클래스를 담고 있는데, 이 클래스를 사용하면 위 과정을 좀 더 쉽게 할 수 있다. 자료형, 혹은 사전의 각 슬롯에 담길 기본값을 생성하는 함수를 넘겨서 사전을 생성하는 것이다.



```python
from collections import defaultdict
by_letter = defaultdict(list)
for word in words:
    by_letter[word[0]].append(word)

by_letter
```

<pre>
defaultdict(list, {'a': ['apple', 'atom'], 'b': ['bat', 'bar', 'book']})
</pre>
### 유효한 사전 키

사전의 값으로 어떤 파이썬 객체라도 가능하지만 키는 스칼라형(정수, 실수, 문자열)이나 튜플(튜플에 저장된 값 역시 바뀌지 않는 객체여야 한다)처럼 값이 바뀌지 않는 객체만 가능하다. 기술적으로는 <strong>해시 가능</strong>해야 한다는 뜻이다. 어떤 객체가 해시 가능한지(즉, 사전의 키로 사용할 수 있는지)는 `hash` 함수를 사용해서 검사할 수 있다.



```python
hash('string')
```

<pre>
236256455159071107
</pre>

```python
hash((1, 2, (2, 3)))
```

<pre>
-9209053662355515447
</pre>

```python
hash((1, 2, [2, 3])) # 리스트는 변경 가능한 값이므로 해시 가능하지 않음
```

리스트를 키로 사용하기 위한 한 가지 방법은 리스트를 튜플로 변경하는 것이다.



```python
d = {}

d[tuple([1, 2, 3])] = 5

d
```

<pre>
{(1, 2, 3): 5}
</pre>
## 집합

집합<sup>set</sup>은 유일한 원소만 담는 정렬되지 않은 자료형이다. 사전과 유사하지만 값은 없고 키만 가지고 있다고 생각하면 된다. 집합은 두 가지 방법으로 생성할 수 있는데 `set` 함수를 이용하거나 중괄호를 이용해서 생성할 수 있다.



```python
set([2, 2, 2, 1, 3, 3]) # 중복된 값은 제거
```

<pre>
{1, 2, 3}
</pre>

```python
{2, 2, 2, 1, 3, 3}
```

<pre>
{1, 2, 3}
</pre>
집합은 합집합, 교집합, 차집합, 대칭차집합 같은 산술 <strong>집합 연산</strong>을 제공한다. 모든 논리 집합 연산은 연산 결과를 좌항에 대입하는 함수도 따로 제공하여 큰 집합을 다룰 때 유용하게 사용할 수 있다.



|함수|대체 문법|설명|
|:---|:---|:---|
|a.add(x)|N/A|a에 원소 x를 추가한다.|
|a.clear()|N/A|모든 원소를 제거하고 빈 상태로 되돌린다.|
|a.remove(x)|N/A|a에서 원소 x를 제거한다.|
|a.pop()|N/A|a에서 임의의 원소를 제거한다. 비어 있는 경우 KeyError를 발생시킨다.|
|a.union(b)|aㅣb|a와 b의 합집합|
|a.update(b)|a l= b|a에 a와 b의 합집합을 대입한다.|
|a.intersection(b)|a & b|a와 b의 교집합|
|a.intersection_update(b)|a &= b|a에 a와 b의 교집합을 대입한다.|
|a.difference(b)|a - b|a와 b의 차집합|
|a.difference_update(b)|a -= b|a에 a와 b의 차집합을 대입한다.|
|a.symmetric_difference(b)|a ^ b|a와 b의 대칭차집합|
|a.symmetric_difference_update(b)|a ^= b|a에 a와 b의 대칭차집합을 대입한다.|
|a.issubset(b)|N/A|a의 모든 원소가 b에 속할 경우 True|
|a.issuperset(b)|N/A|a가 b의 모든 원소를 포함할 경우 True|
|a.isdisjoint(b)|N/A|a와 b 모두에 속하는 원소가 없을 경우 True|

집합의 내용이 같다면 두 집합은 동일하다.



```python
{1, 2, 3} == {3, 2, 1}
```

<pre>
True
</pre>
## 리스트, 집합, 사전 표기법

<strong>리스트 표기법</strong>을 이용하면 간결한 표현으로 새로운 리스틀 만들 수 있다. 기본 형식은 다음과 같다.

<code>

    [expr for val in collection if condition]

    </code>


이를 반복문으로 구현하면 다음과 같다.

<code>

    result = []

    for val in collection:

        if condition:

            result.append(expr)

    </code>


필터 조건은 생략 가능하다. 예를 들어 문자열 리스트가 있다면 아래처럼 문자열의 길이가 2 이하인 문자열은 제외하고 나머지를 대문자로 바꾸는 게 가능하다.



```python
strings = ['a', 'as', 'bat', 'car', 'dove', 'python']

[x.upper() for x in strings if len(x) > 2]
```

<pre>
['BAT', 'CAR', 'DOVE', 'PYTHON']
</pre>
집합과 사전에 대해서도 리스트 표기법과 같은 방식으로 적용할 수 있다. 다음은 각각에 대한 표기법이다.

<code>

    dict_comp = {key-expr: value-expr for value in collection if condition}

    </code>

    <code>

    set_comp = {expr for value in collection if condition}

    </code>


리스트 표기법과 마찬가지로 집합과 사전 표기법 역시 문법적 관용으로, 간결한 코드 작성을 통해 코드의 가독성을 높여준다.



```python
unique_lengths = {len(x) for x in strings}

unique_lengths
```

<pre>
{1, 2, 3, 4, 6}
</pre>
`map` 함수를 이용해서 함수적으로 표현할 수도 있다.



```python
set(map(len, strings))
```

<pre>
{1, 2, 3, 4, 6}
</pre>

```python
loc_mapping = {val: index for index, val in enumerate(strings)}

loc_mapping
```

<pre>
{'a': 0, 'as': 1, 'bat': 2, 'car': 3, 'dove': 4, 'python': 5}
</pre>
### 중첩된 리스트 표기법



```python
all_data = [['John', 'Emily', 'Michael', 'Mary', 'Steven'],
            ['Maria', 'Juan', 'Javier', 'Natalia', 'Pilar']]
```

각 이름에서 알파벳 e가 2개 이상 포함된 이름의 목록을 구하는 예제이다. 리스트는 `for` 문을 사용해서 다음처럼 구현할 수 있으며 <strong>중첩된 리스트 표기법</strong>을 이용해서 한 번에 구현할 수도 있다.



```python
names_of_interest = []
for names in all_data:
    enough_es = [name for name in names if name.count('e') >= 2]
    names_of_interest.extend(enough_es)

names_of_interest
```

<pre>
['Steven']
</pre>

```python
result = [name for names in all_data for name in names
          if name.count('e') >= 2]

result
```

<pre>
['Steven']
</pre>
리스트 표기법에서 `for` 부분은 중첩의 순서에 따라 나열되며 필터 조건은 끝에 위치한다. 다음은 숫자 튜플이 담긴 리스트를 그냥 단순한 리스트로 변환하는 예제이다.



```python
flattend = []

for tup in some_tuples:
    for x in tup:
        flattend.append(x)
        
flattend
```

<pre>
[1, 2, 3, 4, 5, 6, 7, 8, 9]
</pre>

```python
some_tuples = [(1, 2, 3), (4, 5, 6), (7, 8, 9)]

flattend = [x for tup in some_tuples for x in tup]

flattend
```

<pre>
[1, 2, 3, 4, 5, 6, 7, 8, 9]
</pre>
2차원 리스트를 초기화할 때 매우 효과적으로 사용되고 필수적이다.



```python
# N X M 크기의 2차원 리스트 초기화
n = 3
m = 4
array = [[0] * m for _ in range(n)]
print(array)
```

<pre>
[[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]
</pre>
몇 단계의 중첩이라도 가능하지만 만약 2단계 이상의 중첩이 필요하다면 자료구조 설계에 대해 다시 한 번 생각해봐야 할 것이다.



