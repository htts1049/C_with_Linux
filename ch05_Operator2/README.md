# 비트 연산 활용
<br></br>
___
## 비트 연산이 중요한 이유

![image](https://user-images.githubusercontent.com/130421694/236799124-e9512c75-395f-4768-a54a-68ba6ae7ad0f.png)

* 임베디드 개발에서 GPIO 를 제어하려면 특정 메모리의 비트 값을 바꿔야 하기 때문


<br></br>
<br></br>

![image](https://user-images.githubusercontent.com/130421694/236797510-25f2e1dc-15a0-4dfc-9f8f-87693b634327.png)   

* a라는 메모리의 2진수 값 = 0011 0000 
	+ 5,6 번째 전구가 켜진 것


<br></br>
<br></br>
![image](https://user-images.githubusercontent.com/130421694/236797797-e0a27c23-5ef7-4e0f-a371-7b6c2ac29c52.png)   

* 3번째 전구를 켜기 위해서는 3번째 비트 값만 1로 만들어 줘야함
	+ 0011 0000 → 0011 0100
<br></br>
<br></br>

![image](https://user-images.githubusercontent.com/130421694/236798098-59054775-3c51-44db-915c-1b1fc4d4c0de.png)

* 반대로 5번째 전구를 끄기 위해서는 5번째 비트 값만 0으로 만들어 줘야함
	+ 0011 0000 → 0010 0000


<br></br>
<br></br>
___
## 비트 마스킹
* 원하는 비트만 0 또는 1로 바꾸기 위한 방법


<br></br>
<br></br>

### 1. 비트 값 1로 바꾸기

![image](https://user-images.githubusercontent.com/130421694/236798576-34cda965-77eb-455e-a74f-5e7a60f159ef.png)   

* | 연산 활용
* 1을 왼쪽으로 비트 시프트연산 한 숫자와 | 연산
* 다른 비트는 0과 | 연산하기 때문에 __기존의 갖고 있던 비트 값이 그대로 전달__
	+ 1 | 0 = 1
	+ 0 | 0 = 0
* 해당 비트만 1과 | 연산하기 때문에 __기존에 어떤 값이 있든 1이 됨__
	+ 1 | 1 = 1
	+ 0 | 1 = 1
<br></br>
<br></br>

### 2. 비트 값 0으로 바꾸기

![image](https://user-images.githubusercontent.com/130421694/236798853-75a4cf59-2ae9-49d1-ab16-3c491ea64275.png)

* & 연산 활용
* 1을 왼쪽으로 비트 시프트 연산 한 후 ~연산한 숫자와 & 연산
* 다른 비트는 0과 & 연산하기 때문에 __기존에 어떤 값이 있든 0이 됨__
	+ 1 & 0 = 0
	+ 0 & 0 = 0
* 해당 비트만 1과 & 연산하기 때문에 __기존의 갖고 있던 값이 그대로 전달__
	+ 1 & 1 = 1
	+ 0 & 1 = 0
<br></br>
<br></br>
___
## 비트 마스킹 실습

![image](https://user-images.githubusercontent.com/130421694/236799385-79417f3d-8674-407e-9796-07ca909b4dd9.png)

* printBinary 함수 : char 형 변수 x를 받아서 8bit의 2진수로 출력
* a에 48을 대입하고 3번째 비트만 1로 변환
* b에 48을 대입하고 5번째 비트만 0으로 변환
<br></br>
<br></br>

![image](https://user-images.githubusercontent.com/130421694/236799811-571bd385-4648-40e3-90d3-6d9a4cd72567.png)

* 컴파일 후 실행
* 원하는 대로 비트 값이 바뀐 것을 확인
<br></br>
<br></br>
___
# 삼항 연산
* 삼항 연산은 조건 연산이라고도 불리며, if-else 문과 같이 동작
* a ? b : c
  + a가 참이면 b, a가 거짓이면 c 실행
<br></br>
<br></br>
___
## 삼항 연산 실습

![image](https://user-images.githubusercontent.com/130421694/236837999-b36dba04-7aba-406f-a622-2232f89f8a69.png)

* 간단한 조건문 대신 많이 사용됨
* __삼항 연산은 isRunning() 과 같은 함수와 함께 많이 사용됨__


<br></br>
<br></br>

![image](https://user-images.githubusercontent.com/130421694/236838403-ea03b88e-3b60-4dc5-b063-d5f11ed0d42c.png)


* ? 앞이 0이면 false, 그 외에는 어떤 값이 오더라도 true



<br></br>
<br></br>
___
# 형 변환 연산자
* 형이 다른 변수끼리 계산하면 자동으로 형 변환이 일어남
* 이것은 원하는 결과가 나오지 않는 원인이 되기도 함
* __형이 다른 변수끼리 계산할 때에는 형 변환 연산자를 쓰는 것이 안전__
<br></br>
<br></br>
___
## 형 변환 실습

![image](https://user-images.githubusercontent.com/130421694/236841722-34f15f25-510b-4e1a-aaa9-c20fbe3bfff8.png)

* 형 변환을 하기 원하는 변수 앞에 괄호와 자료형을 써주면 됨


<br></br>
<br></br>

![image](https://user-images.githubusercontent.com/130421694/236841894-6f0d2e0a-ca79-495c-965c-045b635524e9.png)

* 자료형으로 인한 오류가 발생할 수 있다고 컴파일러가 경고해줌
* 2번째 줄과 마지막 줄을 보면 값이 이상하게 나온 것을 확인
* 2번째 줄 : int 형인 i가 실수형인 float으로 형변환되었지만 출력을 정수형으로 했기 때문에 이상한 값이 출력
* 마지막 줄 : 500 = 1 1111 0100 (2) 이고, 이것을 1byte인 char 형으로 형변환 하면 하위 8bit만 남게 된다   
              → 1111 0100 (2) 를 출력하게 되고, 이것을 unsigned char 로 변환하면 10진수로 244가 출력


