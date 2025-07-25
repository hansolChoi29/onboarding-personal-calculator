#  Personal Project Calculator 
진화하는 계산기를 만들어보자! </br>
브랜치 별로 Level1,2,3단계로 구분해놓은 프로젝트입니다.

## 프로젝트 목표

- 제어문과 반복문, 배열과 컬렉션

- 클래스/메서드, Exception & 예외처리, 상속/다형성, SOLID(SRP,OCP)

- Enum, 제네릭, 람다&스트림

## 기술 스택

<p align="left">
  <img src="https://img.shields.io/badge/Java-17-007396?style=for-the-badge&logo=openjdk&logoColor=white" alt="Java Badge"/>
 
  
</p>



## 목차
- [프로젝트 목표](#프로젝트-목표)
- [주요 기능](#주요기능)
- [Trouble Shooting](#trouble-shooting)
- [파일 구조](#파일구조)

## 주요기능
1. 사칙연산 계산기</br>

    - +, -, *, /, % 연산을 지원합니다.

    - 연산자는 각각 AddOperator, SubtractOperator, MultiplyOperator, DivideOperator, ModOperator 클래스로 분리되어 OCP 원칙을 지키며 설계되었습니다.

    - ArithmeticCalculator<T extends Number> 제네릭 클래스를 통해 다양한 숫자 타입을 지원합니다 (int, double 등).

    - 연산 결과는 Calculator 클래스의 results 리스트에 자동으로 저장됩니다.

    - 연산 후 결과를 조건에 따라 필터링하여 조회할 수 있습니다</br>
      - listCal() : 전체 결과 조회</br>

    - printResultsGreaterThan(double threshold) : 특정 값보다 큰 결과만 조회

 2. 원의 넓이 계산</br>
    - 반지름을 입력받아 원의 넓이를 계산합니다.

    - CircleCalculator 클래스에서 수행되며, 결과는 Calculator 클래스의 리스트에 함께 저장됩니다.

    - 음수 반지름에 대해 예외 처리(ArithmeticException)가 되어 있습니다.

```java
CircleCalculator cc = new CircleCalculator();
double area = cc.ArithmeticCalculator(3); // 출력: 28.2743...
```

3. 결과 저장 및 관리 기능</br>
    - 계산된 결과를 List<Double> 형태로 내부 저장소(Calculator 클래스)에 저장

    - removeCal() : 가장 오래된 연산 결과를 삭제

    - listCal() : 전체 결과를 출력

    - setResults(List<Double>) : 외부에서 결과 리스트를 덮어쓸 수 있는 기능 제공

```java
Calculator calc = new Calculator();
calc.addResult(42.0);
calc.listCal();           // 저장된 결과 출력
calc.removeCal();         // 가장 오래된 결과 제거
```

4. 사용자 선택형 콘솔 메뉴</br>
    - 메뉴를 통해 사용자가 원하는 기능 선택 가능

        - 1: 사칙연산 수행

        - 2: 원의 넓이 계산

        - 3: 프로그램 종료


    - 계산 이후 입력을 통해 추가 기능 실행

      - remove: 저장된 결과 중 첫 번째 삭제
  
      - inquiry: 전체 결과 조회

      - inquiryGreater: 기준값보다 큰 결과만 조회

      - exit: 프로그램 종료

```java
System.out.println("1.사칙 연산 2.원의 넓이 3.종료");
int choice = scanner.nextInt();
switch (choice) {
    case 1: // 사칙연산
    case 2: // 원의 넓이
    case 3: return; // 종료
}
```

 5. 견고한 예외 처리</br>
    - 나눗셈에서 0으로 나누는 경우

    - 음수 반지름 입력

    - 양의 정수 외 값 입력 등 다양한 예외 상황을 ArithmeticException으로 처리하여 안정적인 실행 보장

```java
if (b == 0) {
    throw new ArithmeticException("0으로 나눌 수 없습니다.");
}
if (radius < 0) {
    throw new ArithmeticException("반지름은 음수일 수 없습니다.");
}

```




## Trouble Shooting👾
[Level1Trouble-Shooting](https://winwin0219.tistory.com/entry/Java-Level1Trouble-Shooting)   </br>
[Level2Trouble-Shooting](https://winwin0219.tistory.com/entry/Java-Level2Trouble-Shooting)   </br>
[Level3Trouble-Shooting](https://winwin0219.tistory.com/entry/Java-Level3Trouble-Shooting)   



## 파일구조
```
onboarding-personal-calculator/
│
├── .gitignore                 # Git이 추적하지 않을 파일 목록 설정
├── README.md                  # 프로젝트 설명 문서
├── build.gradle               # Gradle 빌드 설정 파일
├── gradle/                    # Gradle 관련 내부 설정 폴더
├── gradlew                    # Gradle 실행 파일 (유닉스용)
├── gradlew.bat                # Gradle 실행 파일 (윈도우용)
├── settings.gradle            # 프로젝트 모듈 설정
│
└── src/
    └── main/
        └── java/
            └── calculator/
                ├── App.java                # 프로그램 실행 진입점 (메인 메뉴 및 흐름 제어)
                ├── Calculator.java         # 계산 결과 저장 및 공통 기능 제공 클래스
                ├── ArithmeticCalculator.java # 제네릭 기반 사칙연산 계산기
                ├── CircleCalculator.java   # 원의 넓이 계산 기능 클래스
                ├── Operator.java           # 연산자 인터페이스 (연산 규약 정의)
                ├── OperatorType.java       # 연산자 기호 enum 정의 (+, -, *, /, % 등)
                ├── AddOperator.java        # 덧셈 연산 구현 클래스
                ├── SubtractOperator.java   # 뺄셈 연산 구현 클래스
                ├── MultiplyOperator.java   # 곱셈 연산 구현 클래스
                ├── DivideOperator.java     # 나눗셈 연산 구현 클래스 (0 나눗셈 예외처리 포함)
                └── ModOperator.java        # 나머지(%) 연산 구현 클래스

```
