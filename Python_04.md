## Module

- 함수나 변수 또는 클래스를 모아 놓은 파일
- 모듈은 다른 파이썬 프로그램에서 불러와 사용할 수 있게 만든 파이썬 파일

```python
# fah_converter.py == 모듈1
def convert_to_f(celsius_value):
    return celsius_value * 90 / 5 +32


# 모듈 테스트 할때는 따로 작성해서 해줘야함
if __name__ == '__main__':
    print("모듈 테스트")
    print(convert_to_f(45))  
else:
    print("임포트문 실행")
```

```python
# chap04.py == 모듈2
from fah_converter import convert_to_f #1  모듈1을 불러씀
print(convert_to_f(34))



import fah_converter as fh #2 #1의 다른방법
print(fh.convert_to_f(34))
```

```shell
# fah_converter.py에서 실행 결과
모듈 테스트
842.0
```

```shell
임포트문 실행
644.0
```

#### random

```python
import random

print(random.randint(0, 100)) # 0~100 사이의 정수 난수 발생

import time
print(time.localtime())
```

```python
37 #random
time.struct_time(tm_year=2020, tm_mon=7, tm_mday=14, tm_hour=9, tm_min=51, tm_sec=52, tm_wday=1, tm_yday=196, tm_isdst=0)
```

### Package

예제1 ) 인터넷에서 주식 정보를 가져와 데이터베이스에 저장, 필요한 정보를 계산



1. 디렉토리 구성

- 패키지 명: roboadvisor



- roboadvisor의 기능
  - crawling: 주식 관련 데이터를 인터넷에서 가져옴
  - database: 가져온 데이터를 데이터베이스에 저장
  - analysis: 해당 정보를 분석, 의미있는 가치 추출



hjchoe_pacakage ---- roboadvisor ---- analysis

​															---- crawling

​															---- database

2. 디렉토리별 모듈 작성

- 각 디렉토리가 패키지 임을 표시하기 위해 __ init __.py  파일이 필요
  버전 3.3 이하 반드시필요, 3.6이상부터는 불필요



3. 디렉토리 __ init __.py 파일 작성

- 해당 디렉토리가 파이썬 패키지라고 선언하는 초기화 스크립트
- 패키지 개발자, 설치시 유의사항 등의 메타 데이터를 포함
- 패키지 구조를 기술



## Chap 9. 예외처리

### try, except  as, else, finally

#### try, except, else

```python
for i in range(10):
    try:
        print(10 / i)
    except ZeroDivisionError as e:
        print(e)
        print("Not divided by 0")
    else:
        print(10 / i)
```

```python
5.0
5.0
3.3333333333333335
3.3333333333333335
2.5
2.5
2.0
2.0
1.6666666666666667
1.6666666666666667
1.4285714285714286
1.4285714285714286
1.25
1.25
1.1111111111111112
1.1111111111111112
```

#### finally

```python
for i in range(10):
    try:
        print(10 / i)
    except ZeroDivisionError as e:
        print(e)
        print("Not divided by 0")
    finally:
        print("프로그램 종료")
```

```python
division by zero
Not divided by 0
프로그램 종료
10.0
프로그램 종료
5.0
프로그램 종료
3.3333333333333335
프로그램 종료
2.5
프로그램 종료
2.0
프로그램 종료
3.3333333333333335
프로그램 종료
2.5
프로그램 종료
2.0
프로그램 종료
1.6666666666666667
프로그램 종료
1.4285714285714286
프로그램 종료
1.25
프로그램 종료
1.1111111111111112
프로그램 종료

```

#### raise

```python
while True:
    value = input("변환할 정수값을 입력해 주세요: ")
    for digit in value:
        if digit not in "0123456789":
            raise ValueError("숫자를 입력하지 않았습니다.")
    print("정수값으로 변환된 숫자: ", input(value))
```





```python
def add(a: int, b: int) -> int:
    return a + b

print(add(10, 5))
print(add([1, 2], [3]))
print(add("hi ", "there"))
```

```python
15
[1, 2, 3]
hi there
```





```python
from typing import List

Vector = List[float]

def add(v: Vector, w: Vector) -> Vector:
    assert len(v) == len(w)
    return [v_i + w_i for v_i, w_i in zip(v, w)]

print(add([1, 2, 3], [4, 5, 6]))

def sum_of_squares(v: Vector) -> float:
    #Returns v_i * v_i + ... v_n * v_n
    return dot(v, v)

print(add([1, 2, 3], [4, 5, 6]))
```

```python
[5, 7, 9]
[5, 7, 9]
```





### convert

```python
ARABIC_TO_ROMAN = [
    (1000, "M"), (900, "CM"), (500, "D"), (400, "CD"),
    (100, "C"), (90, "XC"), (50, "L"), (40, "XL"), (10, "X"),
    (9, "IX"), (5, "V"), (4, "IV"), (1, "I")
]

def convert_to_roman_numeral(number: int) -> str:
    result = list()
        #1000, M
    for arabic, roman in ARABIC_TO_ROMAN:
        # 1, 230             
        count, number = divmod(number, arabic)
                      # M * 1
        result.append(roman * count)
    #배열에 있는 문자열들을 모두 합쳐줘라의 join    
    return "".join(result)

print(convert_to_roman_numeral(1230))


# for 내가정하는 변수(a, b, c) in 변수타입 (배열)

```

```python
MCCXXX
```





#### Practice 1)

- 자연수 N을 입력받아 대해 N이 짝수이면 N!을, 홀수이면 시그마N을 구하는 코드를 작성하시오

```python
N =int(input())

if N % 2 == 0:
    result = 1
    for i in range(1, N+1):
        result *= 1 

else:
    result = 0
    for i in range(1, N+1):
        result += i
print(result)
```



#### Practice 2)

- 야구게임

```python
goal = "386"
input_data = input("input number: ")
strike = 0
ball = 0
for number in goal:
    if input_data.count(number) > 0:
        if input_data.find(number) == goal.find(number):
            strike += 1
        else:
            ball += 1

print("Strike:", strike, "Ball:", ball)
```

```python
Strike: 1 Ball: 0
```

