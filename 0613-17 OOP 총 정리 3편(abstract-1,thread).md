## 추상 클래스 및 메소드 abstract
> abstract?
자식 클래스에서 반드시 오버라이딩해야만 사용할 수 있는 메소드를 의미합니다.
추상클래스(고스트라고도 부르기도함)는 **외부에서 로드가 절대 안되므로 자체 실행이 되지 않습니다.**

abstract를 쓰는 이유는 크게 **코드를 정형화시키기 위함**입니다. `특정 기능은 다 이 메소드로 사용한다~` 이런 것이죠.
1. 추상클래스는 **실체클래스의 공통적인 부분(변수,메서드)를 추출해서 선언한 클래스**이고
2. 추상클래스는 **객체를 생성할 수 없으며**
3. 추상클래스와 실체클래스는 **상속관계**임을 알 수 있습니다. (추상클래스에서 실체클래스로 상속)

(ab_1이라는 추상클래스를 생성하고 ab_2에게 상속해 출력하는 코드를 작성했습니다. )
``` java
public class oop4 {
	public static void main(String[] args) {
		ab_2 ab = new ab_2();
		System.out.println(ab.b());
		ab.ab_a();
	}
}

abstract class ab_1 { 
	public void ab_a() { // free (인수값 없는 추상 메소드)
		// <<환경설정할 때 쓰임. 팀플때 공용으로 쓸 메소드들 올려 둘 수도 있음
	}
	public void ab_a(int a) { // free(인수값받는 추상 메소드)
	}
	public abstract void ab_c(); //abstract을 쓰기 때문에 {}대신 ;을 쓸 수 있음
	public abstract int b(); // 추상 메소드 - 자체 실행 안 됨
	// 다 free 구성인데 이렇게 선언하는 것이 더 깔끔하다는것

	public abstract int c(); // <<이거 없으면 main method에서 실행할때 오류남
}
class ab_2 extends ab_1 {
	@Override
	public void ab_a() {
		System.out.println(this.c());
	}
	@Override
	public void ab_a(int a) {
	}
	@Override
	public int b() { // 실제 메소드 + 추상 메소드
		// 이렇게 b를 무조건 가져다 써야함
		return 55;
	}
	@Override
	public int c() {
		return 99;
	}
	@Override
	public void ab_c() {
		// 이거 지우고 위에 다시 보면 빨간색 줄 가 있을 걸 그러니까 위에 선언한 건 다 쓰려고 노력은 해야.. 근데 작동 안되는건 아님
		// 위에서 선언하고 안 써서 너 왜 안 쓰냐? 인거지 너 지금 잘못 썼어는 아닌것임 
		// 그리고 보통 리턴 할때 많이 한다 함	
	}
}
```
***
## Thread  & Multi Thread
동작하고 있는 프로그램을 `프로세스(Process)`라고 합니다. 
보통 한 개의 프로세스는 한 가지의 일을 하지만,
쓰레드를 이용하면 한 프로세스 내에서 두 가지 또는 그 이상의 일을 동시에 할 수 있습니다.
#### **Thread** :
프로세스 내부에서 독립적으로 실행되는 작업을 말함.
※ 중요)  Thread 는 **JVM 에 기본으로 탑재**되어있는 메소드이며, (**Thread는 메소드 하나만 단독으로 사용되지 않음**) 
생성자명도 Thread와 **겹치면 안됩니다.**

#### **Multi Thread**  :
프로세서 내부에서 두 가지 이상의 작업을 동시에 사용하는 것을 의미하며 CPU의 코어와 연관이 있습니다.
장점은 **한 번에 우르르 할 수 있다**는 점인데. 예를 들자면, Thread 사용시 음악만 들을 수 있지만 
Multi Thread 사용시 음악, 유투브, 문서 작성이 동시에 즉, 멀티테스킹이 가능해진다는 것입니다.
- `.start();` : Thread 메소드에 기본 run을 작동시키기 위한 start 메소드(함수)입니다.
- `.run();` : Multi Thread의 기본 실행 메소드입니다.
- `.sleep();` :  주어진 시간동안 일시 정지 상태가 되고, 시간이 지나면 다시 실행 대기 상태로 돌아가는 메소드입니다.
- 그 외에도 `.setStop();` 등의 메소드가 존재합니다.
 ***

(1부터 10까지 반복하여 어느 클래스가 돌아가는지 출력하는 반복문을 작성하였습니다.)

```java
public class oop3 {
	public static void main(String[] args) {
		Thread my = new mythread(); // 부모 메소드 = 자식 메소드
		my.start();
		Thread my2 = new mythread2();
		my2.start(); 
		
		int ct = 1;
		while(ct<=10) {
			System.out.println("내부 클래스 : " + ct);
			ct++;
		}
	}
}
class mythread extends Thread{ 
	@Override
	public void run() { 
		int i=1;
		while(i<=10) {
			System.out.println("외부 클래스 : " + i);
			i++;
		}
	}
}
class mythread2 extends Thread{
	@Override
	public void run() {
		int i=1;
		while(i<=10) {
			System.out.println("외부 클래스2 : " + i);
			i++;
		}
	}
}
```
이 경우에는 **Thread가 기본으로 탑재가 되어있는 메소드임으로 부모메서드로 칭해져야 하며**,
extends 받았기 때문에 자식메서드를 작동해도 부모메서드인 Thread까지 동시에 돌아가게 됩니다.
(기존사용형태 : 자식메소드 = 자식메소드)

또한 start();를 사용하여 thread를 실행해 기본 실행 메소드인 run();를 작동하게 되어 
자식 클래스인 `mythread`와 `mythread2`가 동시에 작동됨을 알 수 있습니다.
