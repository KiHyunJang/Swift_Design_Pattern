# Singleton Pattern

## 싱글톤 패턴 (Singleton Pattern)
싱글턴 패턴을 따르는 클래스는, 생성자가 여러 차례 호출되더라도 실제로 생성되는 객체는 하나이고 최초 생성 이후에 호출된 생성자는 최초의 생성자가 생성한 객체를 리턴한다.   
   
싱글턴 패턴을 사용하게 되면 유일한 객체를 만들 수 있습니다. 싱글턴은 특정 클래스의 인스턴스가 오직 하나임을 보장하는 객체입니다.   
유일한 객체를 만든다는 말은 다양한 객체들이 모두 같은 인스턴스와 소통할 수 있다는 말입니다.   
   
싱글턴의 대안으로 인스턴스를 생성해서 각각의 객체들에게 의존성을 주입하는 방법도 생각해볼 수 있다. 그러나 싱글턴을 사용하면 하나보다 많은 인스턴스를 생성하는 것 자체를 방지할 수 있다.   
   
## 싱글톤 패턴은 언제 사용할까?
앱 전체에 걸쳐서 유일한 객체를 만들기위해 사용한다.   
어디에서나 전역으로 접근할 수 있는 유일한 객체인 셈이다.   
좀 더 풀어서 이야기하면 여러 개의 객체가 같은 객체로부터 동일한 상태의 정보를 받아와야할 때 사용할 수 있다. 예를 들면 사용자의 어떤 정보나 앱 전반에 걸쳐서 공유되어야 하는 데이터들이 그렇다. 우리가 자주 사용하는UserDefault나 NotificationCenter, URLSession등이 있다.   
   
## 싱글톤 패턴의 장점
- 싱글턴 패턴은 유일한 객체를 만들어서 다양한 객체들에게 공유되는 객체를 만들 수 있다는 장점이 있었습니다. 또한 재사용이 가능하여 메모리 낭비를 방지할 수 있다는 장점도 있다.
   
## 싱글톤 패턴의 단점
- 싱글턴 패턴은 객체지향 관점에서 본다면 인스턴스들 간에 결합도가 높아져서 OCP(개방-폐쇄 원칙, Open-Closed Principle) 을 위배하게 된다는 단점이 있어서, 싱글턴 패턴은 웬만하면 지양해야한다.
   
## 싱글톤과 구조체
구조체로도 구현이 가능하나 일반적으로 클래스를 사용하는 이유는 싱글턴의 목적인 유일한 객체를 사용하기 위해서이다.
구조체를 사용하면 주소값이 달라 유일한 객체가 아니게된다.   
   
## 싱글턴 패턴 예제
은행을 예제로 싱글턴 패턴을 구현해보았다.   
   
Singleton
``` swift
enum Bank {
    case ShinhanBank
    case NonghyupBank
    case KookminBank
}

// Singleton
class BankMoney {
    static let shared = BankMoney()
    private var ShinhanBankMoney = 100000000
    private var NonghyupBankMoney = 100
    private var KookminBankMoney = 20000000
    
    private init() { }
    
    //인출
    public func withdrawMoney(_ bank : Bank, money : Int) {
        switch bank {
        case .ShinhanBank:
            ShinhanBankMoney = max(ShinhanBankMoney - money, 0)
        case .NonghyupBank:
            NonghyupBankMoney = max(NonghyupBankMoney - money, 0)
        case .KookminBank:
            KookminBankMoney = max(KookminBankMoney - money, 0)
        }
    }
    
    //입금
    public func depositMoney(_ bank : Bank, money : Int) {
        switch bank {
        case .ShinhanBank:
            ShinhanBankMoney += money
        case .NonghyupBank:
            NonghyupBankMoney += money
        case .KookminBank:
            KookminBankMoney += money
        }
    }
    
    // 예금 확인
    public func checkBankMoney(_ bank : Bank) {
        switch bank {
        case .ShinhanBank:
            print(ShinhanBankMoney)
        case .NonghyupBank:
            print(NonghyupBankMoney)
        case .KookminBank:
            print(KookminBankMoney)
        }
    }
}
```
   
실행
``` swift
BankMoney.shared.checkBankMoney(.KookminBank) // 20000000
BankMoney.shared.depositMoney(.KookminBank, money: 10000)
BankMoney.shared.checkBankMoney(.KookminBank) // 20010000
BankMoney.shared.withdrawMoney(.KookminBank, money: 10000000000)
BankMoney.shared.checkBankMoney(.KookminBank) // 0
```
