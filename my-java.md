# chapter 01 자바를 시작하기 전에 #
## 환경 구성 - 첫번째 ##
* Java SDK 다운로드 받기: Java SDK로 검색해서 나온 링크를 따라갔습니다. 버전은 Java SE(Standard Edition)을 선택했습니다. 기본값을 따라 설치했습니다.
* IntelliJ community 다운로드 받기: 자바 프로그래밍 환경을 어떻게 구성할지 고민하다 IntelliJ를 설치하는 걸로 결론지었습니다. 일반 자바 프로그래밍을 연습하는데는 [커뮤니티](https://www.jetbrains.com/idea/download/#section=windows)버전도 크게 지장이 없어 보입니다. 마찬가지로 기본 설정을 이용해 설치했습니다.
* IntelliJ 실행하기: 처음 프로젝트를 시작할 때 jdk 위치를 지정해야 합니다. Java JDK기본 위치는 자바 구성에서 선택해세요

## 환경 구성 - 두번째 ##
IntelliJ에 정착하지 못했습니다. 뭐가 뭔지 모르겠어요. 이렇게 된 이상 이클립스로 갑니다.

* 이클립스 다운로드 및 설치: Eclipse IDE for Java  Developers 다운받고 설치합니다.
* workspace 설정: dropbox/eclipse/workspace로 설정했습니다.

## Hello, World 실행하기 ##
1. 프로젝트를 만들고
2. class를 추가합니다. 이름은 적당하게 지어주세요. 아무것도 하지 않으니 파일이름과 클래스 이름이 같아지네요.
3. 입력하고 ctrl+F11

코드는 아래와 같습니다.

	class Hello
	{
		public static void main(String[] args)
		{
			System.out.println("Hello, World");
			System.out.println("This is your first Java program.");
		}
	}

## 에러 메시지 ##
그냥 잘 넘어갈 리가 없지요. Editor does not contain a main type 에러가 나왔습니다. 찾아보니 eclipse에러이고 project아래 src에 파일이 없으면 나온다나? 뭐 하여튼 그렇다고 합니다.

이거 사용하면서 발견했는데 src폴더 안에 폴더를 또 만들어서  파일을 저장하면 새로 만든 파일 내부의 파일을 자동으로 인식하지 못하는 듯합니다. 그래서 어떻게 하냐? 파일 오른쪽 클릭. add to source path? 이런 식으로 추가하면 제대로 동작하더이다.

**주의사항**

> 하나의 소스에 여러 클래스를 정의하는 것이 가능하지만 소스파일의 이름과 public class의 이름은 일치해야 합니다. 만약 publc class가 파일에 없다면 이름은 원하는 대로 명명해도 괜찮습니다.

## 자바 프로그램 실행과정 ##
1. 컴파일: javac.exe(자바 컴파일러)가 Hello.java를 바이트코드로 컴파일합니다. 확장자를 달지않고 그냥 클래스 이름이 프로그램이 되나보네요.
2. 실행: java.exe(자바 인터프리터)가 바이트코드를 해석하고 실행합니다.

## 자바 프로그램이 실제로 실행되는 순서 ##
`java Hello`로 실행하면

1. 프로그램의 실행에 필요한 클래스 파일을 로드하고
2. 클래스 파일을 검사하고
3. 지정된 클래스에서 main(String[] args)를 호출합니다.
4. 마지막 코드까지 모두 실행되면 프로그램은 종료되고 모든 자원은 반환됩니다.

**사소한 팁**
> 주석은 /* */ 혹은 //로 합니다.


# chapter 06 객체지향 프로그래밍 I #
객체지향의 사실과 오해라는 책과 내용을 섞겠습니다.

## 객체지향언어 ##
객체지향 프로그래밍은 코드를 재사용하고 코드 관리를 용이하게 합니다. 신뢰성 높은 프로그램을 작성할 수 있도록 준다고 합니다.

## 클래스와 객체 ##
### 객체 ###
> 객체를 이해하는데 세가지가 필요합니다. 역할, 책임 그리고 협력. 객체는 책임을 지고 역할을 하고 다른 객체와 협력합니다.

> 객체는 상태와 행위를 하나의 단위로 묶는 자율적인 존재이다.

> 객체의 대양한 특성을 효과적으로 설명하기 위해서는 객체를 상태(state), 행동(behavior), 식별자(identifier)를 지신 실체로 보는 것이 가장 효과적이다.

### 객체와 인스턴스(instance) ###
> 객체어 어떤 개념을 적용하는 것이 가능해서 개념 그룹의 일원이 될 때 객체를 그 개념의 인스턴스(instance)라고 한다. 따라서 객체를 다음과 같이 정의할 수 있다.

> 객체란 특정 개념을 적용할 수 있는 구체적인 사물을 의미한다. 개념이 객체에 적용되었을 때 객체를 그 개념의 인스턴스라고 한다.

### 분류와 타입 ###
분류란 객체에 특정한 개념을 적용하는 작업이다. 객체에 특정한 개념을 적용하기로 결심했을 때 우리는 그 객체를 특정한 집합의 멤버로 분류하고 있는 것이다.

개념을 대체할 수 있는 용어로 타입을 사용합니다. 

### 객체와 클래스의 관계 ###
> 초기 객체지향 프로그래밍 언어의 초점은 새로운 개몀의 데이터 추상화를 제공하는 클래스라는 빌딩블록에 맞춰져 있었다.

> 클래스는 객체들의 협력관계를 코드로 옮기는 도구에 불과하다.

그래서 클래스가 뭐냐면 객체지향 프로그래밍 언어에서 정적인 모델(그 모델이 가질 수 있는 모든 상태와 행동을 시간에 독립적으로 나열하는 모델)은 클래스를 이용해 구현됩니다.

클래스는 타입을 구현하는 여러 방법 중 정적인 모델을 이용한 방법입니다.

> 객체를 분류하는 기준은 타입이며 타입은 나누는 기준은 객체가 수행하는 행동.

> 객체를 분류하기 위해 타입을 결정한 후 프로그래밍 언어를 이용해 타입을 구현할 수 있는 한가지 방법.

> 클래스는 타입을 구현하기 위해 프로그래밍 언어에서 제공하는 구현 메커니즘

### 나의 언어로 표현하면... ###
객체가 항상 먼저이고 객체를 분류하는데 타입이 필요하고 정적인 타입을 이용하는 방법이 클래스이다. 클래스는 일종의 static type을 정의하는 방법이더라.

모든 것은 객체이고 객체를 구별하는 기준 혹은 타입이 있으면 그것을 적용한 후 객체를 그 기준 혹은 타입의 인스턴스라고 합니다. 메서드는 객체가 받은 메세지를 어떻게 처리하는지 방법을 메서드라고 하며 객체는 메서드를 자율적으로 선택합니다.

타입에는 동적/정적 타입이 있고 정적타입을 프로그래밍 언어로 구현한 것이 클래스입니다. 정적타입은 클래스가 가질 수 있는 모든 상태를 시간에 무관하게 정하는 방식을 말합니다.


## 변수와 메서드 ##
### 메서드 ###
> 객체가 수신된 메세지를 처리하는 방법을 메서드라고 부른다.

객체는 메세지를 처리하기 위한 방법을 자율적으로 선택합니다.


### 객체 생성하기 ###
type referenceVariableName = new type();

## 변수와 메서드 ##
예를 들어 아래와 같은 클래스가 있으면..

	class Variables
	{
		int iv; //instance variable
		static int cv; //class variable
		void method()
		{
			int lv = 0; // local variable
		}
	}

iv는 인스턴스 생성될 때마다 생성되는 변수, cv는 static 키워드를 이용해서 클래스에 모두 공유되는 변수입니다. lv는 local 변수입니다.

클래스 변수는 인스턴스를 생성하지 않아도 바로 사용할 수 있습니다. 이런 개념을 확장해서 클래스 메서드를 만들기도 하는데 인스턴스를 생성하지 않고 메서드만 따로 사용할 수 있는 방법입니다. 예를 들어 Math.abs() 같은 메서드를 클래스 메서드로 정의해두면 클래스를 namespace처럼 사용하며 바로 연산에 이용할 수 있습니다.

### JVM 메모리 구조 ###
위의 설명은 메모리 구조를 알게 되면 자연히 해결되는 문제입니다. 굳이 외울 필요가 없습니다.

JVM의 메모리는 세가지 입니다.
* method area: 클래스 정의가 올라옵니다. 클래스 변수도 이 영역에 저장됩니다.
* call stack: 메서드 작업에 필요한 작업공간을 제공합니다.
* heap: 인스턴스가 저장됩니다. 인스턴스 변수가 여기에 저장됩니다.

## 메서드 오버로딩 ##
* 함수 이름이 동일하고
* 매개변수의 개수와 타입이 같을 때

메서드가 오버로딩되어 있다고 말합니다. 리턴타입은 오버로딩과 아무런 관련이 없습니다.

## 생성자 ##
### 생성자란? ###
* 생성자는 리턴 타입이 없습니다.
* 생성자는 클래스 이름과 동일합니다.

### 생성자에서 다른 생성자 호출하기 ###
생성자 내부에서 다른 생성자를 호출할 수 있습니다. this() 를 사용합니다. 단 생성자 첫 줄에서만 사용할 수 있습니다.

예를 들어

	class Car
	{
		String color;
		String gearType;
		int door;
		
		Car()
		{
			this("white", "auto", 4);
		}
		
		Car(String color)
		{
			this(color, "auto", 4);
		}
		
		Car(String color, String gearType, int door)
		{
			this.color = color;
			this.gearType = gearType;
			this.door = door;
		}
	}
	
	class CarTest
	{
		public static void main(String[] args)
		{
			Car c1 = new Car();
			Car c2 = new Car("blue");
			System.out.println("(" + c1.color + "," + c1.gearType + "," + c1.door + ")");
			System.out.println("(" + c2.color + "," + c2.gearType + "," + c2.door + ")");
	
		}
	}

this는 인스턴스 내부에서 스스로를 지칭하는 키워드입니다.

### 생성자를 이용해 복사하기 ###
	
	Car(Car c)
	{
		this.color = c.color;
		this.gearType = c.gearType;
		this.door = c.door;
	}

### 변수의 초기화 ###
1. 명시적 초기화
2. 생성자
3. 초기화 블록
	1. 클래스 멤버 초기화: static { ...}
	2. 인스턴스 멤버 초기화: {...}안에 들어있는 인스턴스 멤버를 초기화 함. 인스턴스가 만들어질 때마다 실행되기 때문에 { System.out.println("인스턴스가 생성되었습니다."; }를 클래스에 넣으면 생성될 때마다 실행됩니다. 굳이 생성자마다 넣을 필요가 없습니다.
	







