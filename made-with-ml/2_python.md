# Python

[Made With ML - Python](https://madewithml.com/courses/foundations/python/#variables) 의 내용을 정리해보았다.



파이썬의 기초적인 부분부터 설명이 되어있지만 내가 다시 짚었으면 하는 내용 위주로 정리하려 한다.



### **\*args, \*\*kwargs**

- arguments
- keyword arguments

여기서 중요한 것은 `asterisk` 이다. 라틴어로 별이라는 의미를 가진 asterisk는 파이썬에서 가변인자를 표현할 때 사용한다. 1개는 positonal 가변인자, 2개는 keyword 가변인자를 나타낸다.

이를 생각해보면 args와 kwargs라는 단어는 중요한 것이 아니다.

**1**

```python
def f(*args, **kwargs):
    x = args[0]
    y = kwargs.get('y')
    print (f"x: {x}, y: {y}")
```

**2**

```python
def f(*a, **b):
    x = a[0]
    y = b.get('y')
    print (f"x: {x}, y: {y}")
```

위의 1번과 2번은 정확히 같은 동작을 수행한다.



변수명은 바뀔 수 있지만 순서는 바뀔 수 없다. 이는 불확실성을 없애기 위함인데 순서는 다음과 같다.

1. 일반 변수
2. *변수
3. **변수

*변수는 positinal arguments로 여러개의 변수가 들어올 때 함수 내부에서 여러 변수들을 튜플로서 처리한다.

**변수는 keyword arguments로 키워드와 함께 입력되어야하고 함수내부에서 이를 묶어서 딕셔너리로서 처리한다.



위 내용은 [[나룸 중급 파이썬1] *args와 **kwargs](https://brunch.co.kr/@princox/180)를 참고하여 작성하였다.



### **Class**

**\_\_str\_\_**

str은 사실 내장 함수가 아니고, 파이썬의 기본 내장 클래스이다. 이는 `help(str)` 을 통해 확인해볼 수 있다. 여기서 str과 \_\_str\_\_의 관계는 str이라는 함수를 통해 클래스 내부에 정의된 매직메소드 \_\_str\_\_를 호출하는 것이다. 그래서 우리가 클래스를 정의할 때 매직메소드 \_\_str\_\_ 를 정의하면 어떻게 될까?

```python
class Pet(object):
    def __init__(self, species, name):
        self.species = species
        self.name = name

    def __str__(self):
        return f"{self.species} named {self.name}"

dog1 = Pet("Dog", "miki")
str(dog1)

# >>> 'Dog named miki'
```



위 내용은 믿고보는 박성환님의 블로그 [[Python] __str__와 __repr__의 차이 살펴보기](https://shoark7.github.io/programming/python/difference-between-__repr__-vs-__str__) 를 참고하여 작성하였다!! <- 여기 더 좋고 깊은 내용이 있으니 확인할 것!!!!



**상속**

위에서 정의한 Pet 클래스를 상속받아 새로운 클래스 Dog를 정의한다.

```python
class Dog(Pet):
    def __init__(self, species, name, breed):
        super().__init__("dog", name)
        self.breed = breed

    def __str__(self):
        return f"{self.breed} named {self.name}"
```

새로운 클래스에서 \_\_init\_\_ 과 \_\_str\_\_ 두개의 함수를 정의했지만 정의한 방식은 다르다. 첫번째는 부모 클래스의 해당 함수 내용을 그대로 가져와 이어서 사용했고 두번째는 부모 클래스의 내용은 무시하고 현재 정의한 대로 오버라이딩하였다. 



**class method, static method**

클래스메소드와 스태틱메소드 두가지 모두 클래스의 인스턴스와 상관없이 클래스에 접근할 때 사용한다. 클래스의 일반 메소드는 `self` 라는 인스턴스를 가리키는 객체를 통해 접근하기 때문에 인스턴스에 종속적이지만 **@classmethod**는 클래스의 변수에 접근이 가능하며(cls라는 인자를 암묵적으로 받아야한다) 인스턴스에 따라 종속적이지 않다. 다시 말하자면, 같은 클래스의 인스턴스라면 같은 일을 수행한다는 의미이다. **@staticmethod**는 클래스 변수에 접근이 불가능하다. 이는 클래스변수에도 종속적이지 않음을 의미한다. 혼자서 단독적인 행위를 위해 정의하면 된다.



위의 내용도 박성환님의 블로그 [[Python] classmethod VS staticmethod](https://shoark7.github.io/programming/python/staticmethod-and-classmethod-in-Python)를 참고하였다.



**데코레이터**

>  함수를 받아서 새로운 함수를 만들어 반환하는 함수

함수의 실행시간을 측정하고 싶다고 가정하면 함수의 시작과 끝에 `time.time()` 을 통해 시간을 측정할 수 있다. 하지만 시간을 측정하고 싶은 함수가 여러개라면?? 매우 번거로워진다. 이때 함수를 반환하는 함수를 만들어 손쉽게 이를 적용할 수 있다. 데코레이터가 이러한 함수이다. 위에서 설명한 `@classmethod`, `@staticmethod`가 이와같은 데코레이터이다. 



함수는 기본적으로 docstring을 통해 \_\_doc\_\_이라는 매직메소드로 설명을 확인할 수 있고 이를 바탕으로 help라는 함수가 동작한다.?



아래는 함수의 실행시간을 측정해 알려주는 `cal_time` 이라는 데코레이터와 이를 이용한 `print_hello`라는 함수를 정의하였다. \_\_doc\_\_을 통해 `print_hello`함수의 docstring을 확인해보자

```python
def cal_time(f):
  	# @functools.wraps(f)
    def wrapper(*args, **kwargs):
        """Wrapper function for @cal_time."""
        start_time = time.time()
        f(*args, **kwargs)
        end_time = time.time()
        exec_time = end_time - start_time
        print("Execute time : {}".format(exec_time))
    return wrapper
  
@cal_time
def print_hello():
    """print hello function"""
    print("HELLO")

print_hello.__doc__

# >>> Wrapper function for @cal_time.
```

결과는 데코레이터의 docstring이 출력되었다. 이는 내가 원하는 정보가 아니다. 또한 \_\_name\_\_을 통해 메소드에 접근할 때도 wrapper를 가리킨다. 이는 디버깅에서 혼란을 야기할 수 있다. 이를 해결하기 위해 wrapper 함수에 `@functools.wraps` 데코레이터를 적용하면된다. 정확한 동작의 원리는 잘 모른다..!! 



**Callbacks**

데코레이터는 위에서 보았다시피 실행 전후의 과정에 관여가 가능하다. 하지만 함수 내부에 접근하고자 한다면?? 이때 고려해볼만한것이 callback이라는 기법이다.

콜백은 "파이썬에서 모든것은 객체다."라는 아이디어의 집합체라는 생각이든다.

기본예시는 다음과 같다. 

```python
# Callback
class x_tracker(object):
    def __init__(self, x):
        self.history = []
    def at_start(self, x):
        self.history.append(x)
    def at_end(self, x):
        self.history.append(x)
        
# Function
def operations(x, callbacks=[]):
    """Basic operations."""
    for callback in callbacks:
        callback.at_start(x)
    x += 1
    for callback in callbacks:
        callback.at_end(x)
    return x

x = 1
tracker = x_tracker(x=x)
operations(x=x, callbacks=[tracker])

tracker.history
# >>> [1, 2]
```

인스턴스를 인자로 전달하여 메소드에 접근한다는 발상이 재밌었다.

코드를 보면 이해가 될 것이라고 생각하고 이만 줄인다.





















