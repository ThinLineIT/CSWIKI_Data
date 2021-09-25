# Encapsulation(캡슐화)
## 목차
- Encapsulation 개념
- Encapsulation 방법 및 코드예시

## You can answer
- Encapsulation은 무엇인가요?
- Encapsulation을 사용하는 이유가 뭔가요?
- Encapsulation을 어떻게 사용하나요?
- 은닉화와의 차이는 무엇인가요?

---
## Encapsulation 개념
### Encapsulation(캡슐화) 이란??!
- OOP에서 캡슐화는
객체의 속성(data fields)과 행위(메서드, methods)를 __하나로 묶고__,
실제 구현 내용 일부를 외부에 감추어 정보를 __은닉__ 한다.   [위키백과]

쉽게말해서 우리가 흔히 알고있는 캡슐약 처럼 관련된 질병에 관한 약들(속성,메소드)을 모아서 캡슐의 형태로 보호(정보은닉)하는 개념이다.

<img src = "img/capsule.jpeg" width = "50%"/>


### 캡슐화 예시
예시로 한번 알아보자!!

은행에서 사용하는 ATM 클래스가 있다고 하자!

<img src = "img/ATM_Class.png" width = "70%"/>

- 그림처럼 클래스에 속성과 행위(메소드)를 묶어준다.
- 만약 외부에서 고객정보를 확인할 수 있게 된다면 보안상의 큰 문제가 될 수 있으니 고객의 정보를 은닉해야한다!
- ATM 버전 정보는 외부에서도 접근하여 정보를 보거나 수정하는것은 문제가 되지 않기 때문에 은닉하지 않아도 된다!(원하는 버전정보를 선택할 시)



## Encapsulation 방법 및 코드예시

### 방법
- 속성에 맞는 접근 제한자를 설정해 준다.

    __private__ : 동일한 클래스 안에서만 접근이 가능하고, this를 사용하는 것들은 외부에서 접근 불가능하고, 상속도 안된다.

    __default__ : 접근제어자가 없는 형태로 동일한 패키지 안에서만 접근이 가능하다.

    __protected__ : 동일한 패키지 안에서 사용가능하고, 다른 패키지라도 상속받은 클래스에는 접근이 가능하다.

    __public__: 모든 객체에서 접근 가능하다.
    - 해당 클래스에 들어가야하는 속성과 메소드를 잘 구분하여 묶어준다.



### 코드 예시(java)
#### ATM Class
``` java
class ATM{

	//ATM Attribute(속성).
	private int totalMoney = 100000; //금액의 정보는 외부로부터 은닉되어야 한다.
	private String clientName; //고객의 이름정보는 외부로부터 은닉되어야 한다.
	private String AccountNum = ""; //고객의 계좌번호는 외부로부터 은닉되어야 한다.
	public String ver = "2.0.1"; //버전정보는 외부로부터 은닉되지 않아도 된다.
	private boolean stateOfATM;

	//ATM 디폴트 생성자.
	ATM(){
        //통장이 들어와 있지 않음을 표시.
		stateOfATM = true;
	}

	//ATM통장번호와 이름이 입력되는 생성자.
	ATM(String name, String account){
		this.clientName = name;
		this.AccountNum = account;
        System.out.println("어서오십시요 "+ clientName + " 고객님!");
	}

    //ATM Method(메소드)

	//현재 ATM기기에 통장이 들어와 있는지를 확인하는 메소드.
	public boolean isEmpty() {
		if(AccountNum.equals("")) {
			stateOfATM = true;
		}else {
			stateOfATM = false;
		}
		return stateOfATM;
	}


	//ATM 버전 확인 메소드.
	public void version() {
		System.out.println("현재 버전은 " + ver + "입니다.");
	}

	//통장정리 메소드.
	public void plusMoney(int money) {
		System.out.println("입급 금액(원) : " + money);
		this.totalMoney += money;
	}

	public void minusMoney(int money) {
		System.out.println("출금 금액(원) : " + money);
		this.totalMoney -= money;
	}

	public void showMoney() {
		System.out.println("현재 계좌의 잔액은 : "+ totalMoney + "(원)입니다.");
	}
}

```

#### Main Code
``` java

public class Encapsulation {

	public static void main(String[] args) {
		ATM client = new ATM("HongGilDong","352-xxxx-xxx-xx");

		if(client.isEmpty()) {
			System.out.println("통장이 들어오지 않았습니다!");
			return ;
		}

		else {
			System.out.println("통장이 들어왔습니다!");
		}

		client.showMoney();

		//입금.
		//client.totalMoney += 1500000; //고객이 총 금액의 변수를 접근할 수 없다!!(정보 은닉때문!!)
		client.plusMoney(1500000); //메소드로 접근해야 한다!!
		client.showMoney();

		//출금.
		client.minusMoney(500000);
		client.showMoney();

		//ATM 버전 확인.
		client.version();

        //버전정보를 바꿔서 이용.
		client.ver = "3.0.1";
		client.version();
	}

}

```

[결과화면]

<img src = "img/Encapsulation_Result.png" width = "80%"/>

## BONUS
### Q : 은닉화와 캡슐화의 개념이 비슷한거 같은데 차이가 무엇인가요??!!

- __캡슐화__

실제로 구현되는 부분을 외부에 드러나지 않도록 캡슐로 감싸 이용방법만을 알려주는것. 변수와 함수를 하나로 묶는것을 의미한다. 외부에서 직접적인 접근을 하면 안되고 오로지 함수를 통해서만 접근해야 한다!

[캡슐화 예시]
오므라이스에 필요한 재료가 계란,밥,소금,소스 이다.
오므라이스를 만들기 위해 필요한 공간(클래스)을 마련하고 재료들을 한곳에 모아두어야(캡슐화) 요리하기 편리하다. 또한 오므라이스를 만들기 위해 필요한 과정(메소드)들을 통해 오므라이스를 만들 수 있다.
여기서 고객이 요리하는 과정을 볼 필요가 있는가? 밥을 더 먹고 싶다고 직접 밥을 더 담는가? 그러면 안된다! 직원(메소드)를 통해 추가로 밥을 주문해야한다!
- 은닉화

캡슐화에 비해 비교적 구체적인 개념. 은닉화는 객체 외부에서 내부의 데이터나 메소드에 접근을 제한하고 데이터를 수정, 조작하는 동작은 내부에 두고 접근(getter), 설정(setter) 하는 메소드로 __결과만__ 받는것 이다.

[은닉화 예시]
고객에 메뉴판에서 오므라이스를 주문할 경우 요리과정을 굳이 보여주지 않아도 된다. 또한 어떤 계란을 선택할 지 고객이 참여하게 되면 난감한 상황이 벌어지기 때문에 고객은 주문(요청값)만 하고 요리(내부의 함수)해서 나온 오므라이스(결과값)를 맛있게 먹으면 된다!

---
## Reference
- [Encapsulation 정의](https://ko.wikipedia.org/wiki/%EC%BA%A1%EC%8A%90%ED%99%94)
- [Encapsulation 예시](https://javacpro.tistory.com/31)
