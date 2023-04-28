# gdb 디버거와 상수
<br></br>
___
## gdb 디버거를 사용할 줄 알아야 하는 이유
<br></br>
### 프로그램도 프로그램으로 만든다
###### <a href= "https://inpages.tistory.com/157"> <h3> 전처리과정 </h3> </a>
![image](https://user-images.githubusercontent.com/130421694/235079424-ca543402-b441-4252-8b1b-122cb7e524de.png)
<br></br>
* 개발하다보면 일반적인 컴파일러가 아니고 크로스컴파일 하는 경우가 있음

* CPU에 처음 어떤 프로그램이나 코드를 올리려면 어셈블리어를 만들어야 함

* 어셈블리어로 C 컴파일러를 만들고 C로는 다시 리눅스 운영체제를 만듬

* 리눅스 운영체제를 가지고 이제 GCC 컴파일러를 만든다

* 이렇게 만든 GCC 컴파일러를 가지고 Hello World 같은 무궁무진한 main 함수 작성
  → 이런 프로그램들은 모두 리눅스 운영체제 상에서 동작

* 임베디드용 CPU ARM칩에서 동작하는 프로그램을 만들려면 그 전용 컴파일러가 있어야한다

* 근데 IoT 기기 같은 임베디드 기기는 컴파일러를 실행할 수 없음   
  → ex) 모니터에서 gcc를 돌릴 수는 없음   
  → 그래서 필요한 것이 크로스 컴파일이고, 크로스 컴파일을 할 때 gdb를 사용하는 경우가 있다
<br></br>
<br></br>
___
### 크로스 컴파일
###### <a href= "https://haneepark.github.io/2018/09/15/what-is-cross-compile/"> <h3> 크로스 컴파일 </h3> </a>
<br></br>
![image](https://user-images.githubusercontent.com/130421694/235083941-103d530b-cb7b-4156-ac9b-8ac030a56be5.png)

* 만약 내가 CPU에서 어떤 A-GCC라는 프로그램을 만들었다면    
  A-GCC 라는 크로스 컴파일러는 C라는 코드를 짰을 때 기계어로 변환해주는 프로그램

* C라는 코드가 어디서 동작하는 기계어인가 하면, B라는 CPU에서 동작하는 기계어를 만들어주는 프로그램

* 정리하자면 A-GCC는 A에서 동작은 하지만 C라는 코드를 컴파일하면 컴파일한 코드는 B라는 CPU에서 동작하게 된다

* 근데 굳이 B에서 동작하는 프로그램을 A에서 만들어야 하나?   
  → 자원이 많이 들기 때문이다   
  → 라즈베리파이 같이 CPU가 임베디드 용이라고 하기에 다소 큰 CPU라면 운영체제를 설치해서 프로그램을 만들 수 있다   
  → 하지만 일반적으로 임베디드 용이라면 CPU 자원이 한정적이기 때문에 다른 기계에서 크로스 컴파일하는 것이 더 효율적이다   
      ex) 일반 PC에서 안드로이드 스튜디오로 만든 apk 파일을 스마트폰에 다운로드 
<br></br>
<br></br>
___
## gdb 사용법
* gdb가 깔려있지 않다면 vi, gcc와 같이 apt-get install gdb 로 먼저 다운을 받자
<br></br>
###### <a href= "https://mk28.tistory.com/134"> <h3> gdb 더 자세히 알기 </h3> </a>
<br></br>

___
### 디버깅 시작
![image](https://user-images.githubusercontent.com/130421694/235089166-4ca7fb28-45cd-4021-a0ae-b52fa7f66ec4.png)
* 디버깅을 하기 위해서는 디버깅에 필요한 정보를 컴파일하면서 담아줘야 한다   
  → gcc -g filename.c
* 디버깅 창을 연다   
  → gdb a.out
<br></br>
___
### 디버깅
![image](https://user-images.githubusercontent.com/130421694/235090361-f9bee998-b0d5-460f-be4c-be5c2c94d4e3.png)   
* 디버깅 창에서 run 입력시 코드 실행
<br></br>

![image](https://user-images.githubusercontent.com/130421694/235090732-1a8593f9-1c4f-4abb-8676-114f581ea59e.png)   
* l 입력시 코드 출력   
<br></br>

![image](https://user-images.githubusercontent.com/130421694/235091120-0f2165ac-c571-4092-a955-f4104e9a3faf.png)   
* (l 숫자) 입력시 숫자에 해당하는 라인 기준으로 출력
<br></br>

![image](https://user-images.githubusercontent.com/130421694/235091889-46949f57-f09a-4aed-a843-9b130f965a81.png)
* (b 숫자) 라인에 breakpoint 설정
  → breakpoint 잡고 run 하면 브레이크 잡힘
* 이 상태에서 변수 정보 보기 = p
<br></br>

![image](https://user-images.githubusercontent.com/130421694/235093894-23af4206-0414-4ba7-bf64-7916fa3b6083.png)
* disas main 입력시 main 함수에 관련된 어셈블리 단 출력
* 컴파일러는 변수를 선언하면 우리가 모르는 랜덤한 메모리 번지에 값을 넣고 저장
* 어셈블리에서는 실제 이 메모리 주소를 기억하고 저장하고 빼야한다
* 어셈블리에 대해서는 이런 것이 있다는 것만 짚고 넘어가자
<br></br>
* c언어의 장점은 메모리 주소를 기억하지 않고 우리가 변수명을 지정해서 쓸 수 있다는 것이다
* 이런 변수명을 지정을 못하면 0x34, 0x35 이런 식으로 써야함
<br></br>
<br></br>
___
## 상수
###### <a href= "https://jinshine.github.io/2018/05/17/%EC%BB%B4%ED%93%A8%ED%84%B0%20%EA%B8%B0%EC%B4%88/%EB%A9%94%EB%AA%A8%EB%A6%AC%EA%B5%AC%EC%A1%B0/#stack"> <h3> 메모리 구조 </h3> </a>
* 상수는 변수가 저장되는 데이터 영역이 아니라 코드 영역에 저장된다
<br></br>

### 상수의 메모리 위치
![image](https://user-images.githubusercontent.com/130421694/235096097-24f66d73-8e48-4056-9214-357cdddb14d8.png)

* 물리적인 하드디스크의 저장 공간에 a.out과 같은 실행파일이 저장되어 있다
* 이처럼 메모리 안에는 바이너리로 저장된 여러가지 정보가 있다
* 메모리 구조는 코드영역, 데이터영역, 힙영역, 스택영역의 4가지 영역으로 구분된다
* 이 중 상수는 코드영역에 저장되고 변수처럼 값 변경이 불가능하다
<br></br>
<br></br>
___
## 변수명 규칙
* 컴파일러 입장에서 생각해보면 상식적
<br></br>

1. 숫자로 시작 불가능
* 앞에 숫자로 시작하면 상수로 착각 가능
* 변수 이름이 3asdasd 라고하면 컴파일러 입장에서 변수인지 상수인지 구분 불가
* 코드를 전부 읽은 뒤에 구분이 가능하며, 너무 복잡하고 비효율적이다
<br></br>

2. 키워드 불가능
* if, switch, for 같은 키워드는 변수명 불가능
* 위와 마찬가지
<br></br>

3. 연산자 불가능
* 위와 마찬가지
<br></br>
<br></br>
___
## sizeof 연산자
* 자료형 크기 반환

### sizeof 연산자의 중요성
* 보통 int가 4바이트지만, 임베디드 쪽에서는 아직도 int가 4바이트가 아닌 경우가 있다
* 메모리 복사나 초기화를 사용할 경우와 같이 배열이나 구조체의 크기를 구할 필요가 있을때 숫자로 쓰는 것보다 확실하게 sizeof 를 쓰자
<br></br>
<br></br>
___
## const 변수
* const 변수는 값을 못바꾸는건 상수와 같지만 데이터 영역에 저장된다는 점이 다르다
* 쓰임새 : 여러 변수에 const 변수 값을 넣어 두고 const 변수 값만 바꿔서 사용 가능   
![image](https://user-images.githubusercontent.com/130421694/235101862-9f6b3f93-beb9-49c3-b92b-072f7f19eb5e.png)
* ex) 고양이, 개, 사람 등의 눈 개수를 2라고 저장하려고 할 때, 눈의 개수를 const int eyeNum = 2 라고 해둔뒤 각 변수들에 저장
* 만약 눈의 개수가 바뀌었다? eyeNum 만 바꾸면 됨
* define 문을 이용해도 무방
<br></br>
<br></br>
___
## const와 define (매크로 상수)의 차이
* const 는 메모리 공간의 코드 영역에 저장되므로 값 변경이 불가능하다
* 보통 const가 더 좋다, define이 더 좋을 때도 있다
<br></br>
* define은 컴파일이 될 때 전처리기가 변수를 모두 바꾼다음에 컴파일하고 define 문은 사라짐
* 문자열 치환의 개념
* 메모리 공간 절약
