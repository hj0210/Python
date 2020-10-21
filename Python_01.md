# Python_01

## Chap 1. Python 시작

### 1. 객체 생성

- 대소문자를 구별함
- 반드시 들여쓰기
- 변수명 결정
  - 모두 소문자로 쓴다.
    - ex) Java = numberOfCylinder ----- X
    - ex) python = number_of_cylinder ----- O

```python
 book = "The hunt for red October"
 a = 7 # 정수형
 b = 5
    
 a = 1.7 # 실수형

 bool_type = True # boolean type 은  T,F 항상 대묹
    
 # 문자열에서 '(apostrophe) 를 사용할거면 "" 로 묶어줘야 함
 book = 'my name is Tom'
 book = "She's ....."
 book = 'he said "Hi!!"'
 book = """ 여러줄을 넣고싶을 때"""
```

- True

```python
True == 1  ... True
True == 0  ... False
```

- 사칙연산
  - (A%B) = (A+B)%B

```python
print (2 ** 3) ... 8 #2의 3승
print (7 // 2) ... 3# 몫만 나오고 싶을 때
print (7 % 2) ... 1# 나머지
print ( -1 % 5 ) ... 4 #모듈라 연산자 (A%B) = (A+B)%B
print ( 1 % -5 ) ... -4
```

```python
a = 1
a = a + 1
print (a) = 2
a += 1
print (a) = 3

a = 10
b = float(a)
print (a, b) ... 10 10.0
c = int(b)
print (c) ... 10

a = "76.3"
b = float(a)
print (a, b) ... 76.3 76.3
```

#### 1-1) str

```python
a = 10.5
b = 21.8
c = str(a)
d = str(b)
print (a+b, c+d)
32.3 10.521.8 # 문자는 붙여서 나옴
```

#### 1-2) type

```python
a = 10.3
type(a)
<class 'float'>
b = "23"
type(b)
<class 'str'>
```

#### 1-3) lang

- 문자열 인덱싱

```python
lang = 'python'
print(lang[0], lang[2])
```

```python
p t
```





### 2. IDE

- Intefrated Development Environment
  - pycharm
    - community version 다운



## Chap 2. 

### 1. print

````python
print("Enter name : ")

name = input() # 사용자가 입력을 해야함

print("Good morning!", name) # ,를 쓰면 알아서 띄어쓰기 해줌
````

#### #주석표시 

- 드래그 주석표시는 java ( ctrl+ / )와 같음
- ''#'' : 1줄만 주석
  - 파이참에서는 작성한줄에 적어도 두칸은 띄워줘야함
- """ :  여러줄

```python
colors = ['red', 'blue', 'green'] #리스트 객체 생성
print(colors[0])
print(colors[2])
print(len(colors))
print(colors)
```

```python
red
green
3
['red', 'blue', 'green']
```

### 2. list

#### 2-1) mix_list

- 모두 작성하고 맨마지막에 엔터를 한번 넣어야 맨마지막에 밑줄이 안나옴

```python
mix_list = [1, 2, 'Three', 3.14, True] #타입을 구별하지 않고 다 받을수 ㅣㅆ음
print(mix_list)
```

#### 2-2) cities

```python
cities = ['서울', '부산', '인천', '대구', '대전', '광주', '울산', '수원']
print(cities[0:6])
print(cities[:6])
print(cities[2:])

print(cities[-7:])
print(cities[:-2])

print(cities[:])
print(cities)

print(cities[1:7:2]) #1부터 7까지 1,1+2, 1+4
print(cities[::-1])
print(cities[::2])
```

```python
['서울', '부산', '인천', '대구', '대전', '광주']
['서울', '부산', '인천', '대구', '대전', '광주']
['인천', '대구', '대전', '광주', '울산', '수원']

['부산', '인천', '대구', '대전', '광주', '울산', '수원']
['서울', '부산', '인천', '대구', '대전', '광주']

['서울', '부산', '인천', '대구', '대전', '광주', '울산', '수원']
['서울', '부산', '인천', '대구', '대전', '광주', '울산', '수원']

['부산', '대구', '광주']
['수원', '울산', '광주', '대전', '대구', '인천', '부산', '서울']
['서울', '인천', '대전', '울산']
```

#### 2-3) packing, unpacking

- 입력 1)

```python
colors = ['red', 'blue', 'green'] # packing
a, b, c = colors # unpacking
print(a, b, c)
```

```python
red blue green
```

- 입력 2)

```python
colors = ['red', 'blue', 'green'] # packing
a, _, c = colors # unpacking
print(a, c)
```

#### 2-4) list in list

- 입력 1)

```python
kor_score = [60, 65, 85, 100, 90]
eng_score = [70, 80, 90, 85, 100]
math_score = [100, 90, 70, 90, 85]
term_score = [kor_score, eng_score, math_score]
print(term_score)
print(term_score[0]) # [row]
print(term_score[0][2]) # [row][column]
```

```python
[[60, 65, 85, 100, 90], [70, 80, 90, 85, 100], [100, 90, 70, 90, 85]]
[60, 65, 85, 100, 90]
85
```

- 입력 2)
  - 중첩 리스트

```python
a = ['color', 1, 0.2]
color = ['yellow', 'blue', 'red']
a[0] = color #중첩 리스트
print(a)
```

```python
[['yellow', 'blue', 'red'], 1, 0.2]
```

#### 2-5) backup

```python
kor_score = [60, 65, 85, 100, 90]
eng_score = [70, 80, 90, 85, 100]
math_score = [100, 90, 70, 90, 85]
math_backup_score = math_score
term_score = [kor_score, eng_score, math_score]
print(term_score)
math_score[0] = 0 # 0번째 배열항목을 0으로 변경
print(math_score)
print(term_score)
print(math_backup_score)
```

```python
[[60, 65, 85, 100, 90], [70, 80, 90, 85, 100], [100, 90, 70, 90, 85]]
[0, 90, 70, 90, 85]
[[60, 65, 85, 100, 90], [70, 80, 90, 85, 100], [0, 90, 70, 90, 85]]
[0, 90, 70, 90, 85]
```

#### 2-6) reverse

- 배열을 리버스

````python
a = [1, 10, 5, 7, 6]
a.reverse()
print(a)
````

```python
[6, 7, 5, 10, 1]
```

#### 2-7) sort

- 원본을 아예 바꿔 줄 경우
- 정렬 : default 는 오름차순

- 입력 1)
  - 오름차순

````python
a = [1, 10, 5, 7, 6]
a.sort()
print(a)
````

````python
[1, 5, 6, 7, 10]
````

- 입력 2)
  - 내림차순

```python
a = [1, 10, 5, 7, 6]
a.sort(reverse=True)
print(a)
```

```python
[10, 7, 6, 5, 1]
```

##### sorted

- 원본을 보존해야 할 경우

```python
a = [3, 2, 1, 4]
b = sorted(a)  # sort 결과 return.... sorted(a, reverse=True)
print(a, b)
```

```python
[3, 2, 1, 4] [1, 2, 3, 4]
```

#### 2-8) count

```python
a = [5, 10, 5, 7, 6]
print(a.count(5)) # 5가 몇개 있는가?
```

```python
2
```

##### ### 시험

- main_dish[1::3] = 1번째 포함 +3 

```python
appetizer = ['egg', 'salad', 'bread', 'soup', 'canape']
main_dish = ['fish', 'lamb', 'pork', 'beef', 'chicken']
dessert = ['apple', 'ice cream', 'pudding', 'cookies', 'cake']

order = [appetizer, main_dish, dessert]
jane = [order[0][:-2], main_dish[1::3], dessert[1]]
# [['egg', 'salad', 'bread'], ['lamb', 'chicken'], 'ice cream']
del jane[2] # ['ice cream']
jane.extend([order[2][0:1]]) # ['apple']
print(jane)
```

```python
[['egg', 'salad', 'bread'], ['lamb', 'chicken'], ['apple']]
```

### 3. color

- 입력 1)

```python
color1 = ['red', 'blue', 'green']
color2 = ['orange', 'black', 'white']
add_color = color1 + color2
print(len(add_color))
print(add_color)
```

```python
6
['red', 'blue', 'green', 'orange', 'black', 'white']
```

- 입력 2)

```python
color1 = ['red', 'blue', 'green']
color2 = ['orange', 'black', 'white']
mul_color = color1 * 2
print(len(mul_color))
print(mul_color)

```

```python
6
['red', 'blue', 'green', 'red', 'blue', 'green']
```

- 입력 3)
  - 대체

```python
colors = ['red', 'blue', 'green']
colors[2] = 'white'
print(colors)
```

#### 3-1) in

- 이 안에 있냐 확인

```python
color1 = ['red', 'blue', 'green']
color2 = ['orange', 'black', 'white']
print('blue' in color2)
```

```py
False
```

#### 3-2) append

- 기존 리스트에서 항목만 추가
- 3개 만들어서 1개 추가할빠에는 아예 4개로 만들어라

```python
colors = ['red', 'blue', 'green']
colors.append('white')
print(colors)
```

```python
['red', 'blue', 'green', 'white']
```

#### 3-3) extend

- 배열끼리 합칠때

```python
colors = ['red', 'blue', 'green']
colors.extend(['black', 'purple'])
print(colors)
```

```python
['red', 'blue', 'green', 'black', 'purple']
```

#### 3-4) insert

- 특정위치에 삽입

```python
colors = ['red', 'blue', 'green']
colors.insert(1, 'black')
colors.insert(2, 'purple')
print(colors)
```

```python
['red', 'black', 'purple', 'blue', 'green']
```

#### 3-5) remove

- 특정 항목 삭제

##### del

- 해당 인덱스에 있는 항목 삭제

```python
colors = ['red', 'blue', 'green']
colors.remove('blue')
print(colors)

colors = ['red', 'blue', 'green']
del colors[0]
print(colors)
```

```python
['red', 'green']

['blue', 'green']
```

### 4. if

#### 4-1) if, else

- 콜론(:) 을 쓰면 자동적으로 바꿔줌
- tab = space 4칸 이므로 메모장에 쓸경우 space 네번
- 입력 1)

````python
print('Tell me your age?')
my_age=int(input())
````

```python
Tell me your age?
```

- 입력 2)

  - input() 이므로 내가 콘솔창에 직접 입력해야함

  - defalut 값이 new line 이므로 end='' 입력해주면 붙여서 입력이 가능하게 해줌

    ```python
    print('Tell me your age? ', end='')
    blahblahblah ()
    ```

    ```python
    Tell me your age? 22
    Welcome to the Club.
    ```

```python
print('Tell me your age?')
my_age=int(input())
if my_age < 30:
    print("Welcome to the Club.")
else:
    print("Oh! No. You are not accepted.")
```

```python
# 22 입력
Tell me your age?
22
Welcome to the Club.
```

- 입력 3)
  - oneline if

```python
a = 10
b = a * 10 if a % 2 == 0 else a + 10
print(b)
```

```python
100 # 나머지가 0이면 a 곱 10, 0이아니면 a 합 10 
```



##### elif

```python
score = int(input("Enter your score: "))

if score >= 90:
    grade = 'A'
elif score >= 80:
    grade = 'B'
elif score >= 70:
    grade = 'C'
elif score >= 60:
    grade = 'D'
else:
    grade = 'F'

print(grade)
```

``` python
Enter your score : 100 #input 값 
A   # input 값에 대한 점수
```



#### 4-2) None

- None is for non-exist value

- x = None

  - ```python
    assert x == None, # "this is the not the Pythonic way to check for None"
    ```

  - ```python
    assert x is None, # "this is the Pythonic way to check for None"
    ```

- 파이썬이나 사용하는 False

  ```python
  False, None, [], {}, "", set(), 0, 0.0
  ```

### 5. repeat

#### 5-1) for

- java에서 enhanced for loop 

```python
for n in [1, 2, 3, 4, 5]:
    print('No.', n)
```

```python
No. 1
No. 2
No. 3
No. 4
No. 5
```

##### open

- 파일 객체 = open(파일 이름, 파일 열기 모드)

![image-20200724130956450](C:\Users\bitr48\AppData\Roaming\Typora\typora-user-images\image-20200724130956450.png)

```python
f = open("구구단.txt", 'w') #f = open("새파일.txt", 'w') 데이터 쓰기
for num in range(1,10):
    format_string = "2 x {0} = {1}\n".format(num, 2*num)
    f.write(format_string)
f.close() #f.close()

----------------------------------------------------------------------
f= open("구구단.txt") ##################첫번째방법
line = f.readline()
while line:
    print(line, end='')
    line = f.readline()
f.close()

f = open("구구단.txt") #################두번째방법
for line in f:
    print(line, end='')
f.close()
```



##### range

- 입력 1)

```python
for n in range(5): 
    print('No.', n)
```

```python
No. 0
No. 1
No. 2
No. 3
No. 4
```

- 입력 2)

```python
for n in range(1, 6, 2):
    print('No.', n)
```

```python
No. 1
No. 3
No. 5
```

cf)

```python
for n in 'abcdefg':
    print('Char.', n)
```

```python
Char. a
Char. b
Char. c
Char. d
Char. e
Char. f
Char. g
```

#### 5-2 ) multiple for

##### double for

````python
for n in ['banana', 'pineapple', 'mango']:
    for k in n:
        print(k)
    print()
````

```python
b
a
n
a
n
a
	#print()
p
i
n
e
a
p
p
l
e
	#print()
m
a
n
g
o
	#print()
```



### 6. condition

#### 6-1) while

```python
i = 1
while i < 10:
    print(i)
    i += 1
```

```python
1
2
....
8
9
```

#### 6-2) break

- 가장 가까운 반복문을 찾아 탈출

```python
for i in range(10):
    if i == 5:
        break
    print(i)
print("End of program")
```

```python
0
1
2
3
4
End of program
```

#### 6-3) continue

```python
for i in range(10):
    if i == 5:
        continue
    print(i)
print("End of program")
```

```python
0
1
...
8
9
End of program
```



## Chap 3.  Practice_01

**정답은 항상여러가지다!!** 

### Practice 1-1) 

- ```python
  몇단?
  3
  구구단 3단 계산
  3 X 1 = 3
  3 X 2 = 33
  3 X 3 = 333
  3 X 4 = 3333
  3 X 5 = 33333
  3 X 6 = 333333
  3 X 7 = 3333333
  3 X 8 = 33333333
  3 X 9 = 333333333
  ```

- 정답 1)

```python
print("몇단?")
dan = input()
print("구구단", dan, "단 계산")
int_dan = int(dan)
for i in range(1, 10):
    result = int_dan * i
    print(dan, 'X', i, '=', result)
```

### Practice 1-2)

- ```python
  sentence = 'I love you' 의 출력이
  'uoy evol I' 로 나올 수 있게 하시오
  ```

- 정답 2)

```python
sentence = 'I love you'
reverse_sentence = '' #빈 문자열 ''
for char in sentence:
    reverse_sentence = char + reverse_sentence
print(reverse_sentence)
```

### Practice 1-3)

- ```python
  decimal = 14 # 2진수로 출력
  ```

- 정답 3)

```python
decimal = 14
result = ''
while decimal > 0:
    remainder = decimal % 2
    decimal = decimal // 2
    result = str(remainder) + result
print(result)
```

### Parctice 1-4)

- 다음 점수를 가지고 평균점수를 구하라.
  (double for)

  ```python
  kor_score = [49, 80, 20, 100, 80]
  math_score = [43, 60, 85, 30, 90]
  eng_score = [49, 82, 48, 50, 100]
  term_score = [kor_score, math_score, eng_score]
  ```

- 정답 4-1)

  ```python
  kor_score = [49, 80, 20, 100, 80]
  math_score = [43, 60, 85, 30, 90]
  eng_score = [49, 82, 48, 50, 100]
  term_score = [kor_score, math_score, eng_score]
  length = len(kor_score)
  for i in range(length):
      avg = (kor_score[i] + math_score[i] + eng_score[i]) / 3
      print(avg, end=" ")
  ```

- 정답 4-2)

  ```python
  kor_score = [49, 80, 20, 100, 80]
  math_score = [43, 60, 85, 30, 90]
  eng_score = [49, 82, 48, 50, 100]
  term_score = [kor_score, math_score, eng_score]
  
  student_score = [0, 0, 0, 0, 0]
  i = 0
  for subject in term_score:
      for score in subject:
          student_score[i] += score
          i += 1
      i = 0
  
  n_s = len(term_score)
  a, b, c, d, e = student_score
  student_average = [a / n_s, b / n_s, c / n_s, d / n_s, e / n_s]
  print(student_average)
  ```

- 정답 4-3)

  ```python
  kor_score = [49, 80, 20, 100, 80]
  math_score = [43, 60, 85, 30, 90]
  eng_score = [49, 82, 48, 50, 100]
  term_score = [kor_score, math_score, eng_score]
  for i in range(len(kor_score)):
      sum_score = 0
      for j in range(len(term_score)):
          sum_score += (term_score[j][i])
      print(sum_score / len(term_score))
  ```
  
- 정답 4-4)

```python
kor_score = [49, 80, 20, 100, 80]
math_score = [43, 60, 85, 30, 90]
eng_score = [49, 82, 48, 50, 100]
term_score = [kor_score, math_score, eng_score]

student_result = [0, 0, 0, 0, 0]

for i in range(len(kor_score)):  # [0, 1, 2, 3, 4]
    sum_score = 0
    for j in range(len(term_score)):
        sum_score += (term_score[j][i])
    student_result[i] = sum_score / len(term_score)
print(student_result)

```

