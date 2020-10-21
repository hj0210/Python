# Python_03

## Chap 6. Class

### 1. static 변수

- 클래스 변수
  - 클래스 내, 메소드 밖에 선언하는 변수
  - 해당 클래스로 생성한 모든 객체가 공통으로 접근할 수 있는 변수
  - "클래스명.변수명" 으로 사용
- 인스턴스 변수
  - 클래스 내부의 메소드 안에서 "self.변수명" 으로 선언한 변수
  - 각 인스턴스 별로 생성
  - 객체 생성후 "객체명.변수명"으로 접근

- 최상위 클래스는 object
- 상속받을 클래스가 default면 object 임.

```python
class 클래스키워드(상속받을클래스):
```

- ```python
  __init__ == 생성자 생성
  self = java에서 this개념, self는 자동주입
  ```

#### SoccerPlayer

```python
class SoccerPlayer:
    def __init__(self, name, position, back_number):
        self.name = name
        self.position = position
        self.back_number = back_number

    def change_back_number(self, new_number):
        print("선수 등번호 변경 From %d to %d" % (self.back_number, new_number))
        self.back_number = new_number

    def __str__(self):
        return "Hello, My name is %s. I play in %s in center." % (self.name, self.position)

chaboom = SoccerPlayer("Chaboom", "CF", 11)

print("현재 선수의 등번호:", chaboom.back_number)
chaboom.change_back_number(9)
print("현재 선수의 등번호:", chaboom.back_number)
print()
print(chaboom)
```

```python
현재 선수의 등번호: 11
선수 등번호 변경 From 11 to 9
현재 선수의 등번호: 9
Hello, My name is Chaboom. I play in CF in center.
```

#### Car

```python
#클래스 생성
class Car:
    instance_count = 0
    
    def __init__(self, size, color):
        self.size = size
        self.color = color
        Car.instance_count += 1
        print(f"자동차 객체의 수: {Car.instance_count}")
        
    def move(self):
        print(f"자동차({self.size} & {self.color})가 움직입니다.")
#객체 생성
car1 = Car("small", "white")
car2 = Car("big", "black")
print(f"Car 클래스의 총 인스턴스 수: {Car.instance_count}")
car1.move()
car2.move()
```

```python
자동차 객체의 수: 1
자동차 객체의 수: 2
Car 클래스의 총 인스턴스 수: 2
자동차(small & white)가 움직입니다.
자동차(big & black)가 움직입니다.
```

### 2. static 메소드

- 독립적으로 동작, 정의할 때 self를 사용하지 않음
- static 메소드 안에서 인스턴스 메소드, 인스턴스 변수에 접근할 수 없음
- 함수 앞에 @staticmethod  를 선언하여 static 메소드를 표시

#### Car

```python
class Car:
    instance_count = 0

    def __init__(self, size, color):
        self.size = size
        self.color = color
        self.speed = 0
        Car.instance_count += 1
        print(f"자동차 객체의 수: {Car.instance_count}")

    def move(self, speed):
        self.speed = speed
        print(f"자동차({self.size} & {self.color})가 ", end='')
        print(f"시속 {self.speed}킬로미터로 전진")

    def auto_cruise(self):
        print("자율 주행 모드")
        self.move(self.speed)

    @staticmethod
    def check_type(model_code):
        if (model_code >= 20):
            print("이 자동차는 전기차입니다.")
        elif (10 <= model_code < 20):
            print("이 자동차는 가솔린차입니다.")
        else:
            print("이 자동차는 디젤차입니다.")
            
    @classmethod
    def count_instance(cls): #반드시 cls를 가져와야함
        print(f"클래스 변수: {cls.instance_count}")
        
car = Car("small", "red")
car.move(80)
car.auto_cruise()
car.check_type(25)
Car.count_instance()
```

```python
자동차 객체의 수: 1
자동차(small & red)가 시속 80킬로미터로 전진
자율 주행 모드
자동차(small & red)가 시속 80킬로미터로 전진
이 자동차는 전기차입니다.
클래스 변수: 1
```

### 3. 상속

#### Bicycle

```python
class Bicycle:
    def __init__(self, wheel_size, color):
        self.wheel_size = wheel_size
        self.color = color

    def move(self, speed):
        print(f"자전거 시속 {speed}킬로미터로 전진")

    def turn(self, direction):
        print(f"자전거: {direction}회전")

    def stop(self):
        print(f"자전거({self.wheel_size}, {self.color}): 정지")


class FoldingBicycle(Bicycle):
    def __init__(self, wheel_size, color, state):
        super().__init__(wheel_size, color)
        self.state = state

    def fold(self):
        self.state = 'folding'
        print(f"자전거: 접기, state = {self.state}")

    def unfold(self):
        self.state = 'unfolding'
        print(f"자전거: 펴기, state = {self.state}")


folding_bicycle = FoldingBicycle(27, 'white', 'unfolding')
folding_bicycle.move(20)
folding_bicycle.turn('right')
folding_bicycle.stop()
folding_bicycle.fold()
folding_bicycle.unfold()
```

```python
자전거 시속 20킬로미터로 전진
자전거: right회전
자전거(27, white): 정지
자전거: 접기, state = folding
자전거: 펴기, state = unfolding
```

### 4. 오버라이딩

```python
class Person:
    def __init__(self, name, age, gender):
        self.name = name
        self.age = age
        self.gender = gender

    def about_me(self):
        print("저의 이름은", self.name, end='')
        print(f"({self.gender})이고요, 제나이는", str(self.age), "살입니다.")


class Employee(Person):
    def __init__(self, name, age, gender, salary, hire_date):
        super().__init__(name, age, gender)
        self.salary = salary
        self.hire_date = hire_date

    def do_work(self):
        print("열심히 일을 한다.")

    def about_me(self):
        super().about_me()
        print("제 급여는", self.salary, "원이고, 제 입사일은", self.hire_date, "입니다.")

emp = Employee('Tom', 25, '남성', 350, '2020/06/02')
emp.do_work()
emp.about_me()
```

```python
열심히 일을 한다.
저의 이름은 Tom(남성)이고요, 제나이는 25 살입니다.
제 급여는 350 원이고, 제 입사일은 2020/06/02 입니다.
```

#### visability

- 기본적으로 python은 public이다.
- 변수명 앞에 __를 주면 외부에서 접근이 불가능 (private)
- 이름 앞 뒤로 __가 있는건 내부적으로 예약되어 있는 것

```python
class Product:
    pass

class Inventory(object):
    def __init__(self):
        self.__items = []

    def add_new_itme(self, product):
        if type(product) == Product:
            self.__items.append(product)
            print("new item added")
        else:
            raise  ValueError("Invalid Item")

    def get_number_of_items(self):
        return len(self.__items)
    
    @property
    def items(self): #getter
        return  self.__items

my_inventory = Inventory()
items = my_inventory.items
print(items)
print()
items.append(Product)
print(items)
my_inventory.add_new_itme(Product())
my_inventory.add_new_itme(Product())
# my_inventory.__itmes # Error 발생
```

```python
[]

[<class '__main__.Product'>]
new item added
new item added
```



## Chap 7. Vector

```python
def add(v, w): # 1
    assert len(v) == len(w)
    return [v_i + w_i for v_i, w_i in zip(v, w)]

assert add([1, 2, 3], [4, 5, 6]) == [5, 7, 9]

def substract(v, w): # 2
    assert len(v) == len(w)
    return [v_i - w_i for v_i, w_i in zip(v, w)]

assert substract([5, 7, 9], [4, 5, 6]) == [1, 2, 3]

def vector_sum(vectors): # 3
    # Check that vectorts is not empty
    assert vectors, "no vectors provided!"

    # Check the vectors are all the same size
    num_elements = len(vectors[0])
    assert all(len(v) == num_elements for v in vectors), "different sizes!"

    return [sum(vector[i] for vector in vectors) for i in range(num_elements)] #첨자가 같은애들끼리 sum

assert vector_sum([[1, 2], [3, 4], [5, 6], [7, 8]]) == [16, 20]

def scalar_multiply(c, v): # 4
    return [c * v_i for v_i in v]

assert scalar_multiply(2, [1, 2, 3]) == [2, 4, 6]

def vector_mean(vecotrs): # 5
    n = len(vecotrs)
    return scalar_multiply(1 / n, vector_sum(vecotrs)) #3을 이용

assert vector_mean([[1, 2], [3, 4], [5, 6]]) == [3, 4]

def dot(v, w): # 6
    assert len(v) == len(w), "vecotrs must be same length"
    return sum(v_i * w_i for v_i, w_i in zip(v, w))

assert dot([1, 2, 3], [4, 5, 6]) == 32 # 1*4 + 2*5 + 3*6

def sum_of_squares(v): #7
    return dot(v, v) #6 을 이용

assert  sum_of_squares([1, 2, 3]) == 14 # 1*1 + 2*2 + 3*3

A = [[1, 2, 3], # A has 2 rows and 3 columns
     [4, 5, 6]]

B = [[1, 2], # B has 3 rows and 2 columns
     [3, 4],
     [5, 6]]

def shape(A): # 8
    num_rows = len(A)
    num_cols = len(A[0]) if A else 0 #number of elements in first row
    return num_rows, num_cols

assert shape([[1, 2, 3], [4, 5, 6]]) == (2, 3) # 2 rows, 3 columns

def get_row(A, i): # 9
    return A[i]

assert get_row(A, 1) == [4, 5, 6]

def get_column(A, j): # 10
    return [A_i[j] # jth element of row A_i
            for A_i in A] # for each row A_i
assert get_column(A, 0) == [1, 4]

```

### unpacking

```python
u = [2, 2] #1
v = [1, 2]
z = [-3, 5]
result = []

for i in range(len(u)):
    result.append(u[i] + v[i] + z[i])

print(result) # [0, 9]

u = [2, 2] #2
v = [1, 2]
z = [-3, 5]
result = [sum[t] for t in zip(u, v, z)]


def vector_addition(*args): #3
    return [sum(t) for t in zip(*args)]

u = [2, 2]
v = [1, 2]
z = [-3, 5]
print(vector_addition(u, v, z))

```

```python
[0, 9]
```

### packing

```python
def vector_addition(*args):
    return [sum(t) for t in zip(*args)]

u = [2, 2]
v = [1, 2]
z = [-3, 5]
print(vector_addition(u, v, z))

def vector_addition(*args):
    print(args) # packing
    print(*args) # unpacking
    return [sum(t) for t in zip(*args)]

vectors = [[2, 2], [1, 2], [-3, 5]]
print(vector_addition(*vectors))  # unpacking
```

```python
[0, 9]
([2, 2], [1, 2], [-3, 5])
[2, 2] [1, 2] [-3, 5]
[0, 9]
```

## Chap 8. Matrix

- 

```python
#a(u+v) = au + av
#2([1, 2, 3] + [4, 3, 3]) = 2[5, 5, 6] = [10, 10, 12]

u = [1, 2, 3]
v = [4, 3, 3]
alpha = 2
result = [alpha* sum(t) for t in zip(u, v)]
print(result)
```

```python
[10, 10, 12]
```

- 

```python
matrix_a = [[3, 6], [4, 5]]
matrix_b = [[5, 8], [6, 7]]

result = [[sum(row) for row in zip(*t)] for t in zip(matrix_a, matrix_b)]

print(result)
```

```python
[[8, 14], [10, 12]]
```

- A^t

```python
a = [[1, 2, 3], [4, 5, 6]]
a_t = [[1, 4], [2, 5], [3, 6]]

matrix_a = [[1, 2, 3], [4, 5, 6]]
result = [[element for element in t] for t in zip(*matrix_a)]
print(result)
```

```python
[[1, 4], [2, 5], [3, 6]]
```

- 행렬 곱 (**<u>매우어려움</u>**)

```python
matrix_a = [[1, 1, 2], [2, 1, 1]]
matrix_b = [[1, 1], [2, 1], [1, 3]]
result = [[sum(a * b for a, b in zip(row_a, column_b))
          for column_b in zip(*matrix_b)] for row_a in matrix_a]
print(result)
```

```python
[[5, 8], [5, 6]]
```



