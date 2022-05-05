# Observer Pattern

## 옵저버 패턴 (Observer Pattern)
옵저버 패턴은 객체의 상태 변화를 관찰하는 관찰자들.   
즉, 옵저버들의 목록을 객체에 등록하여 상태 변화가 있을 때마다 메서드 등을 통해 객체가 직접 목록의 각 옵저버에게 통지하도록 하는 디자인 패턴이다.   
주로 분산 이벤트 핸들링 시스템을 구현하는 데 사용된다. 발행/구독 모델로 알려져 있기도하다.
-위키백과   
    
**Publisher**   
여러 개의 Observer를 가질 수 있습니다.   
Observer에게 상태의 변경을 알려주고 Observer를 추가하거나 제거하는 프로토콜을 제공합니다.   
     
**Concrete Publisher**   
구체 타입의 Observer 들을 속성으로 가지고 있습니다.   
상태가 변경 될 때마다 Observer에게 알리위해 Publisher의 상태를 저장하고 있습니다.   
   
**Observer(Subscriber)**   
Publisher의 변경 사항을 update 받는 프로토콜을 제공합니다.   
   
**Concrete Observer**   
Concrete Publisher의 상태가 변할 때 마다 이들에게 알려줍니다.   
Publisher의 속성이 어떻게 바뀌었는지 업데이트하는 메서드를 구현합니다.   
   
## 옵저버 패턴을 사용하면 좋을 때
다른 객체의 상태가 변경될 때마다 어떤 행동을 하고 싶다면 옵저버 패턴을 사용하면 된다.   
iOS에선 ViewController에 Observer(Subscriber)가 있고, Model에 Subject(Publisher)가 있는 MVC 패턴에서 사용할 수 있다.   
이를 통해 Model은 ViewController의 타입에 대해 알 필요 없이 상태가 변경될 때마다 이를 ViewController에 전달할 수 있다. 따라서 여러 개의 ViewController가 하나의 Model의 변경사항을 사용할 수 있게 된다.   
   
## 옵저버 패턴의 장단점
**장점**   
- subject의 코드를 수정하지 않고 새로운 옵저버를 추가할 수 있고, 그 반대도 가능하기에 OCP원칙을 지킬 수 있다.
- 런타임에서 객체간 관계를 설정할 수 있다.
   
**단점**   
- Observer에게 알림이 가는 순서는 보장하지 않는다.
- Observer, Subject 간의 관계가 정의가 제대로 되어있지 않다면 원치 않는 동작이 이루어짐.
   
## 옵저버 패턴 구현
Subject(Publisher) Interface   
``` swift
protocol Publisher {
    var observers: [Observer] { get set }
    func subscribe(observer: Observer)
    func unSubscribe(observer: Observer)
    func notify(message: String)
}
```
   
Observer(Subscriber) Interface
``` swift
protocol Observer {
    var id: String { get set }
    func update(message: String)
}

```
   
Concrete Subject(Publisher)
``` swift
class AppleStore: Publisher {
    var observers: [Observer]
    
    init(observers: [Observer]) {
        self.observers = observers
    }
    
    func subscribe(observer: Observer) {
        self.observers.append(observer)
    }
    
    func unSubscribe(observer: Observer) {
        if let index = self.observers.firstIndex(where: { $0.id == observer.id }) {
            self.observers.remove(at: index)
        }
    }
    
    func notify(message: String) {
        for observer in observers {
            observer.update(message: message)
        }
    }
}

```
   
Concrete Observer(Subscriber)
``` swift
class Customer: Observer {
    var id: String
    
    init(id: String) {
        self.id = id
    }
    
    func update(message: String) {
        print("\(id)님 \(message)수신\n")
    }
}
```
   
실행
``` swift
let : appleStore = AppleStore(observers : [])
let A = Customer(id : "A")
let B = Customer(id : "B")
let C = Customer(id : "C")

appleStore.subscribe(observer: A) // observers = [A]
appleStore.subscribe(observer: C) // observers = [A,C]

appleStore.notifi(message : "iPhone 입고") // A님 iPhone 입고 수신, C님 iPhone 입고 수신

appleStore.unsubscribe(observer: C) // observers = [A]
appleStore.notifi(message : "iPad 입고") // A님 iPad 입고 수신
```
   
   
참고
https://icksw.tistory.com/257?category=944177
