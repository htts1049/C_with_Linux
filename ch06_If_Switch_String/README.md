

## scanf 함수란?

* stdio.h 헤더파일에 포함된 표준 입력 함수
* 컴파일러가 다르더라도 최소한 이 함수는 구현을 해준다고 보면 됨
* 윈도우든 리눅스든 stdio.h 를 불러와서 scanf 함수를 쓰는 것은 C언어의 표준이 되었기 때문에 똑같은 결과를 낳는다고 보면 됨
  
<br></br>

![image](https://github.com/htts1049/C_with_Linux/assets/130421694/46483cf1-8ec4-4ec0-8953-1eaaac31784a)

* scanf 함수는 입력받고자 하는 변수의 주소 값을 인자로 받는다

<br></br>

![image](https://github.com/htts1049/C_with_Linux/assets/130421694/a0286bf6-b463-4c5a-a8a2-3aaa4dff6d2f)

* 입출력 포맷은 printf 함수와 동일하다
* 입력받을 변수인 a를 초기화해주지 않으면 잘못된 값이 나올 수 있다

<br></br>
<br></br>
___
## if문

![image](https://github.com/htts1049/C_with_Linux/assets/130421694/5bae11b9-36b4-4fe6-971a-3a907a92f689)

* if문을 배열할 때 가장 참일 확률이 높은 걸 맨 위로 올려주면 밑에 있는 것들을 실행안하니까 프로그램적으로 더 좋다
* if 문은 중괄호를 쓰지 않아도 문장 1개까지는 쓸 수 있지만, 보기 힘들기 때문에 꼭 중괄호를 써주자
* 마찬가지로 들여쓰기를 하지 않으면 보기 힘들다

<br></br>

![image](https://github.com/htts1049/C_with_Linux/assets/130421694/af34cb68-e4ce-4c4c-9019-7fbfe913ef6d)

* else 문 내부의 else if 문에서 isGood() 함수가 1을 반환하므로 조건문이 참이 되어 "Good!\n" 문장을 실행

<br></br>
### vi 에디터 들여쓰기
* v를 누르면 비주얼 모드가 됨
* 비주얼 모드인 상태에서 들여쓰기 혹은 내어쓰기하고 싶은 라인을 지정
* 그 상태에서 shift + > 하면 들여쓰기, shift + < 하면 내어쓰기 가능

<br></br>
<br></br>
___
## switch문

![image](https://github.com/htts1049/C_with_Linux/assets/130421694/e957ac38-b7a8-4654-adc0-9c6f4980d5da)

* 입력한 값에 따라 출력 값이 바뀌는 코드

<br></br>

![image](https://github.com/htts1049/C_with_Linux/assets/130421694/4eaacf4c-cbe4-4574-9963-3952a509dadd)

* 3을 입력하면 3이 출력

<br></br>

![image](https://github.com/htts1049/C_with_Linux/assets/130421694/900d95d7-7eb0-4038-bc32-4175ca5e42e4)

* break 가 없으면 다음 case 문으로 넘어감
* 1을 입력했지만 break가 없어서 case 2로 넘어간 상황
* 오히려 의도적으로 사용할 수도 있음

<br></br>

![image](https://github.com/htts1049/C_with_Linux/assets/130421694/4b754c0f-24e9-44b6-9ac0-c52ceeac82ba)

* 모든 case에 해당하지 않으면 default로 넘어감

<br></br>
<br></br>
___
## 문자열 개념

![image](https://github.com/htts1049/C_with_Linux/assets/130421694/f31fb5ee-a410-401c-be46-c0d45b297641)

* 문자열은 문자의 배열과 같다
* 문자열의 입출력 포맷은 %s이고, 문자의 입출력 포맷은 %c 이다

<br></br>

![image](https://github.com/htts1049/C_with_Linux/assets/130421694/f18ee0cb-4cd4-4f3e-b2c8-a956e66de149)

* 두 출력의 결과는 같지만 분명히 다른 코드이다

<br></br>

![image](https://github.com/htts1049/C_with_Linux/assets/130421694/74720466-9ee9-405a-ad33-13e579998ef6)

* 문자열은 첫 원소의 주소만 무작위이고, 그 뒤로는 순서대로 할당된 __배열__ 이다
* 문자를 일일히 출력한 것은 각 문자의 주소가 모두 무작위이고, 각각의 데이터가 붙어있지도 않을 확률이 높다
