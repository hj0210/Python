# Python_02

## Chap4. Function

### 1. def

- def

  - 함수 정의

  ```python
  def 함수 이름 (인자1, 인자2, ...옵션)
  
  		실행문 1
  
  		실행문2
  
  		return 반환값 (옵션)
  ```

- 입력 1)

  ```python
  def calculate_rectangle_area(x, y):
      return x * y
  
  rectangle_x = 10
  rectangle_y = 20
  print("사각형 x의 길이:", rectangle_x)
  print("사각형 y의 길이:", rectangle_y)
  print("사각형의 넓이:", calculate_rectangle_area(rectangle_x, rectangle_y))
  ```

#### 1-1) assert

- 함수만들 때 습관적으로 사용해보자

- print 해서 체크하는 것보다 내가 만든 함수가 잘 작동이 되는것을 확인할 때 사용

  - 입력1)
    에러나면 아래의 출력처럼 나옴 그래서 뒤에 써보면 어디서 에러나는지 빠르게 알수 있음

  ```python
  def calculate_rectangle_area(x, y):
      return x * y
  #
  # 함수 선언이 끝나고 2칸을 띄워줘야 pythonic 하다!
  assert calculate_rectangle_area(2, 3) == 7, '이거나오면 에러~'
  ```

  ```python
      assert calculate_rectangle_area(2, 3) == 7, '이거나오면 에러~'
  AssertionError: 이거나오면 에러~
  ```

#### 1-2) variable scope

- **파이썬**에서는 **변수**가 선언된 위치에 따라 해당 **변수**가 영향을 미치는 **범위**까지 달라지며, 이것을 **변수의** 유효 **범위**(variable **scope**)라고 부릅니다. 예를 들어, 함수 내부에서 선언된 **변수**는 해당 함수 내부에서만 사용할 수 있으며, 함수 밖에서는 사용할 수 없습니다.
- 입력 1)

```python
# 지역 local nameSpace에 담겨져있는 goods, 함수가 끝나면 사라짐.
def shopping_cart(goods):
    goods.append('coupon')
    goods = [1, 2] #새로운객체를 reference함
    print("In shopping_cart:", goods)

#global nameSpace에 담겨져 있는 shopping_list
shopping_list = ['bean', 'salt', 'beef']
shopping_cart(shopping_list)
print("Goods I bought:", shopping_list)
```

```python
In shopping_cart: [1, 2]
Goods I bought: ['bean', 'salt', 'beef', 'coupon']
```

- 입력 2)

```python
def test(x):
    print(x)
    t = 20
    a = 300
    print("In test t, a:", t, a)
    

a = 10 
test(a)
print("In main x:", a)
```



```python
10
In test t, a: 20 300
In main x: 10
```

- 입력 3)

```python
def f():
    # 함수에서는 자신만의 stack을 가지고 있음
    # local namespace
    global s
    s = "I love Doosan!" 
    print(s)

# global namespace
s = "I love Hanhwa!"
f()
print(s)
```

```python
I love Doosan!
I love Hanhwa!
```

- 입력 4)

```python
#local
def calculate(x, y):
    total = x + y
    print("In Function")
    print("a:", str(a), "b:", str(b), "a + b:", str(a + b), "total:", str(total))
    return total

#global
a = 5
b = 7
total = 0
print("In main")
print("a:", str(a), "b:", str(b), "a + b:", str(a + b))

sum = calculate(a, b)
print("After Calculation")
print("Total:", str(total), "Sum:", str(sum))
```

```python
In main
a: 5 b: 7 a + b: 12
In Function
a: 5 b: 7 a + b: 12 total: 12
After Calculation
Total: 0 Sum: 12
```

##### format

- 파이썬의 string 클래스는 format이라는 method를 가지고있다
- 입력 5)

```python
def print_name(my_name, your_name):
    print("Hello {0}, My name is {1}".format(your_name, my_name))
    

print_name("Tom", "Jane")
print_name(your_name="Jane", my_name="Tom")
```

```python
def print_name(my_name, your_name="Jane"):
    print("Hello {0}, My name is {1}".format(your_name, my_name))


print_name("Tom", "Jane")
print_name("Tom")
```

```python
Hello Jane, My name is Tom
Hello Jane, My name is Tom
```

##### 가변인자 *

- 입력 1)

```python
def variable_length(a, b, *args): #가변인자 *  #args는 변수이름, 바껴도됨
    print(a)
    print(b)
    print(args)


(variable_length(1, 2, 3, 4, 5))
```

```python
1
2
(3, 4, 5)
```

### 2. literal function

- 기초 문자열 함수

```python
s = "BLACK LIVES MATTER"
print(s.upper())
print(s.lower())
print(s.title())
print(s.capitalize())
print(s.count("T"))
print(s.startswith("B"))

k = "123"
print(k.isdigit())
```

```python
BLACK LIVES MATTER
black lives matter
Black Lives Matter
Black lives matter
2
True
True
```

#### 2-1) format String

- 여러가지 표현

```python
print(1, 2, 3)
print("%d %d %d" %(1, 2, 3))
print("%s--%s--%s" % ('abc', 'def', 'ghi'))
print("{} {} {}".format('abc', 'def', 'ghi'))
print("{1} {0} {2}".format('abc', 'def', 'ghi'))
print(f"{'def'} {'abc'} {'ghi'}")
print("{0:>10s}".format('python')) # 전체 10칸을 잡고 우측정렬 
print("{0:<10s}".format('python')) # 전체 10칸을 잡고 좌측정렬
print(f"{'python':>10s}") # 위와 같음
print(f"{'python':<10s}")
```

```python
1 2 3
1 2 3
abc--def--ghi
abc def ghi
def abc ghi
def abc ghi
    python
python    
    python
python    
```

#### 2-2) split

- 단어 하나하나 잘라버리는 메소드
  - 결과는 list로 나온다.

```python
items = 'zero one two three'. split()
print(items)

examples = 'python,javascript,sql'
print(examples.split(','))
a, b, c = examples.split(',')
print(a, b, c)
```

```python
['zero', 'one', 'two', 'three']
['python', 'javascript', 'sql']
python javascript sql
```

#### 2-3) join

- 단어를 붙여 주는 메소드

```python
colors = ['red', 'blue', 'green', 'yellow']
print(colors)
result = ''.join(colors)
print(result)

result = ' '.join(colors)
print(result)

result = ', '.join(colors)
print(result)

result = '-'.join(colors)
print(result)
```

```python
['red', 'blue', 'green', 'yellow']
redbluegreenyellow
red blue green yellow
red, blue, green, yellow
red-blue-green-yellow
```

## Chap 5. Data structure of Python

### 1. Stack

![image-20200710112521906](C:\Users\bitr48\AppData\Roaming\Typora\typora-user-images\image-20200710112521906.png)

#### 1-1) pop

- pop()은 리스트의 맨 마지막 요소를 돌려주고 그 요소는 삭제한다.
- 입력 1

```python
a = [1, 2, 3, 4, 5]
a.append(10)
print(a)
a.append(20)
print(a)

print(a.pop())
print(a)
print(a.pop())
print(a)
```

```python
[1, 2, 3, 4, 5, 10]
[1, 2, 3, 4, 5, 10, 20]

20
[1, 2, 3, 4, 5, 10]
10
[1, 2, 3, 4, 5]
```

- 입력 2)

```python
word = input("Input a word:")
word_list = list(word)
print(word_list)

result = []
for _ in range(len(word_list)): #길이만큼 돌겠다.
    result.append(word_list.pop())

print(result)
print(word[::-1])
```

```python
Input a word:hello #내가 hello라고 input값을 줌
['h', 'e', 'l', 'l', 'o']
['o', 'l', 'l', 'e', 'h']
olleh
```



### 2. Queue

#### 2-1) pop(x)

- pop(x) 
  - x번째껄 빼냄

```python
a = [1, 2, 3, 4, 5]
a.append(10)
a.append(20)
print(a)
print(a.pop(0))
print(a.pop(0))
print(a)
```

```python
[1, 2, 3, 4, 5, 10, 20]
1
2
[3, 4, 5, 10, 20]
```



### 3. Tuple

- () 선언
- **tuple이 선언되면 값을 바꿀 수 없음** **==> list와 다른점**
- 원소가 한개이면 한개인 표시인 콤마를 무조건 넣어줘야 함
- 리스트와 같음. 항목만 써줌

```python
t = (1, 2, 3)
print(t+t, t*2)
print(len(t))

t2 = (1,) # 원소가 한개이면 한개인 표시인 콤마를 무조건 넣어줘야 함
print(t2)
```

```python
(1, 2, 3, 1, 2, 3) (1, 2, 3, 1, 2, 3)
3

(1,)
```



### 4. Set

- 중복값 삭제
- 순서가 없음. 입력하는대로 나온다고 생각하면 안됨
- 입력 1)

```python
s = set([1, 2, 3, 1, 2, 3]) 
print(s)

s.add(1)  #1 한개만 삭제
print(s)
s.remove(1)  #2 없는 항목을 remove 하면 오류가 발생
print(s)
s.update([1, 4, 5, 6, 7])  #3 리스트
print(s)
s.discard(3)  #4 없는 항목을 discard 하면 아무일 없이 
print(s)
s.clear()  #5
print(s)
```

```python
{1, 2, 3}
{1, 2, 3}
{2, 3}
{1, 2, 3, 4, 5, 6, 7}
{1, 2, 4, 5, 6, 7}
set()
```

- 입력 2)

```python
s1 = set([1, 2, 3, 4, 5])
s2 = set([3, 4, 5, 6, 7])

print(s1.union(s2))
print(s1 | s2)
#print()
print(s1.intersection(s2))
print(s1 & s2)
#print()
print(s1.difference(s2))
print(s1 - s2)
```

```python
{1, 2, 3, 4, 5, 6, 7}
{1, 2, 3, 4, 5, 6, 7}

{3, 4, 5}
{3, 4, 5}

{1, 2}
{1, 2}
```



### 5. Dictionary

- Java 에서 Hashmap, general하게는 dictionary
- key, value type
- 입력 1)

```python
student_info = {20190001: 'Tom', 20190002: 'Jane', 20190003: 'Mike', 20190004: 'Jessica'}
print(student_info[20190002])

student_info[20190002] = 'Kate'
print(student_info)

student_info[20190005] = 'David'
print(student_info)
```

```python
Jane
{20190001: 'Tom', 20190002: 'Kate', 20190003: 'Mike', 20190004: 'Jessica'}
{20190001: 'Tom', 20190002: 'Kate', 20190003: 'Mike', 20190004: 'Jessica', 20190005: 'David'}

```

- 입력 2)

```python
country_code = {'USA': 1, 'Korea': 82, 'China': 86, 'Malaysia': 60}
print(country_code)

print(country_code.keys())

country_code['German'] = 49
print(country_code)

print(country_code.values())
print(country_code.items()) # tuple 형태의 리스트로 만들어 줌
print()

for k, v in country_code.items(): # unpacking
    print('Key:', k)
    print('Value:', v)

print('Korea' in country_code.keys())
print(85 in country_code.values())
```



```python
{'USA': 1, 'Korea': 82, 'China': 86, 'Malaysia': 60}
dict_keys(['USA', 'Korea', 'China', 'Malaysia'])
{'USA': 1, 'Korea': 82, 'China': 86, 'Malaysia': 60, 'German': 49}
dict_values([1, 82, 86, 60, 49])
dict_items([('USA', 1), ('Korea', 82), ('China', 86), ('Malaysia', 60), ('German', 49)])

Key: USA
Value: 1
Key: Korea
Value: 82
Key: China
Value: 86
Key: Malaysia
Value: 60
Key: German
Value: 49
True
False
```

### 6. Collections module

- 기본 자료구조를 확장하여 미리 제작하고, 빠이썬 모듈로 제공
- deque, OrderedDict, defaultdict, counter, namedtuple 등

#### 6-1) deque

- collection 이란 모듈안에 deque이라는 클래스를 가져온다. 여기서 deque은 deque클래스 안에 deque이라는 메소드를 호출해서 deque이라는 객체를 만든다.

- deque과 queue 의 차이
  - deque: 양쪽다 입출력이 가능하다
- 입력 1)

```python
from collections import deque

deque_list = deque()
for i in range(5):
    deque_list.append(i)

print(deque_list) #1

print(deque_list.pop()) #2
print(deque_list.pop())
print(deque_list)

deque_list.appendleft(5)
deque_list.appendleft(6)
print(deque_list)#3

print(deque_list.popleft())#4
print(deque_list.popleft())
print(deque_list)
```

```python
deque([0, 1, 2, 3, 4]) #1
4 #2
3
deque([0, 1, 2])
deque([6, 5, 0, 1, 2])#3
6 #4
5
deque([0, 1, 2])
```

- 입력 2)

```python
from collections import deque

deque_list = deque()
for i in range(5):
    deque_list.appendleft(i)

print(deque_list)

deque_list.rotate(2)
print(deque_list)

deque_list.rotate(-2)
print(deque_list)

deque_list.extend([5, 6, 7])
print(deque_list)

deque_list.extendleft([9, 10]) #순서 헷갈리지 말기 !! 시험 
print(deque_list)
```

```python
deque([4, 3, 2, 1, 0])
deque([1, 0, 4, 3, 2])
deque([4, 3, 2, 1, 0])
deque([4, 3, 2, 1, 0, 5, 6, 7])
deque([10, 9, 4, 3, 2, 1, 0, 5, 6, 7])
```

#### 6-2) OrderedDict

- 내가 입력한 순서대로 순서를 보장함
- 잘 안씀

##### lambda

- 첫번째 요소를  key로 써라

- 입력 1)

```python
from collections import OrderedDict

d = dict() #생성자 호출
d['x'] = 100
d['y'] = 200
d['z'] = 300
d['a'] = 400
print(d) #1

od = OrderedDict(sorted(d.items(), key=lambda x: x[0])) # key값 정렬

print()
print(od)#2

od_list = sorted(od.items(), key=lambda x: x[1]) #value값 정렬 

print()
print(od_list)#3
```

```python
{'x': 100, 'y': 200, 'z': 300, 'a': 400} #1

OrderedDict([('a', 400), ('x', 100), ('y', 200), ('z', 300)]) #2

[('x', 100), ('y', 200), ('z', 300), ('a', 400)] #3
```

#### 6-3) defaultdict

- default로 하나를 지정해줌

```python
from collections import defaultdict

d = defaultdict(lambda: 100)
print(d['first'] + 10)

d2 = defaultdict(int)
print(d2['aaa'])

s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1)]
d2 = defaultdict(list)

for k, v in s:
    d2[k].append(v) # key값이 list값으로 만들었기 때문에 append가 됨

print(d2.items())
```

```python
110
0
dict_items([('yellow', [1, 3]), ('blue', [2, 4]), ('red', [1])])
```



#### 6-4) counter

- 입력 1)

```python
from collections import Counter

c = Counter('scientist')
print(c)

print(c['i'])
print(c['n'])
```

```python
Counter({'s': 2, 'i': 2, 't': 2, 'c': 1, 'e': 1, 'n': 1})
2
1
```

- 입력 2)
  - dictionary에 count 후 elements

```python
from collections import Counter

c = Counter({'red': 4, 'blue': 2})
print(c)

print(list(c.elements()))
```

```python
Counter({'red': 4, 'blue': 2})
['red', 'red', 'red', 'red', 'blue', 'blue']
```

- 입력 3)

```python
from collections import Counter

c = Counter(cats=4, dogs=6)
print(c)

print(list(c.elements()))
```

```python
Counter({'dogs': 6, 'cats': 4})
['cats', 'cats', 'cats', 'cats', 'dogs', 'dogs', 'dogs', 'dogs', 'dogs', 'dogs']
```

- 입력 4)

```python
from collections import Counter

c = Counter(a=4, b=2, c=0, d=-2)
d = Counter(a=1, b=2, c=3, d=4)

print(c + d)
print(c & d) # 0과 음수는 false라고 생각하면 됨
print(c | d) # or는 더 큰값을 가져옴

c.subtract(d) # 빼기를 한다는 subtract 메소드를 가져옴
print(c)
```

```python
# dictionary type은 순서가 없음, ordereddict 해야함.
Counter({'a': 5, 'b': 4, 'c': 3, 'd': 2})
Counter({'b': 2, 'a': 1})
Counter({'a': 4, 'd': 4, 'c': 3, 'b': 2}) 
Counter({'a': 3, 'b': 0, 'c': -3, 'd': -6})
```



#### 6-5) namedtuple

- 이름이 있는 tuple, 잘 안씀

```python
from collections import namedtuple

Point = namedtuple('my_point', ['x', 'y'])
p = Point(11, 22)
print(p)
print(p.x, p.y)
print(p[0], p[1])
```

```python
my_point(x=11, y=22)
11 22
11 22
```

##### # practice)

- 단어들의 개수들을 센다음에 단어가 많은 순으로 나열하시오

```python
A press release is the quickest and easiest way to get free publicity. If
	 well written, a press release can result in multiple published articles about your 
	firm and its products. And that can mean new prospects contacting you 
    asking you to sell to them. ….
```

- 정답

```python
from collections import defaultdict

text = """A press release is the quickest and easiest way to get free publicity. If
	 well written, a press release can result in multiple published articles about your 
	firm and its products. And that can mean new prospects contacting you 
    asking you to sell to them. ….""".lower().split()

word_count = defaultdict(lambda: 0)
for word in text:
    word_count[word] += 1

from collections import OrderedDict
for k, v in OrderedDict(sorted(word_count.items(), key=lambda t: t[1], reverse=True)).items():
    print(k,v)
```

### 7. list comprehension

#### 7-1) One line

- 입력 1)

```python
result = []

for i in range(10):
    if i % 2 == 0:
        result.append(i)

print(result)

result2 = [i for i in range(10) if i % 2 == 0]
print(result2)

result3 = [i if i % 2 == 0 else 99 for i in range(10)]
print(result3)
```

```python
[0, 2, 4, 6, 8] #result
[0, 2, 4, 6, 8] #result2
[0, 99, 2, 99, 4, 99, 6, 99, 8, 99] #result3
```

- 입력 2)

```python
word1 = 'Hello'
word2 = 'World'
result = [i + j for i in word1 for j in word2]
print(result)
```

```python
# 위와 같음
word1 = 'Hello'
word2 = 'World'
result= []
for i in word1:
    for j in word2:
        result.append(i+j)
print(result)
```



```python
['HW', 'Ho', 'Hr', 'Hl', 'Hd', 'eW', 'eo', 'er', 'el', 'ed', 'lW', 'lo', 'lr', 'll', 'ld', 'lW', 'lo', 'lr', 'll', 'ld', 'oW', 'oo', 'or', 'ol', 'od']
```

- 입력3)

```python
case1 = ['A', 'B', 'C']
case2 = ['A', 'B', 'C']
result = [i + j for i in case1 for j in case2 if i!=j]
print(result)
```

```python
['AB', 'AC', 'BA', 'BC', 'CA', 'CB']
```

#### 7-1) list in list

```python
case1 = ['A', 'B', 'C']
case2 = ['D', 'E', 'F']

result = [[i + j for i in case1] for j in case2] # 바깥쪽이 베이스
print(result)
```

```python
[['AD', 'BD', 'CD'], ['AE', 'BE', 'CE'], ['AF', 'BF', 'CF']]
```

### 8. enumerate

- 반복문 사용 시 몇 번째 반복문인지 확인이 필요할 수 있음

```python
for i, v in enumerate(['tic', 'tac', 'toe']):
    print(i,v)
```

```python
0 tic
1 tac
2 toe
```

- dictionary 형태로 출력

```python
result = {i: j for i, j in enumerate("""The Dark Tower is a series of eight books and one short story written by American author Stephen King""".split())}
print(result)
```

```python
{0: 'The', 1: 'Dark', 2: 'Tower', 3: 'is', 4: 'a', 5: 'series', 6: 'of', 7: 'eight', 8: 'books', 9: 'and', 10: 'one', 11: 'short', 12: 'story', 13: 'written', 14: 'by', 15: 'American', 16: 'author', 17: 'Stephen', 18: 'King'}
```

### 9. zip

- 동일한 개수로 이루어진 자료형을 묶어 주는 역할을 하는 함수

```python
alist = ['a1', 'a2', 'a3']
blist = ['b1', 'b2', 'b3', 'b4']
for a, b in zip(alist, blist):
    print(a, b)
```

```python
a1 b1
a2 b2
a3 b3
```

- 입력 1)

```python
a, b, c = zip((1, 2, 3), (10, 20, 30), (100, 200, 300))
print(a, b, c)
```

```python
(1, 10, 100) (2, 20, 200) (3, 30, 300)
```

- 입력 2)
  - 입력 1)의 결과를 sum 함수를 통해 list형식으로 만듬

```python
result = [sum(x) for x in zip((1, 2, 3), (10, 20, 30), (100, 200, 300))]
print(result)
```

```python
[111, 222, 333]
```

- 입력 3)

```python
alist = ['a1', 'a2', 'a3']
blist = ['b1', 'b2', 'b3']
for i, (a, b) in enumerate(zip(alist, blist)):
    print(i, a, b)
```

```python
0 a1 b1
1 a2 b2
2 a3 b3
```

#### 9-1) lambda

- java 에서는 익명구현객체를 람다식으로 대체
  python 에서는 익명함수를 람다식으로 대체
- 오직 one line만 가능

```python
모두 같은 소스
----------------------------------------1
def f(x, y):
    return x + y

print(f(1, 4))
----------------------------------------2
f1 = lambda x, y: x + y

print(f1(1, 4))
----------------------------------------3
print((lambda x, y: x + y)(1, 4))
```

- 

```python
f = lambda n, m: n if n%2 == 0 else m
print(f(1, 3))
print()
print(f(2, 3))
```

```python
3

2
```

- lambda로 익명함수로 만들어 주고 익명함수로 리턴해줌

```python
def makeFunc(n):
    return lambda a : a % n == 1

# isOdd = lambda a : a % 2 == 1
isOdd = makeFunc(2)

# isOdd = lambda 3 : 3 % 2 == 1  = True
print(isOdd(3))
# isOdd = lambda 4 : 4 % 2 == 1  = False
print(isOdd(4))
```

```python
True
False
```



### **args

```python
def key_variable_length(**args):
    print(args)
    print("First value is {first}".format(**args))
    print(f"First value is {args.get('first')}")
    print("Second value is {second}".format(**args))
    print("Third value is {third}".format(**args))


key_variable_length(first=3, second=4, third=5)
```

```python
{'first': 3, 'second': 4, 'third': 5}
First value is 3
First value is 3
Second value is 4
Third value is 5
```



### 10. asterisk

```python
def asterisk_test(a, *args): #여러개의 collection 인자를 가변인자로 받을 때
    print(a, args)
    print(type(args))
    
asterisk_test(1, 2, 3, 4, 5, 6)
```

```python
1 (2, 3, 4, 5, 6)
<class 'tuple'>
```

#### 10-1) **kargs

- **kwargs 와 같음

```python
def asterisk_test2(a, **kargs):
    print(a, kargs)
    print(type(kargs))
    
asterisk_test2(1, b=2, c=3, d=4, e=5, f=6)
```

```python
1 {'b': 2, 'c': 3, 'd': 4, 'e': 5, 'f': 6}
<class 'dict'>
```

### 11. unpacking

- 인자로 * 받을 때는 개수로 받는다는 의미고
  실행문에서 * 받을때는 unpacking을 의미 

```python
def unpacking_test(a, args):
    print(a, *args) #unpacking
    print(type(args))

unpacking_test(1, (2, 3, 4, 5, 6))
```

```python
1 2 3 4 5 6
<class 'tuple'>
```

- 

```python
def unpacking_test2(a, *args):
    print(a, args)
    print(type(args))
    
unpacking_test2(1, *(2, 3, 4, 5, 6))
```

```python
1 (2, 3, 4, 5, 6)
<class 'tuple'>
```

- 

```python
a, b, c = ([1, 2], [3, 4], [5, 6])
print(a, b, c)

data = ([1, 2], [3, 4], [5, 6])
print(data)
print(*data)
```

```python
[1, 2] [3, 4] [5, 6]
([1, 2], [3, 4], [5, 6])
[1, 2] [3, 4] [5, 6]
```

#### 11-1) zip unpacking 

- pythonic 한 langauge

```python
tom_score = [95, 85, 90]
jane_score = [90, 90, 100]
kate_score = [100, 100, 80]
student_scores = [tom_score, jane_score, kate_score] # list in list
tom_total = 0
jane_total = 0
kate_total = 0
for tom, jane, kate in zip(*student_scores): # *: unpacking, zip
    tom_total += tom
    jane_total += jane
    kate_total += kate
    
print((tom_total / 3, jane_total / 3, kate_total /3))
```

````python
(90.0, 93.33333333333333, 93.33333333333333)
````

#### 11-2) dict unpacking

```python
def unpacking_dict(a, b, c, d):
    print(a, b, c, d)
    
data = {'b': 1, 'c': 2, 'd': 3}
unpacking_dict(10, **data)
```

```python
10 1 2 3
```

