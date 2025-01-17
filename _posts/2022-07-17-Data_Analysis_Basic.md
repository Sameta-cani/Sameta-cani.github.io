---
layout: single
title:  "Data Analysis Basic"
categories: 
tag: [python]
toc: false
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
      line-height: 120%;
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

# 데이터 분석

---

데이터 분석 업무의 80&#126;90%는 데이터를 수집하고 정리하는 일이 차지한다고 한다. 나머지 10&#126;20%는 알고리즘을 선택하고, 모델링 결과를 분석하여 데이터로부터 유용한 정보(information)을 뽑아내는 분석 프로세스의 몫이다. 데이터과학자가 하는 가장 기초적이고 중요한 일은 데이터를 수집하고 분석이 가능한 형태로 정리하는 것이라고 말할 수 있다.

<br>
<strong>여기서 '데이터'는 정확히 무슨 뜻일까?</strong>

주된 의미는 구조화된 데이터(structed data)다.

- 각 컬럼(column)의 형식이 문자열, 숫자, 날짜 등으로 서로 다른 표 혹은 스프레드시트와 비슷한 데이터. 이는 관계형 데이터베이스 혹은 탭(tab)이나 쉼표(commma)로 구분되는 텍스트 파일 형식으로 저장되는 대부분의 데이터를 포함한다.
- 다차원 배열(행렬)
- SQL(Structured Query Language, 구조화 질의어)에서 기본키나 외래키 같은 키 컬럼에 의해 서로 연관되는 여러 가지 표
- 일정하거나 일정하지 않은 간격의 시계열

대부분의 데이터는 모델링이나 분석을 위해 좀 더 쉬운 구조로 형태를 바꿀 수 있다. 또는 데이터 안에서 어떤 특성을 추출해서 구조화된 형태로 만들 수 있다. 예를 들어 뉴스 기사 모음은 사용 단어 빈도표를 만들어 감성 분석에 사용할 수도 있다.

<br>

# 데이터 분석에서의 파이썬

---

파이썬은 작은 프로그램이나 업무 자동화 스크립트를 빠르고 간단하게 만들 수 있는 **스크립트**언어이다.  이러한 파이썬이 과학 기술 컴퓨팅계에서 성공을 하게 된 이유로는 C, C++, 포트란<sup>FORTRAN</sup>코드와 통합이 쉽다는 점을 들 수 있다. 또한, 연구를 하거나 프로토타입을 만드는 데 적합한 언어인데다 분석 애플리케이션, 범용 시스템 그리고 실제 시스템을 개발하는 데도 적합하다.  다음은 파이썬의 또다른 장점이다.

 - 쉽고 뛰어난 개발 생산성으로 전 세계 개발자들이 파이썬을 선호한다. 특히 구글, 페이스북 등의 유수의 IT 업계에서도 파이썬의 높은 생산성으로 인해 활용도가 매우 높다.
 - 오픈 소스 계열의 전폭적인 지원을 받고 있으며 놀라울 정도의 많은 라이브러리로 인해 개발 시 높은 생산성을 보장해 준다.
 - 인터프리터 언어(Interpreter Language)의 특성상 속도는 느리지만, 대신에 뛰어난 확장성, 유연성, 호환성으로 인해 서버, 에트워크, 시스템, IoT, 심지어 데스크톱까지 다양한 영역에서 사용되고 있다.
 - 머신러닝 애플리케이션과 결합한 다양한 애플리케이션 개발이 가능하다.

- EA[^0] 로의 확장 및 마이크로서비스 기반의 실시간 연계 등 다양한 기업 환경으로의 확산이 가능하다.

이런 장점을 갖춘 파이썬에도 단점이 있는데, 파이썬은 인터프리터 언어이므로 Java나 C++ 같은 컴파일 언어보다 많이 느리다. 그래서 실시간 거래 시스템처럼 매우 짧은 응답 시간을 필요로 하는 애플리케이션에서는 가능한 한 최고의 성능을 내고자 생산성은 떨어지지만 C++ 같은 저수준 언어로 개발을 한다. 
추가로, **GIL**<sup>global interpreter lock</sup>(전역 인터프리터 잠금) 매커니즘은 인터프리터가 한 번에 하나의 파이썬 명령만 실행하도록 해서 동시다발적인 멀티스레드를 처리하거나 CPU에 집중된 많은 스레드를 처리하는 애플리케이션에 적합한 언어가 아니다.
하지만, 중요한 점은 **개발자의 시간 비용**은 **CPU의 시간 비용**보다 비싸다는 것이다.

<br>

# 필수 라이브러리

---

### [NumPy](https://numpy.org/)

NumPy(넘파이)는 Numerical Python의 약자로 자료구조, 알고리즘 산술 데이터를 다루는 대부분의 과학 계산 애플리케이션에서 필요한 라이브러리를 제공하며 대표적인 파이썬 기반 수치 해석 라이브러리이다. 다음은 NumPy가 제공하는 기능이다. 

- 빠르고 효울적인 다차원 배열 객체 ndarry
- 배열 원소를 다루거나 배열 간의 수학 계산을 수행하는 함수
- 디스크로부터 배열 기반의 데이터를 읽거나 쓸 수 있는 도구
- 선형대수[^1] 계산, 푸리에 변환[^2], 난수 생성기[^3]
- 파이썬 확장과 C, C++ 코드에서 NumPy의 자료구조에 접근하고 계산 기능을 사용할 수 있도록 해주는 C API

루프를 사용하지 않고 대량 데이터의 배열 연산을 가능하게 하므로 빠른 배열 연산 속도를 보장한다. 대량 데이터 기반의 과학과 공학 프로그램은 빠른 계산 능력이 매우 중요하므로 파이썬 기반의 많은 과학과 공학 패키지는 넘파이에 의존하고 있다. 
넘파이API는 매우 넓은 범위를 다루고 있으므로 머신러닝 애플리케이션을 작성할 때 중요하게 활용될 수 있는 핵심 개념 위주로 숙지하는 것이 좋다. ex) Dimension, axis, etc.

설치 명령어는 cmd에서 `pip install numpy`를 입력한다.

참고 사이트: <a href='https://sebastianraschka.com/pdf/books/dlb/appendix_f_numpy-intro.pdf' target='blank'>https://sebastianraschka.com/pdf/books/dlb/appendix_f_numpy-intro.pdf</a>

### [pandas](https://pandas.pydata.org/)

pandas(판다스)는 구조화된 데이터나 표 형식의 데이터를 빠르고 쉽고 표현적으로 다루도록 설계된 고수준의 자료구조와 함수를 제공한다.  주된 목표는 서로 다른 형식을 갖는 여러 종류의 데이터를 컴퓨터가 이해할 수 있도록 동일한 형식을 갖는 구조로 통합하는 것이다. 이를 위해 판다스는 1차원 배열 객체인 Series(시리즈)와 표 형태의 row와 column 이름을 가지는 DataFrame(데이터프레임)이라는 구조화된 데이터 형식을 제공한다.

일반적으로 대부분의 데이터 세트는 2차원 데이터 즉, 행(Row) x 열(Column)로 구성돼 있다. 행과 열의 2차원 데이터가 인기 있는 이유는 바로 인간이 가장 이해하기 쉬운 데이터 구조이면서도 효과적으로 데이터를 담을 수 있는 구조이기 때문이다. 판다스는 이처럼 행과 열로 이뤄진 2차원 데이터를 효율적으로 가공/처리할 수 있는 다양하고 훌륭한 기능을 제공한다.

설치 명령어는 cmd에서 `pip install pandas`를 입력한다.

참고 사이트: <a href='https://pandas.pydata.org/pandas-docs/stable/user_guide/10min.html' target='blank'>https://pandas.pydata.org/pandas-docs/stable/user_guide/10min.html</a>

### [matplotlib](https://matplotlib.org/)

matplotlib(맷플롯립)은 그래프나 차트 등 그래픽으로 표현하는 데 사용하는 파이썬 기반 2D 시각화 도구이다. 판다스와 연계하여 데이터를 다양한 방식으로 시각화하는 기능을 제공한다. 데이터와 분석 결과를 다양한 관점에서 시각화해보면 매우 중요한 통찰을 얻을 수 있다. 하지만, 맷플롯립은 너무 세분화된 API로 익히기가 번거롭고 시각적인 디자인 부분에서도 투박한 면이 있다. 이를 보완하기 위해 Seaborn(시본)을 대표적으로 사용한다. 시본은 맷플롯립을 기반으로 만들었지만, 판다스와의 쉬운 연동, 더 함축적인 API, 분석을 위한 다양한 유형의 그래프/차트 제공 등으로 파이썬 기반의 데이터 분석가/과학자에게 인기를 얻고 있다.


설치 명령어는 cmd에서 `pip install matplotlib`를 입력한다.

참고 사이트: <a href='https://matplotlib.org/1.5.3/users/beginner.html' target='blank'> https://matplotlib.org/1.5.3/users/beginner.html</a>

### [SciPy](https://scipy.org/)

SciPy(사이파이)는 과학 계산 컴퓨팅 영역의 여러 기본 문제를 다루는 패키지 모음이다. 다음은 SciPy에 포함된 패키지 중 일부다.

 - **scipy.integrate**<br>

   수치적분 루틴과 미분방적식 풀이법

 - **scipy.linalg**<br>
   numpy.linalg에서 제공하는 것보다 더 확장된 선형대수 루틴과 매트릭스 분해

 - **scipy.optimize**<br>
   함수 최적화기와 방정식의 근을 구하는 알고리즘

 - **scipy.signal**<br>
   시그널 프로세싱 도구

- **scipy.sparse**<br>
  희소 행렬과 희소 선형 시스템 풀이법

- **scipy.special**<br>
  감마 함수처럼 흔히 사용되는 수학 함수를 구현한 포트란 라이브러리인 SPECFUN 래퍼

- **scipy.stats**<br>
  표준 연속/이산 확률 분포(밀도 함수, 샘플러, 연속 분포 함수)와 다양한 통계 테스트 그리고 좀 더 기술적인 통계도구

설치 명령어는 cmd에서 `pip install scipy`를 입력한다.

참고 사이트: <a href='http://scipy-lectures.org/' target='blank'> http://scipy-lectures.org/</a>

### [scikit-learn](https://scikit-learn.org/stable/documentation)

scikit-learn(사이킷런)은 머신러닝 학습을 위한 파이썬 라이브러리이다. 다음과 같은 모델의 하위모듈을 포함한다.

- **classification**: SVM(Support Vector Machine), KNN(K-Nearest Neighbor), Random Forest, Logistic Regression, etc.
- **regression**: Ridge, Lasso, Elastic-Net, etc.
- **clustering**: K-Mean, Spectral Clustering, etc.
- **dimensionality reduction**: PCA(Principal Component Analysis), Feature Selection, LDA(Linear Discriminant Analysis), etc.
- **model selection**: GridSearch, Cross Validation, Matrix, etc.
- **preprocessing**: Feature Extraction, Normalization, etc.

설치 명령어는 cmd에서 `pip install -U scikit-learn`을 입력한다.

참고 사이트: <a href='https://scikit-learn.org/stable/user_guide.html' target='blank'>사용자 가이드</a>, <a href='https://scikit-learn.org/stable/modules/classes.html' target='blank'>API 문서</a>

### statsmodels

statsmodels은 다양한 R 언어용 회귀분석 모델을 구현한 스탠퍼드 대학의 통계학 교수인 조나단 테일러<sup>Jonathan Taylor</sup>의 작업을 기반으로 만들어진 통계분석 패키지다. scikit-learn과 비교하여 statsmodels는 전통적인 통계(주로 빈도주의적 접근)와 계량경제학 알고리즘을 포함하고 있다. 다음과 같은 하위모듈을 포함한다.

- **회귀 모델**: 선형회귀, 일반화 선형 모델, 로버스트 선형 모델, 선형 혼합효과 모델 등
- **분산분석**(ANOVA: analysis of variance)
- **시계열분석**: AR, ARMA, ARIMA, VAR 및 기타 모델
- **비모수 기법**: 커널밀도추정, 커널회귀
- **통계 모델 결과의 시각화**

설치 명령어는 cmd에서 `pip install statsmodels`를 입력한다.

### 정리

---

1. 파이썬 언어를 이용해 머신러닝 애플리케이션을 작성하기 위해서는 **머신러닝, 행렬/선형대수/통계 패키지**와 **데이터 핸들링, 시각화**에 친숙해져야 한다.

2. 파이썬 기반의 머신러닝 개발을 위해서는 넘파이와 판다스를 이해하는 것이 매우 중요하다. 사이킷런이 넘파이 기반에서 작성됐기 때문에 넘파이의 기본 프레임워크를 이해하지 못하면 사이킷런 역시 실제 구현에서 많은 벽에 부딪힐 수 있다.

3. 사이킷런은 API 구성이 매우 간결하고 직관적이어서 이를 이용한 개발 또한 쉽다. 오히려 넘파이와 판다스가 가지는 API가 더 방대하기 때문에 이를 익히는 데 시간이 많이 소모될 수 있다.

4. 따라서, 넘파이와 판다스에 대한 기본 프레임워크와 중요 API만 습득하고, 일단 코드와 부딪쳐 가면서 모르는 API는 인터넷 자료를 체득하는 것이 머신러닝뿐만 아니라 넘파이와 판다스에 관한 이해를 넓히는 더 빠른 방법이다.

[^0]: 엔터프라이즈 아키텍처(Enterprise Architecture; EA)는 조직의 프로세스 및 정보 시스템 및 부서의 구조와 기능을 포괄적이고 정확한 방법으로 기술하는 방법이고, 이것을 통해 조직이 전략적 목표에 따라 행동하도록 방향을 제시하는 것이다. 정보기술(IT)와 관련이 깊지만, 사업 최적화도 관련이 깊고, 사업구조, 성과관리, 조직구조 아키텍처 등으로 불린다.
[^1]: 벡터, 행렬, 선형 변환을 연구하는 수학의 한 분야
[^2]: 시간이 함수인 신호 등을 주파수 성분으로 분해하는 변환
[^3]: 초깃값을 이용하여 이미 결정되어 있는 메커니즘에 의해 생성되는 난수로, 초깃값을 알면 언제든 같은 값을 다시 만들 수 있으므로 진짜 난수와 구별하여 유사 난수라고 합니다.