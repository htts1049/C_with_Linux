# 1. Data Type
* 자료형의 종류와 크기는 일반적으로 다음과 같다
<br></br>
![image_3](https://user-images.githubusercontent.com/130421694/232484852-51af004f-2089-4eec-b061-b5dac921cff8.png)
<br></br>
* 그런데 여기서 의문이 생긴다
* 왜 char은 1byte이고, 나머지 자료형들은 크기가 2배씩 늘어날까?
<br></br>
<br></br>
___
## 1-1. char
* 먼저 아스키 코드 표와 함께 char 자료형 부터 살펴보자
<br></br>
<br></br>
![image_4](https://user-images.githubusercontent.com/130421694/232484848-bf8f9fcf-633e-412d-975a-a5165f509ae3.png)
<br></br>
* 1byte = 8bit 이고, 2^8 = 256 이므로 1byte 로는 00000000 ~ 11111111 까지의 256가지의 표현이 가능하다
* 아스키 코드 표에서 보이듯 128가지만으로도 충분히 표현이 가능하기 때문에 char 자료형은 1byte의 크기를 갖는다
<br></br>
<br></br>
___
## 1-2. int, long, ...
* 다음으로 char 를 제외한 다른 자료형의 크기가 왜 2배씩 늘어나는지 생각해보자
* 먼저 CPU는 메모리를 병렬로 처리하면 속도가 빠르며 이를 병렬 컴퓨팅이라고 한다
![image_10](https://user-images.githubusercontent.com/130421694/232489642-8da6842e-c123-411f-b67f-a71d351de56f.png)
<br></br>
* 추측일 뿐이지만 자료형 크기가 2배씩 늘어나는 이유는 이것 때문으로 보인다
* 어떤 프로그래머가 3비트 컴퓨터에서 작동하던 프로그램을 5비트 컴퓨터로 옮긴다고 생각해보자
* 이 때 5비트 컴퓨터에서 3비트를 차지하는 프로그램을 실행 중이라면, 나머지 2비트로 뭘 할수 있을까?
* 남은 2비트로는 3비트짜리 프로그램을 실행할 수도 없고 프로그램을 옮기는 작업이 어렵다고 한다
<br></br>
* 하지만 2비트에서 4비트로 옮기는 건 비트가 남을 일도 없고 비트 자리만 옮겨주면 되기에 호환이 쉽다
* 예를들면 64비트에서 32비트 프로그램을 쓰는건 쉽다 → 나머지 반 32비트를 그냥 안쓰면 된다
<br></br>
* 요약하자면 다음과 같은 이유들로 인해서 자료형의 크기가 2배씩 늘어난 것으로 보인다
  1. 병렬 컴퓨팅으로 인한 속도 향상
  2. 기존에 작업한 프로그램을 더 많은 비트의 컴퓨터로 옮길 때 편리함
  3. 호환이 잘 됨
<br></br>
<br></br>
___
# 2. 실습
___
## 2-1. 일반적인 값 출력
![image_6](https://user-images.githubusercontent.com/130421694/232484896-9e5f17e9-f8a4-4ba4-9e12-f0fce4483c5e.png)
* 자료형에 따라 포맷을 다르게 하여 printf 함수를 실행한다
  + 여담으로 printf 함수는 엄연히 c언어 문법이 아니며, 입출력 포맷은 c언어를 만든 사람이 지정한 형식이다
<br></br>
* unsigned 는 부호가 없는 정수를 뜻한다
  + 컴퓨터는 원래 맨 앞 비트가 1이면 음수로 인식하지만 unsigned 로 지정한 수는 양수로 인식한다
  + 음수가 차지하던 값을 양수로 사용하여 2배 넓은 범위의 양수를 사용할 수 있다
<br></br>
<br></br>
![image_5](https://user-images.githubusercontent.com/130421694/232484893-3855e2cc-0e5a-4eab-87be-2a72bd4bb3f1.png)
* 대입한 값에 맞게 출력이 잘 된다
<br></br>
<br></br>
___
## 2-2. 2진수로 출력
![image_8](https://user-images.githubusercontent.com/130421694/232484904-17cd385b-e330-40ab-82ab-7c9de9082b80.png)
* 입력받은 숫자를 2진수로 출력하는 함수를 작성했다
<br></br>
![image_9](https://user-images.githubusercontent.com/130421694/232484907-a55c5424-24bd-4560-8976-132079a9b38c.png)
<br></br>
![image_7](https://user-images.githubusercontent.com/130421694/232484901-05d3f326-6eeb-42ce-9922-05251e49c47c.png)
* int
  + int에서 출력할 수 있는 최대 양수는 2,147,483,647 로 2,147,483,648을 출력하자 최상위 비트가 1이 되어 음수로 판단해 출력한다
  + unsigned int 에서는 범위를 벗어나지 않으므로 그대로 출력한다
<br></br>

* char
  + '8'과 's' 모두 아스키 코드 값에 맞게 출력되었다
<br></br>

* short
  + short의 출력 범위는 -32,768 ~ 32,767 로 음수인 s는 그대로 출력한다
  + unsigned 에서는 최상위 비트가 1이어도 양수로 판단하므로 양수로 변환되어 출력된다
<br></br>

* long
  + long은 원래 4byte로 알고있었고 위 표에서도 4byte라고 표기되어 있었는데, printf로 확인해보니 8byte 였다
  + 검색해보니 운영체제나 프로그램에 따라 다른 듯 하다
<br></br>

![image_11](https://user-images.githubusercontent.com/130421694/232502092-f0df4600-b74c-4ed0-9c31-cf301655e185.png)
* float, dobule
  + 컴퓨터는 실수를 비트를 지수부, 가수부로 구분지어 판단한다
  + float과 double에 같은 3.14를 대입해도 2진수 값이 다른 것은 이 때문이다
  + 지수부, 가수부로 나누기 때문에 계산이 정수형보다 느리다는 점만 짚고 넘어가자
<br></br>
<br></br>
___
### 참고
##### <a href= "https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=angelcorean&logNo=220804837093&view=img_5"> <h3> ㆍ 자료형 크기 </h3> </a>
##### <a href= "https://blog.naver.com/PostView.naver?blogId=with_msip&logNo=222439390237&redirect=Dlog&widgetTypeCall=true&directAccess=false"> <h3> ㆍ 병렬 컴퓨팅 </h3> </a>
##### <a href= "https://stepbystep1.tistory.com/10"> <h3> ㆍ 아스키 코드 </h3> </a>
##### <a href= "https://nasanx2001.tistory.com/entry/8-%EA%B0%80%EC%88%98%EB%B6%80%EC%99%80-%EC%A7%80%EC%88%98%EB%B6%80"> <h3> ㆍ 실수형 </h3> </a>
