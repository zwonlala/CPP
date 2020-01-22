# Chapter01 C언어 기반의 C++

## 01-1. printf와 scanf를 대신하는 입출력 방식

입출력하기 위해선 `#include <iostream>` 해야함<br>
- `<iostream.h>`은 과거의 표준 입출력 라이브러리 및 헤더파일을 의미
- `<iostream>`은 새로운 표준 입출력 라이브러리 및 헤더를 의미

C++에선 데이터의 입력도 출력도 별도의 포맷 지정이 필요 없다<br>
<br>
문자열도 그냥 하면 됨!!
```C++
ex) 
char str[100];
std::cin >> str;
```
<br>

지역변수 선언이 함수 내 어디서든 삽입이 가능<br>
<br>

```
std::cin >> '변수1' >> '변수2';
```
위와 같이 연속적인 데이터의 입력을 할 수도 있다<br>
이때 첫번째 변수와 두번째 변수의 경계는 탭, 스페이스바, Enter키의 입력과 같은 공백에 의해 나눠진다<br> 

for문의 초기화 문장 내에서 변수 선언이 가능<br>

<br>
<br>
<br>
<br>

## 01-2. 함수 오버로딩(Function Overloading)

C언어에서는 동일한 함수가 정의되는 것을 허용하지 않음<br>
(∵ 두 함수의 이름이 같기 때문에 컴파일 오류가 발생함)<br>
<br>
함수 호출 시 전달되는 인자를 통해서 호출하고자 하는 함수의 구분이 가능하기 때문에 매개변수의 선언형태가 다르면, 동일한 이름의 함수정의를 허용할 수 있다<br>
-> 이러한 함수 정의를 가리켜 `함수 오버로딩(Function Overloading)`이라고 한다<br>
<br>
그럼 C언어는 허용하지 않는데 C++는 허용하는 이유는..?<br>
-> ∵ 호출할 함수를 찾는 방식이 서로 다르기 때문..!   

> C++ : 	'함수의 이름', '매개변수의 선언'
  
> C	: 	'함수의 이름'

따라서 C언어는 함수의 오버로딩이 불가능하며, 문법적으로 허용하지도 않음!
<br>
<br>
C++은 호출할 함수를 찾을 때, 다음 두가지 정보를 동시에 활용.

```
ex)
MyFunc(30, 40);
``` 
=> "두 개의 int형 정수를 인자로 전달 받을 수 있는 MyFunc라는 이름의 함수를 찾아야겠다!"

<br>
<br>

함수의 오버로딩이 가능하려면, 매개변수의 선언이 달라야 함.<br>

```C++
ex1)
int MyFunc(char c) {...}
int MyFunc(int n) {...}
```
위 두 함수는 오버로딩이 가능(∵ 매개변수의 자료형이 다르므로)<br>

<br>
<br>

```C++
ex2)
int MyFunc(int n) {...}
int MyFunc(int n1, int n2) {...}
```
위 두 함수는 오버로딩이 가능(∵ 매개변수의 갯수가 다르므로)<br>

<br>

=> 따라서 결론을 내리면 함수의 오버로딩이 가능하려면
"매개변수의 자료형 또는 갯수가 달라야 한다!!'

<br>
<br>

```C++
ex3)
void MyFunc(int n) {...}
int MyFunc(int n) {...}
```


위 두 함수는 오버로딩이 불가능<br>
(∵ 두 함수는 반환형만 다른데, 반환형은 함수 호출 시, 호출되는 함수를 구분하는 기준이 될 수 없음)<br>
-> 위와 같은 함수 정의는 컴파일 오류로 이어짐



<br>
<br>
<br>
<br>




## 01-3. 매개변수의 디폴트 값(Default Value)


다음과 같이 함수의 매개변수에 다음의 형태로 선언하는게 가능
```C++
int MyFuncOne (int num = 7)
{
	return num + 1;
}

int MyFuncTwo (int num1 = 5, int num2 = 7) 
{
	return num1 + num2;
}
```

위 MyFuncOne의 매개변수 선언은 다음과 같음<br>

`int num = 7;`<br>

그리고 이건 `"함수호출 시 인자를 전달하지 않으면, 7이 전달될 것으로 간주하겠다."`<br>
<br>
따라서 아래 두 문장은 동일한 의미를 갖는다<br>
```C++
MyFuncOne(); //7이 전달된 것으로 간주
MyFuncOne(7);
```

```C++
MyFuncTwo(); //5와 7이 전달 된 것으로 간주
MyFuncTwo(5, 7);
```
<br>
<br>

```C++
예제코드)DefaultValue1.cpp

#include <iostream>

int Adder(int num1 = 1, int num2 = 2)
{
	return num1 + num2;
}

int main(void) 
{
	std::cout << Adder() << std::endl;
	std::cout << Adder(5) << std::endl; //인자를 하나만 전달하고 있음. 이때는 인자는 첫번째 매개변수로 전달된다. 그래서 두번째 매개변수에는 2가 전달된 걸로 간주
	std::cout << Adder(3, 5) << std::endl; //매개변수의 디폴트 값은 의미를 갖지 않음.
	return 0;
}
```
<br>
정리하면!<br>
<br>
"매개변수에 디폴트 값이 설정되어 있으면, 선언된 매개변수의 수보다 적은 수의 인자전달이 가능!<br>
그리고 전달되는 인자는 왼쪽에서부터 채워져 나가고, 부족분은 디폴트 값으로 채워진다."<br>

<br>

또 함수원형을 별도로 선언하는 경우, 매개변수의 디폴트 값은 함수원형 선언에만 표현해야 함.<br>
-> ∵ 만약에 디폴트 값의 선언이 함수의 선언부분에 위치하지 않는다면, 컴파일이 불가능할 것이다..!<br>

<br>
<br>

**부분적 디폴트 값 설정**

<br>
디폴트 값을 설정할 때 매개변수 전부 다가 아닌 일부만 설정 할 수 있다.<br>
<br>
그리고 그때는 반드시 오른쪽 매개변수의 디폴트 값투터 채우는 형태로 정의해야 한다.<br>

즉 다음과 같은 함수정의는 유효하다!<br>

```C++
int YourFunc(int num1, int num2, int num3=30) {...}
int YourFunc(int num1, int num2 = 20, int num3 = 30) {...}
int YourFunc(int num1 = 10, int num2 = 20, int num3 = 30) {...}
```

<br>

그리고 다음과 같은 함수 정의는 유효하지 않다.
```C++
int YourFunc(int num1 = 10, int num2, int num3) {...}
int YourFunc(int num1 = 10, int num2 = 20, int num3) {...}
```
<br>

그렇다면 반드시 오른쪽부터 채울 것을 요구하는 이유는 무엇일까..?
-> 함수에 전달되는 인자가 왼쪽에서 오른쪽으로 채워지기 때문!!
-> 그래서 오른쪽부터 채워진 함수의 정의만이 의미를 갖는다!







<br>
<br>
<br>
<br>


## 01-4. 인라인(inline) 함수

인라인 함수를 의역해보면, '프로그램 코드 라인 안으로 들어가 버린 함수'라는 뜻이다.<br>
<br>
C 언어의 매크로 함수를 기억해 보면 이런 장/단점이 존재한다.<br>
- 장 : 일반적인 함수에 비해서 실행속도의 이점이 있다.
- 단 : 정의하기가 어렵다. 복잡한 한수를 매크로의 형태로 정의하는데 한계가 있음.

위와 같은 조건을 만족하는 것이 바로 C++의 인라인 함수이다.
<br>


```C++
예제)InlineFunc.cpp
#include <iostream>

inline int SQUARE (int x) //키워드 inline의 선언을 통해 함수 SQUARE는 인라인 함수가 되었다.
{
	return x*x;
}

int main(void)
{
	std::cout << SQUARE(5) << std::endl; //SQUARE 함수를 호출하고 있다. 그런데 이 함수는 인라인 함수이니 몸체부분이 호출문을 대체하게 된다.
	std::cout << SQUARE(12) << std::endl;
	return 0;
}
```


참고로 매크로를 활용한 함수의 인라인화는 전처리기가 처리하지만,<br>
키워드 inline을 이용한 함수의 인라인화는 컴파일러에 의해 처리가 됨.<br>
따라서 컴파일러가 함수의 인라인화가 오히려 성능에 해가 된다고 판단할 경우, 이 키워드를 무시하기도 함. <br>
또 컴파일러가 필요한 경우에 일부 함수를 임의로 인라인 처리하기도 함<br>
<br>

매크로 함수에는 있지만, 인라인 함수에는 없는 장점<br>
```C
#define SQUARE(x) ((x)*(x))
```
위 매크로는 자료형에 의존적이지 않은 함수이다. 그래서 자료형에 상관없이 사용이 가능하나<br>

인라인 함수는 다른 자료형으로 호출하면 데이터의 손실이 일어난다.<br>
물론 함수의 오버로딩을 통해 이 문제를 해결할 수 있으나, 그렇게 되면 함수를 추가로 정의하는 꼴이 되니 한번만 정의하면 되는 매크로 함수의 장저모가는 거리가 멀어진다.<br>
그러나 C++의 탬플릿이라는 것을 이용하면, 매크로 함수와 마찬가지로 자료형에 의존적이지 않은 함수가 완성된다.<br>



<br>
<br>
<br>
<br>




## 01-5. 이름 공간(namespace)에 대한 소개

이름 공간이란 쉽게 말하면, '이름을 붙여놓은 공간'이다.<br>
말 그대로 특정 영역에 이름을 붙여주기 위한 문법적 요소이다.<br>
<br>

**이름공간의 등장배경**

프로그램이 대형화 되어 가면서 이름의 충돌문제가 등장


```C++
#include <iostream>

void SimpleFunc(void)
{
	std::cout << "BestCom이 정의한 함수" << std::endl;
}

void SimpleFunc(void)
{
	std::cout << "ProgCom이 정의한 함수" << std::endl;
}

int main(void)
{
	SimpleFunc();
	return 0;
}
```


위의 코드를 보면 함수의 이름과 매개변수의 형과 갯수가 동일하기 때문에 문제가 된다.<br>
근데 BestCom과 ProgCom이 각각 자신만의 이름공간을 만들고 함수를 정의하거나 변수를 선언한다면 이름충돌은 발생하지 않는다.<br>
<br>

위의 코드는 이와 같이 바꿀 수 있다.

```C++
#include <iostream>

namespace BestComImpl
{
	void SimpleFunc(void)
	{	
		std::cout << "BestCom이 정의한 함수" << std::endl;
	}
}

namespace ProgComImpl
{
	void SimpleFunc(void)
	{	
		std::cout << "ProgCom이 정의한 함수" << std::endl;
	}
}

int main(void)
{
	BestComImpl::SimpleFunc();
	ProgComImpl::SimpleFunc();
	return 0;
}
```

위 예제에서 사용된 연산자 `"::"`를 가리켜 `'범위지정 연산자(scope resolution operator)'`라 하며, <br>
그 이름이 의미하듯이 이름공간을 지정할 때 사용하는 연산자 이다.<br>

<br>
<br>


**이름공간 기반의 함수 선언과 정의의 구분**

일반적으로 함수의 선언과 정의를 분리하는 것이 일반적<br>
'함수의 선언'은 `헤더 파일`에 저장하고,<br>
'함수의 정의'는 `소스 파일`에 저장하는 것이 일반적이다.<br>
다음 예제는 이름공간 기반에서 함수의 선언과 정의를 구분하는 방법이다<br>

```C++
#include <iostream>

namespace BestComImpl //이름공간 안에 함수의 선언만 삽입
{
	void SimpleFunc(void);
}

namespace ProgComImpl //이름공간 안에 함수의 선언만 삽입
{
	void SimpleFunc(void);
}

int main(void)
{
	BestComImpl::SimpleFunc();
	ProgComImpl::SimpleFunc();
	return 0;
}

void BestComImpl::SimpleFunc(void) //이름공간 BestComImpl에 선언된 함수 SimpleFunc의 정의부분
{
	std::cout << "BestCom이 정의한 함수" << std::endl;
}

void ProgComImpl::SimpleFunc(void) //이름공간 ProgComImpl에 선언된 함수 SimpleFunc의 정의부분
{
	std::cout << "ProgCom이 정의한 함수" << std::endl;
}
```































