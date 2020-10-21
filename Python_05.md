# Python_05

## Generator

- 제곱을 만들어주는 리스트 코드

```python
#일반 코드
def square_numbers(nums):
    result = []
    for i in nums:
        result.append(i * i)
    return result

my_nums = square_numbers([1, 2, 3, 4, 5])

print(my_nums)
```

```python
[1, 4, 9, 16, 25]
```

### yield

```python
#1
def square_numbers(nums):
    for i in nums:
        yield i * i
        
        
my_nums = square_numbers([1, 2, 3, 4, 5])
print(next(my_nums))
print(next(my_nums))
print(next(my_nums))
print(next(my_nums))
print(next(my_nums))

#2
def square_numbers(nums):
    for i in nums:
        yield i * i

my_nums = square_numbers([1, 2, 3, 4, 5])

for num in my_nums:
    print(num)
    
#3

my_nums = (x * x for x in [1, 2, 3, 4, 5])

print(my_nums)

for num in my_nums:
    print(num)
    
    
#4

a = [1, 2, 3, 4, 5]

my_nums = (x*x for x in a)

print(my_nums)

print(list(my_nums)) #배열형태로 나옴
```

## First class function

- 함수를 변수취급해서 함수안에 함수를 만들수 있게 함

```python
def double_func(x):
    return x * 2

print(double_func(3))

a = double_func 

print(double_func) 
print(a) 
print(a(5))
```

```python
6
<function double_func at 0x0000016EBBB7FD38>
<function double_func at 0x0000016EBBB7FD38>
10
```



```python
from typing import Callable, List

def double_func(x):
    return x * 2

def make_double_list(func:Callable, args:List) -> List:
    result = []
    for i in args:
        result.append(func(i))
        
    return result

input_list = [1, 2, 3, 4, 5]

doubles = make_double_list(double_func, input_list)

print(doubles)
```

```python
[2, 4, 6, 8, 10]
```



- 함수안의 함수를 리턴

```python
import time

def log_formatter(msg):
    def log_message():
        time_str = time.strftime('%c', time.localtime(time.time()))
        print(time_str, end='')
        print(' ----> ', end='')
        print(msg)

    return log_message

log_msg = log_formatter('test log')
print(log_msg)
log_msg()
```

```python
<function log_formatter.<locals>.log_message at 0x0000018A9B39B798>
Wed Jul 15 10:23:07 2020 ----> test log
```

### closure

- log_formatter 함수의 로컬변수 msg는 함수실행이 종료된 후 사라지는 변수
- 종료된 이후에도 참조가 가능? log_message 를 클로저(closure)라고 함
- 클로저는 다른함수의 지역변수 값을 그 함수가 종료된후에도 기억
- 어떤 함수를 함수 자신이 가지고 있는 환경과 함께 저장한 레코드
- 함수가 가진 프리변수(free variable)를 클로저가 만들어지는 당시의 값과 레퍼런스에 매핑하는 역할
- 자신의 영역 밖에서 호출된 함수의 변수값과 레퍼런스를 복사하고 저장

##### ## free variable

- 코드블럭 안에서 사용은 되지만 그 코드블럭안에서 정의되지 않은 변수

```python
import time

def log_formatter(msg):
    def log_message():
        time_str = time.strftime('%c', time.localtime(time.time()))
        print(time_str, end='')
        print(' ----> ', end='')
        print(msg) #msg는 free variable

    return log_message

log_msg = log_formatter('test log')
print(log_msg)
log_msg()

del log_formatter # 함수 삭제
try:
    print(log_formatter)
except NameError:
    print('log_formatter 함수는 존재하지 않습니다.')

log_msg()
```

```python
<function log_formatter.<locals>.log_message at 0x0000018A9B399DC8>
Wed Jul 15 10:32:50 2020 ----> test log
log_formatter 함수는 존재하지 않습니다.
Wed Jul 15 10:32:50 2020 ----> test log
```

- 

```python
def outer_func():
    msg = 'Good Morning! ' #outter 함수에서는 local 변수
    def inner_func():
        print(msg) #inner func에서는 msg가 free variable

    return inner_func() 


outer_func()
```

```python
Good Morning! 
```

- 

```python
def outer_func():
    msg = 'Good Morning! '
    def inner_func():
        print(msg) 

    return inner_func


func = outer_func()
print(func)
func()
```

```python
<function outer_func.<locals>.inner_func at 0x0000018A9B39BAF8>
Good Morning! 
```

#### dir

- dir 안에 객체를 집어넣으면 객체안에 멤버들을 표시해주는 func

```python
def outer_func():
    msg = 'Good Morning! '
    def inner_func():
        print(msg)

    return inner_func


func = outer_func()
print(func)

print(dir(func))
print(type(func.__closure__))
print(func.__closure__)
print(func.__closure__[0])
print(func.__closure__[0].cell_contents)
```

```python
<function outer_func.<locals>.inner_func at 0x0000018A9B39BAF8>
['__annotations__', ..., '__subclasshook__']
<class 'tuple'>
(<cell at 0x0000018A9B2E2DC8: str object at 0x0000018A9B61EC70>,)
<cell at 0x0000018A9B2E2DC8: str object at 0x0000018A9B61EC70>
Good Morning! 

```



#### decorate pattern

```python
import time

def log_decorator(param_func):
    def log_message():
        time_str = time.strftime('%c', time.localtime(time.time()))
        print(time_str, end='')
        print(' ----> ', end='')
        return param_func()
        
    return log_message

def test_log_msg():
    print('This is test log message')
    
def runtime_log_msg():
    print('This is runtime log message')
    
test_log = log_decorator(test_log_msg) # 객체지향의 decorate 패턴
runtime_log = log_decorator(runtime_log_msg)

test_log()
print()
runtime_log()
```

```python
Wed Jul 15 11:19:50 2020 ----> This is test log message
Wed Jul 15 11:19:50 2020 ----> This is runtime log message
```

##### @log_decorator

- @ = 함수를 데코레이터 하겠다

```python
import time

def log_decorator(param_func):
    def log_message():
        time_str = time.strftime('%c', time.localtime(time.time()))
        print(time_str, end='')
        print(' ----> ', end='')
        return param_func()

    return log_message

@log_decorator
def test_log_msg():
    print('This is test log message')

@log_decorator
def runtime_log_msg():
    print('This is runtime log message')

test_log_msg()
print()
runtime_log_msg()
```

```python
Wed Jul 15 11:22:32 2020 ----> This is test log message
Wed Jul 15 11:22:32 2020 ----> This is runtime log message
```

##### # 가변인자를 받는 decorator

```python
import time

def log_decorator(param_func):
    def log_message(*args, **kargs): #dictionary type{}은 맨뒤에 넣으쇼
        time_str = time.strftime('%c', time.localtime(time.time()))
        print(time_str, end='')
        print(' ----> ', end='')
        return param_func(*args, **kargs)

    return log_message


@log_decorator
def runtime_log_msg(host, ip):
    print(f'This is runtime log message {host} : {ip}')

print()
runtime_log_msg('localhost', '192.168.1.10')
```

```python
Wed Jul 15 13:11:15 2020 ----> This is runtime log message localhost : 192.168.1.10
```



