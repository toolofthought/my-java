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

### 오버라이딩과 오보로딩의 차이 ###
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

기본적으로 Parent 클래스의 멤버변수는 Parent 클래스의 생성자가 생성하도록 합니다.


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
		

		
			
			
