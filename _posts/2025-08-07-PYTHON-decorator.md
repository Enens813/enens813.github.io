---
layout: post
title: Python Decorator 사용법
date: 2025-08-07 19:31 +0900
categories: [Programming Language, Python]
tags: [programming, language, python, decorator]
description: Python의 decorator 문법 설명
---

# What is decorator?
- 함수나 클래스의 기능을 수정, 확장할 수 있는 방법. 이걸 꾸며준다고 표현
- 함수나 클래스위에 @함수명 처럼 작성하여 사용


# How it works?
- 기본 개념:
  1. decorator가 될 함수A는 다른 함수를 argument로 전달받아, 다른 함수를 반환하는 구조.
  2. @함수A 가 위에 붙은 채로 선언된 다른 함수B는, 함수A(함수B)가 실행되고, 그 결과를 함수 B에 저장
- 이해하려 하기보단 직접 보는게 빠르다

FYI) 함수를 말할 때,
  - Parameter(매개변수): 함수 정의 시 사용하는 변수 이름
  - Argument(인자): 함수를 호출할 때 전달하는 실제 값


## 기본적인 Decorator 사용법
- 왼쪽과 오른쪽은 동일한 코드이다
<p align="center">
  <img src="assets/img/postimgs/deco_basic1.png" alt="기본 데코레이터 사용 예제" width="45%" />
  <img src="assets/img/postimgs/deco_basic2.png" alt="데코레이터와 동일한 코드 예제" width="45%" />
</p>

- 아예 함수를 바꾸어 새로운 함수로 전달하는 것도 가능하다
![assets/img/postimgs/deco_basic3.png]

- 함수가 아닌 다른 걸 전달해도 된다
![assets/img/postimgs/deco_basic4.png]

- decorator가 그냥 함수가 아니라 class method 여도 된다. 이 땐 class 인스턴스를 만들어서(init), 그걸 call한 결과가 나온다. 그리고, class를 선언할 때 인자를 넣어도 된다.
![assets/img/postimgs/deco_basic5.png]

- class를 이용한 decorator로 좀 더 복잡하게 사용하면, 아래처럼도 가능하다.
![assets/img/postimgs/deco_basic6.png]

FYI) *args는 모든 위치 인자를, **kwargs는 모든 키워드 인자를 받음. 무엇이든 일단 받겠다는 것이다. 겁먹지 말자

## Common use cases
- 위의 문법만 봐선 어디다 쓰는 지 모를 수 있다.
- 다음은 함수 실행시간 측정을 하는 방법이다.
![assets/img/postimgs/deco_basic7.png]
- 이 함수를 이용하면 원하는 함수의 실행시간을 측정하는 걸 쉽게 할 수 있다.
- 즉, 함수를 객체화해서 반복 사용한다고 이해해도 된다.





## 기 정의된 decorator들 예시
1. @staticmethod
  - class의 method가 아니라 일반 함수처럼 정의 (첫 번째 변수로 자신(인스턴스)를 받지 않겠다)
  - 인스턴스 선언 없이 값을 확인할 때 유용
![assets/img/postimgs/deco_use1.png]

2. @classmethod
  - 첫 번째 변수로 자신(인스턴스)가 아닌 자신 클래스를 받음. 그 변수명으로 주로 self 대신 cls를 씀.
  - 종종 생성자 대신 사용됨
![assets/img/postimgs/deco_use2.png]

3. @property
  - 함수를 변수처럼 사용. 괄호 ()없이 값 확인 가능.
  - OOP의 getter역할. 
  - ()없이 할당하는 setter, del로 지울수 있게 하는 deleter와 함께 사용 가능
![assets/img/postimgs/deco_use3.png]
![assets/img/postimgs/deco_use4.png]

4. @contextmanager
  - with ~ 문에서 전처리, 후처리할 때 사용
  - context manager가 꾸미는 함수는 result가 아닌 yield와 함께 쓰이는데, yield 앞에는 with내부코드 실행 전 처리, 뒤에는 with내부코드 실행 후 처리를 함.
  - 주로 오류가 나도 열려있는 파일을 닫기 위해서 try~finally를 추가로 사용
![assets/img/postimgs/deco_use5.png]
![assets/img/postimgs/deco_use6.png]

5. @wraps
  - 위의 방식대로 decorator에서 새 함수를 정의해서 return 하면, 함수 내부 이름 등의 메타데이터가 변경됨.
  - @wraps를 쓰면 데코레이터 내부에서 원래 함수의 메타데이터(이름, docstring 등)를 유지.
![assets/img/postimgs/deco_use7.png]
![assets/img/postimgs/deco_use7result.png]

6. @lru_cache
  - 메모이제이션을 해주는 코드
  - max_size 인자를 받아서 최대 몇 개 까지 기억할 지 지정 가능.
  - 아래의 두 코드는 같은 역할을 한다.
![assets/img/postimgs/deco_use8.png]
![assets/img/postimgs/deco_use9.png]


##### 첨부파일
위 예제를 작성할 때 사용된 코드 파일(ipynb)는 다음 링크에서 다운 받을 수 있습니다.
[Download Notebook](https://github.com/Enens813/anything/blob/main/blog-files/decorator_practice.ipynb)


# Reference
- https://wikidocs.net/160127
- https://wikidocs.net/184210
- https://youtu.be/3t26Z4vk7XE?si=2v5FMRlIFWWKikvJ
- https://youtu.be/7dMDSXx7TwE?si=l30epUcPW6HFpj5Q
- https://youtu.be/gfAImdVcgn4?si=In-yvgdS_JjJYjgN
- https://youtu.be/-zoRYdsfzco?si=99Q1Ad4vk7c0jVSk
- https://youtu.be/txDg45IsC9A?si=4NOVXV5tn-1pZUl7
- https://youtu.be/KciDHojdxcE?si=KTkwMv6D7hF3cag8
