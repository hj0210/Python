# Python_06

## Anaconda3 (Jupyter Notenook)



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

```python
2 x 1 = 2
....
2 x 9 = 18
```



##### with

- with를 사용하면 f.close()를 사용안해도 됨

```python
with open("aaa.txt", 'w') as f: #데이터쓰기
    f.write('line1 \n')
    f.write('line2 \n')
    f.write('line3 \n')
    
--------------------------------------------------------------------
with open("aaa.txt", 'r') as f: #데이터읽기
    file_string = f.read()
    print(file_string)
```

```python
line1 
line2 
line3 
```



### 데이터분석 패키지

#### Numpy

- 다차원의 배열을 처리해주는 패키지

##### array

- 1

```python
import numpy as np
data = [0,1,2,3,4,5]
a1 = np.array(data)
a1
```

```python
array([0, 1, 2, 3, 4, 5]) #array라는 것을 명시해주기위해 array라고 나옴
```

- 2

```python
data2 =[0.1, 1,5,4,12,0.5]
a2 = np.array(data2)
a2
```

```python
array([ 0.1,  1. ,  5. ,  4. , 12. ,  0.5]) #실수형태로 나옴
```

##### arange

- 배열생성

```python
np.arange(0,10,2) #1

np.arange(5) #2
```

```python
array([0, 2, 4, 6, 8]) #1

array([0, 1, 2, 3, 4]) #2
```

###### reshape

- 원하는 행열 생성
- 함수.함수 

```python
b1 = np.arange(12).reshape(4,3) # 4x3 행열 생성
b1.shape
```

```python
array([[ 0,  1,  2],
       [ 3,  4,  5],
       [ 6,  7,  8],
       [ 9, 10, 11]])
(4, 3)	`
```

##### linspace

##### zeros

- 배열을 zero 상태로 초기화시킬때

```python
np.zeros((3,4))
```

```python
array([[0., 0., 0., 0.],
       [0., 0., 0., 0.],
       [0., 0., 0., 0.]])
```

##### ones

```python
np.ones(5) #1차원배열
np.ones((3,4)) #2차원배열
```

```python
array([1., 1., 1., 1., 1.]) #1

array([[1., 1., 1., 1.], #2
       [1., 1., 1., 1.],
       [1., 1., 1., 1.]])
```

##### astype

- astype(type이름)
- 형변환

```python
str_1 = np.array(['1.5', '0.65', '2', '4.14', '3.14159265'])
num_1 = str_1.astype(float)
num_1
```

```python
array([1.5       , 0.65      , 2.        , 4.14      , 3.14159265]) 
# '' 표시가 사라짐
```



##### random

![image-20200724142401100](C:\Users\bitr48\AppData\Roaming\Typora\typora-user-images\image-20200724142401100.png)

- 로또번호

```python
np.random.randint(1,45)
for i in range(6):
    print(np.random.randint(1,45))
```

```python
1
10
2
7
21
15
```









#### Pandas



````python
import pandas as pd

s1 = pd.Series([10,20,30,40,50])
s1
````

```python
0    10  #table형태로 나옴
1    20 #data 앞에 index가 붙음
2    30
3    40
4    50
dtype: int64
```

##### DataFrame

- 입력1

```python
pd.DataFrame([[1,2,3],[4,5,6],[7,8,9]])
```

![image-20200724154913890](C:\Users\bitr48\AppData\Roaming\Typora\typora-user-images\image-20200724154913890.png)-  결과2



- 입력2

````python
data_list = np.array([[10,20,30],[40,50,60],[70,80,90]])
pd.DataFrame(data_list)
````

![image-20200724155041991](C:\Users\bitr48\AppData\Roaming\Typora\typora-user-images\image-20200724155041991.png)- 결과2



- 입력3

```python
data = np.array([[1,2,3], [4,5,6], [7,8,9], [10,11,12]])
index_date = pd.date_range('2020-07-24', periods=4)
columns_list = ['A','B','C']
pd.DataFrame(data, index=index_date, columns=columns_list)
```

![image-20200724161522122](C:\Users\bitr48\AppData\Roaming\Typora\typora-user-images\image-20200724161522122.png)

- 입력4-1

```python
data = np.array([["2020", "한국", "1000"],["2021","한국","1500"], ["2022","미국", "500"], ["2023", "한국", "1300"]])
index_date = pd.date_range('2020', periods=4)
columns_list = ['연도','지사','고객수']
pd.DataFrame(data, columns=columns_list)
```

![image-20200724162401379](C:\Users\bitr48\AppData\Roaming\Typora\typora-user-images\image-20200724162401379.png)

- 입력4-2

```python
table_data = {'연도': [2020,2021,2022,2023],
             '지사': ['한국','한국','미국','미국'],
             '고객수': [1000,1500,500,1300]}
table_data
pd.DataFrame(table_data)
```



#### read_csv, read_excel

