# 객체지향 프로그래밍 II #
## 상속 ##

	class Child extends Parent {
	...
	}

Child 클래스는 Parent 클래스의 멤버변수를 모두 가지고 메서드도 모두 상속받게 됩니다.

클래스 간의 관계는 두 개중 하나로 사용되는 경우가 대부분입니다.

1. has-a: 한 클래스가 다른 클래스를 멤버변수로 소유합니다.
2. is-a: 한 클래스는 다른 클래스와 같은 종류입니다.(한 클래스가 다른 클래스를 상속했습니다.)

여러 부모를 가지는 경우도 가능하지만(이론적으로는) 자바는 이런 다이아몬드 상속을 금하고 있습니다. 

자바의 모든 클래스는 java.lang.Object를 상속받습니다. 명시적으로 선언하던 하지않던 Object 클래스는 늘 상속받습니다.

	class MyClass extends Object {
	...
	}

위의 코드처럼 명시적으로 선언하는 것도 가능하고...

	class MyClass {
	...
	}
위의 코드처럼 생략해도 가능합니다.

## 오버라이딩 ##
오버라이딩(overriding)은 Parent 클래스의 method를 Child 클래스에서 수정하는 것을 말합니다. 필요에 맞게 재정의하는 것입니다.

오버라이딩에는 몇가지 조건이 필요합니다.

1. 메서드의 이름이 같아야 하고
2. 매개변수가 같아야 하고
3. return 값이 같아야 합니다.(이게 과연 필요할까요? 타입 conversion이 안 일어난다는 보장을 어떻게 하지요?)


추가로 몇가지 조건이 더 필요합니다.

4. Child 클래스의 접근 제어자가 더 엄격할 수 없습니다. Parent가 protected 메서드를 사용하는데 Child 클래스가 private일 수 없습니다. protected와 public만 허용됩니다.
5. Child 클래스는 예외를 다루는데 Parent 클래스보다 더 관용적이어야 합니다.

### 오버라이딩과 오버로딩의 차이 ###
오버로딩은 Parent에서 없는 메서드을 Child에서 추가하는 것이고 오버라이딩은 Parent에 있는 메서드를 Child에서 수정하는 것입니다. 

### super 키워드 ###
super 키워드는 Child 클래스 내부에서 Parent 클래스의 멤버변수를 구별해 지칭할 때 사용할 수 있습니다. 같은 이름을 Parent 클래스와 Child 클래스에서 사용하고 있다면(뭐 대부분이 그렇겠지요) this와 super 키워드로 다른 멤버변수를 지칭할 수 있습니다.

super 키워드는 static 메서드에서 사용할 수 없습니다. 인스탄스를 만들지 않는데 무슨 super입니까?

	class Test {
		public static void main()(String[] args) {
			Child c = new Child();
			c.method();
		}
	}

	class Parent {
		int num = 20;
	}

	class Child extends Parent {
		int num = 40;
		void method() {
			system.out.println("num: " + num);
			system.out.println("num(this): " + this.num);
			system.out.println("num(super): " + super.num);
		}
	}
### super() - Parent 클래스의 생성자 사용하기 ###
this()가 클래스 내부에서 생성자를 지칭하는 이름이듯 super()도 Child 클래스에서 Parent 클래스의 생성자를 지칭하는 이름입니다.

Child 클래스의 생성자는 Parent 클래스의 생성자를 호출합니다. (생략하면 컴파일러가 추가합니다.) 

**기본적으로 Parent 클래스의 멤버변수는 Parent 클래스의 생성자가 생성하도록 합니다.
**

	public class TestSuperConstructor {
	    public static void main(String[] args) {
	        Child c = new Child();
	        c.method();
	    }
	}
	
	class Parent {
	    int x = 20;
	    int y = 30;
	
	    Parent(int x, int y) {
	        this.x = x;
	        this.y = y;
	    }
	}
	class Child extends Parent {
	    int z = 40;
	
	    Child() {
	        this(20, 30, 40);
	    }
	
	    Child(int x, int y, int z) {
	        super(x, y);
	        this.z = z;
	    }
	
	    void method() {
	        System.out.println("x: " + x);
	        System.out.println("y: " + y);
	        System.out.println("z: " + z);
	    }
	}
		
## 패키지와 import ##

1. 패키지는 클래스의 모음입니다.
2. 패키지는 디렉토리 구조를 반영합니다. 예를 들어 `java.lang.String` 클래스는 `java/lang/String.java` 파일에 정의되어 있습니다.

파이썬과 비슷한 것 같네요.

패키지의 선언은 

`package package_name;`으로 합니다. 이 구문을 실행한 이후의 클래스는 `package_name`에 묶이게 됩니다.

** 모든 클래스는 반드시 하나의 패키지에 포함되어야 합니다. ** 패키지 선언없이 클래스 정의가 가능했던 이유는 `이름없는 패키지`에 선언되기 때문입니다.

> 패키지를 컴파일 하려면 뭐 약간의 작업이 필요합니다. 일단 넘어가겠습니다. 

다른 패키지를 사용하려면 `import`를 사용합니다.

	import java.util.Calendar;
	import java.util.Date;
	import java.util.Arraylist;

이렇게도 가능하고 아래처럼 `*`을 사용할 수도 있습니다.

	import java.util.*

하지만 아래처럼 사용할 수는 없습니다. 아래처럼 `import`를 사용해도 상위의 클래스를 `import`하지는 않습니다.

	import java.*; 

혹시 빠트리더라도 `import java.lang.*;`은 언제나 실행됩니다.

algospot online-judge에서는 package선언을 하지 않도록 요구합니다. 이렇게 하면 이름없는 패키지에 클래스가 선언되겠지요.

	import java.util.Date;
	import java.text.SimpleDateFormat;
	public class Chapter07TestImport {
	    public static void main(String[] args) {
	        Date today = new Date();
	
	        SimpleDateFormat date = new SimpleDateFormat("yyyy/MM/dd");
	        SimpleDateFormat time = new SimpleDateFormat("hh:mm:ss");
	
	        System.out.println("오늘의 날짜는: " + date.format(today));
	        System.out.println("현재 시간은: " + time.format(today));
	    }
	}


SimpleDateFormat 클래스에 대해 조금 더 알아봅시다. 사용법이 생소해서 찾아보니 이렇습니다. 

SimpleDateFormat 인스턴스 formatter의 메서드로 `format()`이 있고 Date 객체를 매개변수로 받습니다.

	public StringBuffer format(Date date, StringBuffer toAppendTo, FieldPosition pos)

`java.util.Date`대신 `java.util.Calendar`를 사용할 수 있습니다. 이 경우 Calendar는 추상클래스이므로 생성자를 사용할 수 없고 getInstance() 메서드를 사용해 객체를 만듭니다. 