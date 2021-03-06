### 스프링부트

- 스프링 기반 단독 실행 가능한 어플리케이션 생성 가능

  - tomcat, jetty or undertow 임베드 되어있음
  - starter 컴포넌트를 제공
  - auto configuration
  - etc

- @SpringBootApplication 어노테이션
  - auto configuration
  - 컴포넌트 스캔 (각종 컴포넌트 읽어옴)

### 강의 중간 나온 용어/개념 정리

- IOC

  - 어떤 객체가 사용할 객체(의존관계인 객체)를 직접 선언하여 사용하는 것이 아니라, 어떤 방법을 사용하여(ex. 생성자)사용하여 주입 받아 사용하는 것
    > https://velog.io/@max9106/Spring-IOC%EB%AF%B8%EC%99%84

```java
/*
일반적인 제어권: 자기가 사용할 의존성은 자기가 만들어서 사용
*/
@Service
public class CarService {
	private CarRepository carRepository = new CarRepository();
}
/*
Inversion Of Control
다른 누군가가 의존성을 밖에서 준다.(제어권의 역전)
의존성을 주입해주는 일:Dependency Injection(일종의 IOC)
*/
@Service
public class CarService {

    // CarRepository를 사용은 하지만 만들지는 않는다.
	private CarRepository carRepository;

    /*
    생성자를 통해서 받아온다.
    따라서 의존성을 관리하는 일은 CarService가 하는 일이아니다. 누군가 밖에서 해주는 것이다.
    */
    public CarService(CarRepository carRepository){
    	this.carRepository = carRepository;
    }
}
```

- 스프링 IOC 컨테이너
  - IOC기능을 제공하는 컨테이너. Bean들을 담고있음, Bean 정의를 읽어들이고, Bean을 구성하고 제공.(Bean을 만들어주고, 엮어주고, 제공해줌)
    > https://velog.io/@max9106/Spring-IOC%EB%AF%B8%EC%99%84
- Bean
  - 컨테이너 안에 들어있는 객체들. 컨테이너에 담겨있기 때문에 사용하려면 컨테이너에서 가져와야한다. 여러 annotaion을 사용하여 일반적인 객체를 bean으로 등록할 수 있다. 또한 Bean에 등록되어있는 객체들을 쉽게 주입받아 사용할 수 있다.의존성 주입을 하기 위해서는 Bean이 되어야한다.
    > https://velog.io/@max9106/Spring-IOC%EB%AF%B8%EC%99%84
- Annotation
  - @를 이용한 주석, 자바코드에 주석을 달아 특별한 의미를 부여한 것
    (참고로 클래스, 메소드, 변수 등 모든 요소에 선언이 가능)
  - 메타데이터(실제데이터가 아닌 Data를 위한 데이터) 라고도 불리고 JDK5부터 등장
  - 컴파일러가 특정 오류를 억제하도록 지시하는 것과 같이 프로그램 코드의 일부가 아닌
    프로그램에 관한 데이터를 제공, 코드에 정보를 추가하는 정형화된 방법.
    데이터에 대한 유효성 검사조건을 어노테이션을 사용하여 Model 클래스에 직접 명시함으로써
    해당 데이터들에 대한 유효 조건을 쉽게 파악할수 있게되며, 코드의 양도 줄어든다.
