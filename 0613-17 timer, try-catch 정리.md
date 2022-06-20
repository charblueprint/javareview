## try - catch문 (예외 처리 기능 문법)
> **try - catch문**은 **예외 발생할 코드를 적용**해 사용합니다.  
(1부터 10까지 1초 간격으로 try-catch문를 적용해 미지수 i를 출력하는 코드를 작성해보았습니다.)
```java
public class time1 {

	public static void main(String[] args) {
  		int i = 1;
			do {
				try { 
					Thread.sleep(1000); 
				} catch (InterruptedException e) {
				}
				System.out.println(i);				
				i++;
			} while (i<=10);
   	 }

}
 ```
**Thread.sleep();** 메소드는 *일시정지 상태*를 의미합니다. 여기서 1000은 1초를 의미합니다. 즉, 100은 0.1초를 의미합니다.   
***
>  자주 일어나는 예외 모음
* InterruptedException : 해당 예외 발생이 되었을 경우 처리하기 위한 문법   
* ArrayIndexOutOfBoundsException : 해당 인덱스의 범위를 벗어났을 때   
* NumberFormatException : 문자열로 되어있는 데이터를 숫자로 변경하는 경우   
* ClassCastException : 억지로 타입변환을 시도할 경우  
(+) 타입 변환(Casting)은 상위 클래스와 하위 클래스간에 발생하고 구현 클래스와 인터페이스 간에도 발생한다. 
이러한 관계가 아니라면 클래스는 다른 클래스를 타입으로 변환할 수 없다.
## Time util을 활용해 시간함수 활용
> **timer.scheduleAtFixedRate**(new gogo(), 0, 5000); => **(시작할 메소드/클래스, 몇 초뒤에 시작할 지, 반복 시간)**   **scheduleAtFixedRate** : 지속적으로 반복 작업을 할 때 
TimerTask는 배너나 로딩화면을 실행 할 때 사용한다.   
(adata에 해당하는 4개의 자료들을 4.5초 간격으로 출력하는 코드를 작성하였습니다.)    
```java
import java.util.Timer;
import java.util.TimerTask;

public class time2  {
	
	public static void main(String[] args) {
		Timer timer = new Timer(); 
		TimerTask TT = new TimerTask() { 
			int a = 0;
			String adata[] = {"홍길동","이순신","강감찬","유관순"};
			@Override
			public void run() { //Task에서 실행하는 메소드입니다.
				if(a>=4) { //4바퀴를 돌았을때 a를 0으로 돌려놓아 처음부터 다시 실행되도록 합니다.
					a = 0; 
				}
				System.out.println(adata[a]);
				a++;
			}
		};
		timer.scheduleAtFixedRate(TT, 0, 4500);
	}	
}
```

