---
layout: single
title:  "Basic prepare course"
categories: 
tag: [python]
toc: true
author_profile: false
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


# 주피터 노트북


## 탭 자동완성

대부분의 통합 개발 환경이나 대화형 데이터 분석 환경에 구현되어 있는 기능으로, 셸에서 입력을 하는 동안 탭을 누르면 네임스페이스에서 그 시점까지 입력한 내용과 맞아떨어지는 변수(객체, 함수 등)를 자동으로 찾아준다.

![image.png](attachment:image.png)

어떤 객체의 메서드나 속성 뒤에 마침표를 입력한 후 자동완성 기능을 활용할 수도 있다.

![image-2.png](attachment:image-2.png)

탭 자동완성은 대화형 네임스페이스 검색과 객체 및 모듈 속성의 자동완성뿐만 아니라 파일 경로를 입력(파이썬 문자열 안에서도)한 후 탭을 누르면 입력한 문자열에 맞는 파일 경로를 컴퓨터의 파일 시스템 안에서 찾아서 보여준다. 또한 함수에서 이름을 가진 인자(= 기호까지 포함해서)도 보여준다.

![image-3.png](attachment:image-3.png)


## 자기관찰

변수 이름 앞이나 뒤에 ?기호를 붙이면 그 객체에 대한 일반 정보를 출력한다.

![image.png](attachment:image.png)

이 기능은 객체의 **자기관찰**(인트로스펙션<sup>introspection</sup>)이라고 하는데, 만약 객체가 함수이거나 인스턴스 메서드라면 정의되어 있는 문서<sup>docstring</sup>를 출력해준다.



??를 사용하면 가능한 경우 함수의 소스 코드도 보여준다.


## 표준 IPython 키보드 단축키



|키보드 단축키|내용|

|:------|:---|

|Ctrl-P 또는 위 화살표 키|명령어 히스토리를 역순으로 검색하기|

|Ctrl-N 또는 아래 화살표 키|명령어 히스토리를 최근 순으로 검색하기|

|Ctrl-R|readline 형식의 히스토리 검색(부분 매칭)하기|

|Ctrl-Shift-V|클립보드에서 텍스트 붙여넣기|

|Ctrl-C|현재 실행 중인 코드 중단하기|

|Ctrl-A|커서를 줄의 처음으로 이동하기|

|Ctrl-E|커서를 줄의 끝으로 이동하기|

|Ctrl-K|커서가 놓인 곳부터 줄의 끝까지 텍스트 삭제하기|

|Ctrl-U|현재 입력된 모든 테스트 지우기|

|Ctrl-F|커서를 앞으로 한 글자씩 이동하기|

|Ctrl-B|커서를 뒤로 한 글자씩 이동하기|

|Ctrl-L|화면 지우기|



## 매직 명령어

IPython은 파이썬 자체에 존재하지 않는 '매직'명령어라고 하는 여러 가지 특수한 명령어를 포함하고 있다. 이 매직 명령어는 일반적인 작업이나 IPyhton 시스템의 동작을 쉽게 제어할 수 있도록 설계된 특수한 명령어다. 매직 명령어는 앞에 % 기호를 붙이는 형식으로 사용한다.



|명령어|설명|

|:------|:---|

|%quickref|IPython의 빠른 도움말 표시|

|%magic|모든 매직함수에 대한 상세 도움말 출력|

|%debug|최근 예외 트레이스백의 하단에서 대화형 디버거로 진입|

|%hist|명령어 입력(그리고 선택적 출력) 히스토리 출력|

|%pdb|예외가 발생하면 자동으로 디버거로 진입|

|%paste|클립보드에서 들여쓰기 된 채로 파이썬 코드 가져오기|

|%cpaste|실행할 파이썬 코드를 수동으로 붙여 넣을 수 잇는 프롬프트 표시|

|%page *OBJECT*|객체를 pager를 통해 보기 좋게 출력|

|%run *script.py*|IPython 내에서 파이썬 스크립트 실행|

|%prun *statement*|cProfile을 이용하여 *statement*를 실행하고 프로파일 결과를 출력|

|%time *statement*|*statement*의 단일 실행 시간을 출력|

|%timeit *statement*|*statement*를 여러 차례 실행한 후 평균 실행 시간을 출력. 매우 짧은 시간 안에 끝나는 코드의 시간을 측정할 때 유용|

|%who, %who_ls, %whos|대화형 네임스페이스 내에 정의된 변수를 다양한 방법으로 표시|

|%xdel *variable*|*Variable*을 삭제하고 IPython 내부적으로 해당 객체에 대한 모든 참조를 제거|


# 파이썬

<strong>파이썬은 가독성과 명료성 그리고 명백함을 강조한다.</strong>


## 들여쓰기

파이썬은 R, C++, 자바, 펄 같은 다른 많은 언어와는 다르게 중괄호 대신 공백 문자(탭이나 스페이스)를 사용해서 코드를 구조화한다. 콜론(:)은 코드 블록의 시작을 의미하며 블록이 끝날 때까지 블록 안에 있는 코드는 모두 같은 크기만큼 들여 써야 한다.

<code>

    for x in array:

        if x < pivot:

             less.append(x)

         else:

             greater.append(x)


## 주석

\# 뒤에 오는 문자는 모두 파이썬 인터프리터에서 무시된다. 이를 이용해서 코드에 주석을 달 수 있다. 또한 코드를 지우지 않고 **실행만 되지 않도록** 남겨두고 싶을 때도 활용한다.



```python
for i in range(5):
    # 이 부분은 무시
    #print('출력이 안됩니다.')
    print(i, end=' ')
```

<pre>
0 1 2 3 4 
</pre>
## 함수와 객체 매서드 호출

함수는 괄호와 0개 이상의 인자를 전달해서 호출할 수 있다. 반환되는 값은 선택적으로 변수에 대입할 수 있다. 파이썬의 거의 모든 객체는 함수를 포함하고 있는데 이를 **메서드**라고 하며 객체의 내부 데이터에 접근할 수 있다.


### 변수와 인자 전달

파이썬에서 변수(혹은 **이름**)에 값을 대입하면 대입 연산자 오른쪽에 있는 객체에 대한 **참조**를 생성하게 된다.



```python
a = [1, 2, 3]
```


```python
b = a # b는 a를 참조한다.
```


```python
a.append(4) # b가 a와 같은 객체를 참조하므로 4가 추가된 list객체를 참조한다.
print(b)
```

<pre>
[1, 2, 3, 4]
</pre>
변수에 값을 할당하는 것은 이름을 객체에 연결하는 것이므로 **바인딩**이라고 부른다. 값이 할당된 변수 이름을 때때로 바운드 변수라고 부르기도 한다.


## 동적 참조와 강한 타입

파이썬에서 모든 객체는 특정한 자료형(또는 **클래스**)을 가지며 다음과 같은 어떤 명백한 상황에서만 묵시적인 변환을 수행하는 자료형을 구분하는 **강한 타입**의 언어라고 하는 것이 맞을 것이다.



```python
a = 4.5

b = 2

print('a is {0}, b is {1}'.format(type(a), type(b)))
print(a / b) # b는 int형이지만 묵시적인 변환을 수행하여 연산에 참여
```

<pre>
a is <class 'float'>, b is <class 'int'>
2.25
</pre>
isinstance 함수를 이용하면 객체의 자료형을 검사할 수 있다.



```python
a = 5
isinstance(a, int)
```

<pre>
True
</pre>
## 속성과 메서드

파이썬에서 객체는 일반적으로 속성(객체 내부에 저장되는 다른 파이썬 객체)과 메서드(객체의 내부 데이터에 

접근할 수 있는 함수)를 가진다. 속성과 메서드는 *obj.attribute_name* 문법으로 접근할 수 있다. getattr 함수를 통해 이름으로 접근하는 것도 가능하다.



```python
a = 'foo'
getattr(a, 'split')
```

<pre>
<function str.split(sep=None, maxsplit=-1)>
</pre>
## 덕 타이핑

객체의 자료형에는 관심이 없고 그 객체가 어떤 메서드나 행동을 지원하는지만 알고 싶은 경우 사용한다. 예를 들어 어떤 객체가 **이터레이터**를 구현했다면 순회가 가능한 객체인지 검증할 수 있다.



```python
def isiterable(obj):
    try:
        iter(obj)
        return True
    except TypeError: # iterable 객체 아님
        return False
```


```python
print(isiterable('a string'))
print(isiterable([1, 2, 3]))
print(isiterable(5))
```

<pre>
True
True
False
</pre>

```python
# x의 자료형이 list형이 아니고 순회가 가능하다면 list형으로 재할당
# ex) x = 'a string' 이면, x는 list형은 아니고 순회가 가능하므로
# x의 자료형은 str에서 list형으로 변경
if not isinstance(x, list) and isiterable(x):
    x = list(x)
```

## 모듈 임포트

파이썬에서 <strong>모듈</strong>은 간단히 파이썬 코드가 담긴 .py파일이다.



```python
# some_module.py
PI = 3.141592

def f(x):
    return x + 2

def g(a, b):
    return a + b
```

some_module.py에 정의된 변수와 함수에 접근하려면 같은 디렉터리에 있는 다른 파일에서 다음과 같이 작성한다.



```python
import some_module
result = some_module.f(5) # result = 7
pi = some_module.PI # pi = 3.141592
```

또는 다음과 같이 작성한다.



```python
from some_module import f, g, PI
result = g(5, PI) # result = 8.141592
```

`as` 예약어를 사용하면 모듈을 다른 이름으로 임포트할 수 있다.



```python
import some_module as sm
from some_module import PI, as pi, g as gf # from 후에는 'sm'이 아닌 .py파일의 원본 이름!

r1 = sm.f(pi) # r1 = 5.141592
r2 = gf(6, pi) # r2 = 9.141592
```

## 비교문

두 참조 변수가 같은 객체를 가리키고 있는지 검사하려면 `is` 예약어를 사용한다. `is not`을 사용하면 두 객체가 같지 않은지 검사할 수 있다.



```python
a = [1, 2, 3]
b = a
c = list(a)
```


```python
a is b
```

<pre>
True
</pre>

```python
a is not c # `list`는 항상 새로운 파이썬 리스트를 생성하므로 다른 파이썬 객체를 참조한다.
```

<pre>
True
</pre>
`is`로 비교하는 것과 `==` 연산자로 비교하는 것은 같지 않다. `==` 연산자는 객체 안의 내용이 동일한지 비교하는 연산자이다.



```python
a == c
```

<pre>
True
</pre>
`is`와 `is not`은 변수가 None인지 검사하기 위해 사용하는데, None 인스턴스는 하나만 존재하기 때문이다.



```python
a = None

a is None
```

<pre>
True
</pre>
## 뮤터블, 이뮤터블 객체

파이썬에서 리스트, 사전, NumPy 배열 또는 사용자 정의 클래스 같은 대부분의 객체는 변경 가능하다(뮤터블). 이 말은 객체나 값의 내용을 바꿀 수 있다는 뜻이다.



```python
a_list = ['foo', 2, [4, 5]]
a_list[2] = (3, 4) # [4, 5] -> (3, 4)

a_list
```

<pre>
['foo', 2, (3, 4)]
</pre>
문자열이나 튜플은 변경 불가능하다(이뮤터블).



```python
a_tuple = (3, 5, (4, 5))

a_tuple[1] = 'four'
```

## 스칼라형

파이썬은 숫자 데이터와 문자열, 불리언값 (True 또는 False) 그리고 날짜와 시간을 다룰 수 있는 몇몇 내장 자료형을 제공한다. 이런 '단일 값'을 담는 자료형을 스칼라 타입이라고 하며 날자와 시간을 다루는 방법은 표준 라이브러리의 `datetime` 모듈에서 제공한다.



|자료형|설명|

|:---|:---|

|None|파이썬의 'null'값(하나의 유일한 None 인스턴스만 존재한다.)|

|str|문자열 자료형. 유니코드(UTF-8 인코딩) 문자열|

|bytes|Raw ASCII 바이트(또는 바이트로 인코딩된 유니코드)|

|float|배정밀도(64비트) 부동소수점수. double형이 따로 존재하지 않는다는 점을 기억하자.|

|bool|참(True) 또는 거짓(False)|

|int|부호가 있는(음수 표현이 가능한) 정수. 값의 범위는 플랫폼에 의존적이다.|


### 숫자 자료형

숫자를 위한 파이썬의 주요 자료형은 int와 float다. int는 임의의 숫자를 저장할 수 있다.



```python
ival = 17239871

ival ** 6 # 6제곱
```

<pre>
26254519291092456596965462913230729701102721
</pre>
부동소수점수는 float형으로 나타낸다. 내부적으로 배정밀도(64비트)를 가지는 값이다. float는 과학 표기법(지수 표기법)으로 나타낼 수도 있다.



```python
fval = 7.243
fval2 = 6.78e-5
```

정수 나눗셈은 정수를 반환하지 않고 부동소수점수를 반환한다.



```python
3 / 2 # 자동으로 int형에서 float형으로 형변환
```

<pre>
1.5
</pre>
나눗셈의 결과가 정수가 아닐 경우 몫만을 돌려주는 C 형식의 정수 나눗셈은 `//` 연산자로 계산한다.



```python
3 // 2
```

<pre>
1
</pre>
### 문자열

파이썬은 강력하고 유연한 문자열 처리 기능을 제공한다. <strong>문자열</strong>은 작은 따옴표(')나 큰따옴표(")로 둘러싸서 표현할 수 있다.



```python
a = '문자열을 작은 따옴표로 둘러싼다.'
b = "문자열을 처리하는 다른 방법"
```

개행 문자(\n)포함된 여러 줄에 걸친 문자열은 세 개의 작은따옴표나 큰따옴표로 둘러싼다.



```python
C = """
여러 줄에 걸친 문자열은
따옴표 세 개로 둘러싼다.
""" 
C
```

<pre>
'\n여러 줄에 걸친 문자열은\n따옴표 세 개로 둘러싼다.\n'
</pre>
`count` 메서드는 찾고자 하는 문자의 수를 반환한다.



```python
C.count('\n')
```

<pre>
3
</pre>
파이썬의 문자열은 변경 불가능하다. 위에서 언급한 이뮤터블 객체다.



```python
a = 'this is a string'

a[10] = 'f' # TypeError 발생!
```

많은 파이썬 객체는 `str` 함수를 이용해서 문자열로 변환할 수 있다.



```python
a = 5.6 # a의 자료형은 int형
s = str(a) # str형으로 변환
print(type(s), s)
```

<pre>
<class 'str'> 5.6
</pre>
문자열은 일련의 유니코드 문자이므로 리스트나 튜플 같은 다른 순차적인 자료형과 같이 취급된다.



```python
s = 'python'

list(s)
```

<pre>
['p', 'y', 't', 'h', 'o', 'n']
</pre>
<strong>슬라이싱</strong>이라고 부르는 s[:3] 문법은 파이썬 시퀀스<sup>sequence</sup> 자료구조에 구현되어 있다.



```python
s[:3] # s의 0부터 2번째 자리까지 출력(0='p', 1='y', 2='t')
```

<pre>
'pyt'
</pre>
역슬래시(\)는 <strong>이스케이프 문자</strong>로, 개행 문자(\n)나 유니코드 문자 같은 특수한 목적의 문자를 나타내기 위해 사용한다. 역슬래시를 나타내려면 다음처럼 역슬래시 자체를 이스케이프한다.



```python
s = '12\\34'

print(s)
```

<pre>
12\34
</pre>
특수 문자 없이 역슬래시(\)가 많이 포함된 문자열을 나타내려면 문자열 앞에 `r`을 써서 문자열을 있는 그대로 해석하도록 할 수 있다. 여기서의 `r`은 raw를 뜻한다.



```python
s = r'this\has\no\special\characters'

print(s)
```

<pre>
this\has\no\special\characters
</pre>
두 문자열을 더하면 두 문자열을 이어붙인 새로운 문자열이 생성된다.



```python
a = 'this is the first half'
b = 'and this is the second half'
a + b
```

<pre>
'this is the first halfand this is the second half'
</pre>
문자열 객체는 포맷에 따라 문자열을 대체하여 새로운 문자열을 반환하는 `format` 메서드를 가지고 있다.



```python
templete = '{0:.2f} {1:s} are worth US${2:d}'
```

위 문자열에서



 - {0:.2f}는 첫 번째 인자를 소수점 아래 2자리까지만 표시하는 부동소수점 형태로 출력하라는 의미다.

 - {1:s}는 두 번째 인자가 문자열이라는 의미다.

 - {2:d}는 세 번째 인자가 정수라는 의미다.

 

 

 인자를 이런 포맷 매개변수를 이용해 대치하려면 인자를 `format` 메서드에 전달해야 한다.



```python
templete.format(4.5560, 'Argentine Pesos', 1)
```

<pre>
'4.56 Argentine Pesos are worth US$1'
</pre>
### 바이트와 유니코드

파이썬 3.0부터는 아스키와 비-아스키(아스키가 아닌) 텍스트를 일관되게 다루기 위해 유니코드가 최상위 문자열 타입이 되었다. 파이썬 구 버전에서 문자열은 유니코드 인코딩을 명시하지 않은 바이트였다. 문자 인코딩을 알고 있다는 가정 하에 유니코드로 변환할 수 있었다.



```python
val = "español"
val
```

<pre>
'español'
</pre>
`encode` 메서드를 사용해서 위 유니코드 문자열을 UTF-8 바이트 형식으로 변환할 수 있다.



```python
val_utf8 = val.encode('utf-8')
print(type(val_utf8), val_utf8)
```

<pre>
<class 'bytes'> b'espa\xc3\xb1ol'
</pre>
bytes 객체의 유니코드 인코딩을 알고 있다면 `decode` 메서드를 이용해서 다시 거꾸로 되돌릴 수 있다.



```python
val_utf8.decode('utf-8')
```

<pre>
'español'
</pre>
여러 가지 다른 인코딩을 사용하는 데이터를 만나게 될 수도 있다.



참고 자료: <a href='https://docs.python.org/3/library/codecs.html#standard-encodings' target='blank'>https://docs.python.org/3/library/codecs.html#standard-encodings</a>



```python
val.encode('latin1')
```

<pre>
b'espa\xf1ol'
</pre>

```python
val.encode('utf-16')
```

<pre>
b'\xff\xfee\x00s\x00p\x00a\x00\xf1\x00o\x00l\x00'
</pre>

```python
val.encode('utf-16le')
```

<pre>
b'e\x00s\x00p\x00a\x00\xf1\x00o\x00l\x00'
</pre>
파일을 다룬다면 bytes 객체를 만나게 되는 일은 흔하다. 이렇게 하는 경우는 흔하지 않지만 다음과 같이 문자열 앞에 `b`를 붙여서 바이트 표현임을 나타낼 수도 있다.



```python
bytes_val = b'this is bytes'

bytes_val
```

<pre>
b'this is bytes'
</pre>

```python
decoded = bytes_val.decode('utf8')
decoded # str (유니코드) 타입
```

<pre>
'this is bytes'
</pre>
### 불리언(boolean)

파이썬에서 불리언값은 True와 False다. 비교와 조건식은 True 아니면 False로 해석된다. 불리언값은 `and`와 `or` 예약어로 조합할 수 있다.



```python
True and True
```

<pre>
True
</pre>

```python
False or True
```

<pre>
True
</pre>
### 형변환

str, bool, int, float 자료형은 형변환을 위한 함수로 쓰인다.



```python
s = '3.141592'
fval = float(s) # str -> float
type(fval)
```

<pre>
float
</pre>

```python
int(fval) # float -> int
```

<pre>
3
</pre>

```python
bool(fval) float -> bool
```

<pre>
True
</pre>

```python
bool(0) # 0을 제외한 모든 숫자는 True 이고, 0만이 False 이다.
```

<pre>
False
</pre>
### None

None은 파이썬에서 사용하는 널<sup>null</sup>값이다. 만약 어떤 함수에서 명시적으로 값을 반환하지 않으면 묵시적으로 None을 반환한다.



```python
a = None

a is None
```

<pre>
True
</pre>

```python
b = 5

b is not None
```

<pre>
True
</pre>
또한 None은 함수 인자의 기본값<sup>default</sup>으로 흔히 사용되기도 한다.



```python
def add_and_maybe_multiply(a, b, c=None): # c 인자에 아무 값도 들어오지 않았다면 None이 할당
    result = a + b
    
    if c is not None: # c 인자에 값이 들어왔다면 다음 연산을 실행
        result = result * C
    
    return result
```

기술적인 측면에서 None은 예약어가 아니라 NoneType의 유일한 인스턴스임을 기억하자.



```python
type(None)
```

<pre>
NoneType
</pre>
### 날짜와 시간

파이썬 내장 datetime 모듈은 datetime, date 그리고 time형을 지원한다. datetime형은 이름에서 알 수 있듯이 date와 time 정보를 함께 저장하며 주로 사용되는 자료형이다. 후에 시계열 데이터를 다룰 때 사용한다.



```python
from datetime import datetime, date, time

dt = datetime(2022, 7, 21, 23, 22, 42)

print(dt.day, dt.minute) # 일과 분
```

<pre>
21 22
</pre>
datetime 인스턴스에서 `date` 메서드와 `time` 메서드를 사용해서 해당 `datetime`의 날짜와 시간을 추출할 수 있다.



```python
dt.date()
```

<pre>
datetime.date(2022, 7, 21)
</pre>

```python
dt.time()
```

<pre>
datetime.time(23, 22, 42)
</pre>
`strftime` 메서드는 datetime을 문자열로 만들어준다(str from time).



```python
dt.strftime('%m/%d/%Y %H:%M') # 정해준 format으로 반환
```

<pre>
'07/21/2022 23:22'
</pre>
`strptime` 함수를 이용하면 문자열을 해석하여 datetime 객체로 만들어준다.



```python
datetime.strptime('20220721', '%Y%m%d')
```

<pre>
datetime.datetime(2022, 7, 21, 0, 0)
</pre>
문자열 포맷 규칙은 다음 표를 참고하자.





|포맷|설명|

|:---|:---|

|%Y|4자리 연도|

|%y|2자리 연도|

|%m|2자리 월[01, 12]|

|%d|2자리 일[01, 31]|

|%H|시간(24시간 형식) [00, 23]|

|%I|시간(12시간 형식) [00, 12]|

|%M|2자리 분[00, 59]|

|%S|초[00, 61] (60, 61은 윤초)|

|%w|정수로 나타낸 요일[0(일요일),6(월요일)]|

|%U|연중 주차[00, 53]. 일요일을 그 주의 첫 번째 날로 간주하며, 그 해에서 첫 번째 일요일 앞에 있는 날은 0주차가 된다.|

|%W|연중 주차[00, 53]. 월요일을 그 주의 첫 번째 날로 간주하며, 그 해에서 첫 번째 월요일 앞에 있는 날은 0주차가 된다.|

|%z|UTC 시간대 오프셋을 +HHMM 또는 -HHMM으로 표현한다. 만약 시간대를 신경 쓰지 않는다면 비워둔다.|

|%F|%Y-%m-%d 형식에 대한 축약(예: 2022-7-21)|

|%D| %m/%d/%y 형식에 대한 축약(예: 07/21/22)|


다른 방식으로 그룹핑된 시계열 데이터를 집계할 때 datetime의 필드를 치환하는 것이 유용한 경우가 종종 발생한다. 예를 들어 분과 초 필드를 0으로 치환해서 새로운 객체를 생성할 수 있다.



```python
dt.replace(minute=0, second=0)
```

<pre>
datetime.datetime(2022, 7, 21, 23, 0)
</pre>
datetime.datetime은 변경 불가능하며, 이런 메서드들은 항상 새로운 객체를 반환한다.



두 datetime 객체의 차는 datetime.timedelta 객체를 반환한다.



```python
dt2 = datetime(2022, 8, 15, 22, 30)

delta = dt2 - dt

print(type(delta), delta)
```

<pre>
<class 'datetime.timedelta'> 24 days, 23:07:18
</pre>
timedelta 객체를 datetime 객체에 더하면 그만큼 시간이 미뤄진 datetime 객체를 얻을 수 있다.



```python
dt + delta
```

<pre>
datetime.datetime(2022, 8, 15, 22, 30)
</pre>
## 흐름 제어

파이썬은 다른 프로그래밍 언어와 마찬가지로 조건절과 반복문 그리고 표준 <strong>흐름 제어</strong>를 위한 예약어를 가지고 있다.


### if, elif, else

`if` 문은 조건을 검사하여 그 조건이 True일 경우 `if` 블록 내의 코드를 수행한다.

`if` 문은 부가적으로 하나 이상의 `elif` 블록과 다른 모든 조건이 False인 경우에 수행될 `else` 블록을 가질 수 있다. 만일 이 중 하나의 조건이라도 True면 이후의 `elif`나 `else`블록은 검사하지 않는다. and나 or과 함께 사용하면 이 조건을 왼쪽에서 오른쪽 순서로 검사하며 왼쪽 조건이 True인 경우 오른쪽 조건은 검사하지 않는다.



```python
a = 5; b = 7
c = 8; d = 4

if a < b or c > d: # 이미 왼쪽 조건문이 True이므로 오른쪽의 c > d 조건은 검사하지 않고 if블록 실행
    print('Made it')
```

<pre>
Made it
</pre>
여러 조건을 연결해서 사용하는 것도 가능하다.



```python
4 > 3 > 2 > 1
```

<pre>
True
</pre>
### for 문

`for` 문은 리스트나 튜플 같은 컬렉션이나 이터레이터를 순회한다. `for` 문의 기본 문법은 다음과 같다.

<code>

    for value in collection:

        # value를 이용하는 코드 작성

    </code>


`for` 문은 `continue` 예약어를 사용해서 남은 블록을 건너뛰고 다음 순회로 넘어갈 수 있다.



```python
sequence = [1, 2, None, 4, None, 5]
total = 0
for value in sequence:
    if value is None:
        continue
    total += value

print(total)
```

<pre>
12
</pre>
`for` 문은 `break` 예약어를 사용해서 빠져나갈 수 있다. `break` 예약어는 가장 안쪽에 있는 `for` 문만 빠져나간다. 바깥쪽에 있는 `for` 문은 계속 실행된다.



```python
for i in range(4): # i는 0 ~ 3 까지 순회
    for j in range(4): # j는 0 ~ 3 까지 순회
        if j > i: # 만약 j값이 i값보다 커지면
            break # for j in range(4): 블록을 빠져나가라
        print((i, j))
```

<pre>
(0, 0)
(1, 0)
(1, 1)
(2, 0)
(2, 1)
(2, 2)
(3, 0)
(3, 1)
(3, 2)
(3, 3)
</pre>
컬렉션의 원소나 이터레이터가 순차적인 자료(예를 들면 튜플이나 리스트)라면 `for` 문 안에서 여러 개의 변수로 꺼낼 수 있다.

<code>

    for a, b, c in iterator:

        # 필요한 코드 작성

    </code>


### while 문

`while` 문은 조건을 명시하여 해당 조건이 False가 되거나 `break` 문을 사용해서 명시적으로 반복을 끝낼 때까지 블록 내의 코드를 수행한다.



```python
x = 256
total = 0
while x > 0: # x가 양수면 반복해라
    if total > 500: # 만약 total값이 500보다 크다면
        break # if total > 500: 블록을 탈출해라
    total += x # total에 x를 더해라 256, 128, 64, 32, 16, 8
    x = x // 2 # x에 x를 2로 나눈 몫을 재할당

print(total)
```

<pre>
504
</pre>
### pass

파이썬에서 `pass`는 아무 것도 하지 않음을 나타낸다. 이는 블록 내에서 어떤 작업도 실행하지 않을 때 사용한다(또는 아직 구현하지 않은 코드를 나중에 추가하기 위한 플레이스홀더 용도로 사용한다). `pass`를 사용하는 이유는 파이썬이 공백 문자를 블록으로 구분하는 데 사용하기 때문이다.


<code>

    if x < 0:

        print('negative!)

    elif x == 0:

        # TODO: 여기에 내용 채울 것(아직 미구현)

        pass

    else:

        print('positive!)

             </code>


### range

`range` 함수는 연속된 정수를 넘겨주는 이터레이터를 반환한다.



```python
range(10)
```

<pre>
range(0, 10)
</pre>

```python
list(range(10))
```

<pre>
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
</pre>
start, end, step(음수가 될 수도 있다: end 부터 start 까지 거꾸로 진행) 값을 지정할 수 있다.



```python
list(range(0, 20, 2)) # 0부터 20까지 2씩 건너뛰어서 출력
```

<pre>
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
</pre>

```python
list(range(5, 0, -1))
```

<pre>
[5, 4, 3, 2, 1]
</pre>
`range`는 마지막 값 바로 이전 정수까지의 값을 반환한다. `range` 함수는 일반적으로 색인(인덱스)으로 시퀀스를 반복하기 위해 사용한다.



```python
seq = [1, 2, 3, 4]
for i in range(len(seq)): # len(seq) = 4이므로 i는 0 ~ 3
    val = seq[i]
    print(val)
```

<pre>
1
2
3
4
</pre>
참고로, `range` 함수는 임의 크기로 값을 생성해낼 수 있지만 메모리 사용량은 매우 적다.


### 삼항 표현식

파이썬의 <strong>삼항 표현식</strong>은 `if-else` 블록을 한 줄로 표현할 수 있도록 한다. 문법은 아래와 같다.


<code>

    value = true-expr if condition else false-expr

    </code>


여기서 `true-expr`과 `false-expr`은 어떤 파이썬 표현이라도 상관없다. 삼항 표현식은 `if-else` 블록처럼 조건이 참인 경우의 표현식만 실행된다. 따라서 삼항 표현식에서 `if`와 `else`에 비용이 많이 드는 계산이 올 수 있으며 조건이 참인 파이썬 표현만 실행된다.



```python
x = 5

'Non-negative' if x >=0 else 'Negative'
```

<pre>
'Non-negative'
</pre>