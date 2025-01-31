## **⚙ Python 문법**

***



###  **1. 이항 연산자**

### **2. 뮤터블, 이뮤터블 객체**

### **3. 슬라이싱**

### **4. 날짜와 시간**

### **5. 흐름 제어**

### **6. 예약어**

### **7. 함수**

### **8. 익명함수 - 람다**









<br>



### **⚙ [1] 이항 연산자**

> 파이썬에서 제공하는 이항 연산자

- +, -, *, / : 기본 사칙연산
- a // b : a를 b로 나눈 몫을 취한다(소수점 이하는 버린다.)
- a ** b : a의 b승을 구한다.
- a & b : a와 b 모두 True인 경우 True를 반환(AND 연산)
- a | b : a 또는 b 둘중 하나가 True이거나 둘 다 True인 경우 True를 반환(OR 연산)
- a ^ b : a와 b의 XOR 연산
- a == b : a와 b가 같은 경우 True
- a != b : a와 b가 다른 경우 True
- <, <=, >, >= : 부등호에 적합한 경우 True
- a is b : a와 b가 같은 객체 참조 시 True
- a is not b : a와 b가 다른 객체 참조 시 True



<br>



### **⚙ [2] 뮤터블, 이뮤터블 객체**

> 리스트, 사전, Numpy 배열 도는 사용자 정의 클래스 같은 대부분의 객체는 변경이 가능하다(뮤터블)
>
> - 객체나 값의 내용을 바꿀 수 있음을 의미

* Mutable

  ```python
  a_list = ['foo', 2, [4, 5]]
  a_list[2] = (3, 4)
  
  a_list
  
  # 결과
  ['foo', 2, (3, 4)]
  ```

  

* Immutable

  > 문자열이나 튜플은 변경 불가능

  ```python
  a_tuple = (3, 5, (4, 5))
  a_tuple[1] = 'four'
  # print TypeError Message
  ```

  

<br>

### **⚙ [3] 슬라이싱**

> 파이썬 시퀀스 자료구조에 구현되어 있다.

```python
s = 'python'

# list에 문자열 삽입
list(s)

# 3번째 원소 까지 출력
s[:3]

# 결과
'pyt'
```



<br>

### **⚙ [4] 날짜와 시간**

> 내장 datetime module은 datetime, date, time 형을 지원한다.
>
> **datetime** : date와 time 정보를 함께 저장하며 주로 사용되는 자료형



```python
from datetime import datetime, date, time

# 년, 월, 일, 시, 분, 초 format
dt = datetime(2021, 10, 29, 20, 30, 21)

# dt에서 요일을 추출
dt.day
# 결과 : 29

# dt에서 분을 추출
dt.minute
# 결과 : 30

# strftime method : datetime을 문자열로 만들어준다.
dt.strftime('%m/%d/%y %H:%M')
# 결과 : '10/29/2011 20:30'

# strptime method : 문자열을 datetime 객체로 만들어준다.
datetime.strptime('20210215', '%y%m%d')
# 결과 : datetime.datetime(2021, 02, 15, 0, 0)
```



- **시계열 데이터 집계 시 datetime의 필드 치환이 유용한 경우가 있음**

  ```python
  # 분과 초 필드를 0으로 치환해서 새로운 객체 생성
  # datetime.datetime은 변경 불가능
  # 두 datetime 객체의 차가 datetime.timedelta 객체를 반환한다.
  dt.replace(minute=0, second=0)
  # 결과 : datetime.datetime(2011, 10, 29, 20, 0)
  
  # datetime 객체 선언
  dt2 = datetime(2011, 11, 15, 22, 30)
  
  # 두 datetime 객체의 차가 timedelta 객체를 반환한다.
  # timedelta(17, 7179) 결과 : 17일과 7179초만큼의 시간 차이를 나타냄
  delta = dt2-dt
  delta
  # 결과 : datetime.timedelta(17, 7179)
  
  # timedelta 객체 + 첫 번째 datetime 객체 : 시간이 미뤄진 datetime 객체 추출
  # dt 객체 : datetime.datetime(2011, 10, 29, 20, 30, 21)
  # delta 객체 : datetime.timedelta(17, 7179)
  dt + delta
  # 결과 : datetime.datetime(2011, 11, 15, 22, 30)... dt2 객체
  ```

  

  

<br>

### **⚙ [5] 흐름 제어**

> 조건절, 반복문, 표준 흐름 제어를 위한 예약어를 가지고 있다.



- **if 문**
  - 조건 검사 -> 조건 True인 경우 블록 내 코드 수행
  - and, or과 함께 사용 시 왼쪽에서 오른쪽 순서로 검사(왼쪽 조건이 True일 경우 오른쪽 검사 안한다)

- **for 문**

  - 리스트, 튜플 같은 컬렉션이나 이터레이터 순회

    ```python
    for value in collection:
        # value를 이용하는 코드 작성
    ```

  - 예약어

    - **continue** : 특정 조건의 블록을 건너뛸 수 있다. 
    - **break** : for 문을 빠져나갈 수 있다.

- **while 문**

  - 해당 조건이 False가 되거나 break 문을 사용해서 명시적으로 반복을 끝낼 때까지<br> 블록 내의 코드를 수행한다.

- **pass**

  - 아무것도 하지 않음을 나타낸다.
  - 블록에서 어떤 작업도 실행하지 않을 때 사용한다.
  - **구현하지 않은 코드를 나중에 추가하기 위한 플레이스 홀더 용도**

  ```python
  if x < 0:
      print('negative')
  elif x == 0:
      pass
  else:
      print('positive')
  ```

- **range 함수**

  - 연속된 정수를 넘겨주는 이터레이터를 반환한다.
  - start, end, step(음수가 될 수도 있다) 값 지정 가능

  ```python
  list(range(0, 20, 2))
  # 결과 : [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
  ```

- **삼항 표현식**

  - if-else 블록을 한 줄로 표현할 수 있도록 한다.
  - value = **true-expr** if condition else **false-expr**
    - **true-expr** : condition이 True일 경우 동작
    - **false-expr** : condition이 False일 경우 동작
    - ex) 'Non-negative' if x >= 0 else 'Negative'

<br>

### **⚙ [6] 예약어**

- **in** 예약어

  - 리스트에 어떤 값이 존재하는지 검사

    ```python
    a_list = (1, 3, 5, 7)
    3 in a_list
    # True 
    ```

- **not** 예약어

  - in 예약어를 반대 의미로 사용

  - 리스트에 어떤 값이 존재하지 않는지 검사

    ```python
    3 not in a_list
    # False(3이 a_list에 존재하기 때문에 False 출력)
    ```

    <br> 

### **⚙ [7] 함수**

- 코드를 재사용, 조직화하기 위한 중요 수단

- **def** 예약어로 정의, **return** 예약어를 사용해서 값을 반환

- **return**문은 여러 개를 사용해도 상관없다.

- 함수 블록이 끝날 때까지 return 문이 존재하지 않는다면 None이 자동으로 반환된다.

- 여러 개의 일반 인자와 키워드를 인자로 받을 수 있다.

  ```python
  def func(x, y, z=1.5):
      if z > 1:
          return z * (x+y)
      else:
          return z/(x+y)
  ```

- 여러 값을 반환할 수 있다.

  ```python
  def f():
      a = 5
      b = 6
      c = 7
      return a, b, c
  a, b, c = f()
  a
  # 5
  b
  # 6
  c
  # 7
  ```

<br> 

- **[전역과 지역 스코프에서 변수 참조, Namespace]**

  - 함수 내에서 선언된 변수(지역 네임스페이스) : 함수 호출 시 생성, 함수 인자를 통해 즉시 생성, 함수 종료 시 소멸

    ```python
    def func():
        a = []
        for i in range(5):
            a.append(i)
    ```

  - 함수 외부에서 선언된 변수(전역 네임스페이스) : 시스템 전체의 상태를 저장하기 위한 용도로 사용

    - 많이 사용하게 되면 클래스를 사용하는 객체지향 상황 반증

    ```python
    a = None
    
    def bind_a_value():
        global a # 함수 스코프 밖에서 변수에 값을 대입하려면 그 변수를 global 예약어로 선언
        a = []
    ```

    <br> 

### **⚙ [8] 익명 함수 - 람다**

- 단순한 한 문장으로 이루어진 함수를 말한다.

- 람다 함수 객체에는 명시적인 ' __name__' 속성이 없다.

- lambda 예약어로 정의한다.

  ```python
  # 기본 함수
  def short_func(x):
      return x * 2
  
  # 람다 함수
  equiv = lambda x: x * 2
  ```

  

 

