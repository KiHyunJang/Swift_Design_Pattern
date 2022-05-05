# Abstract Factory Method Pattern

## 추상 팩토리 메서드 패턴 (Abstract Factory Method Pattern)
추상 팩토리 패턴의 목적은 구체적인 클래스를 지정하지 않고 관련된 객체들을 모으기 위한 인터페이스를 제공하는 것입니다. 또한 코드를 변경하지 않고도 조건에 따른 적절한 객체를 사용할 수 있게 해줍니다.   
추상 팩토리 패턴은 기존의 팩토리를 한번 더 추상화하여 서로 관련이 있는 제품군을 생성하게 해준다.   
   
**AbstractFactory** : 개념적 제품에 대한 객체를 생성하는 오퍼레이션으로 인터페이스를 정의한다.   
**ConcreateFactory** : 구체적인 제품에 대한 객체를 생성하는 오퍼레이션을 구현한다.   
**AbstractProduct** : 개념적 제품 객체에 대한 인터페이스를 정의한다.   
**ConcreateProduct** : 구체적으로 팩토리가 생성할 객체를 정의하고, AbstractProduct 가
정의하고 있는 인터페이스를 구현한다.   
**Client** : AbstractFactory 와 AbstractProduct 클래스에 선언된 인터페이스를 사용한다.   
   
## 추상 팩토리 메서드 패턴은 언제 사용할까?
생성을 책임지는 구체적인 클래스를 분리시키고 싶을 때 사용한다.   
- 추상 팩토리 패턴은 인스턴스를 생성하는 과정을 캡슐화 한 것입니다. 따라서 생성에 관한 구체적인 내용이 사용자와 분리됩니다.
여러 제품군중 선택을 통하여 시스템을 구성하고 제품군을 대체하고 싶을 때
- 구체 팩토리를 추가하거나 변경을 통해 서로 다른 제품을 사용할 수 있게 할 수 있습니다. 추상 팩토리는 필요한 모든 것을 생성하기 때문에 전체 제품군은 한 번에 변경이 가능합니다.
   
## 추상 팩토리 메서드 패턴 예제
야곰 디자인 패턴 강의에서 제공하는 예제가 좋길래 예제를 가져왔다.
   
AbstractFactory
``` swift
protocol UIFactoryalbe {
    func createButton() -> Buttonalbe
    func createLabel() -> Labelable
}
```
   
ConcreateFactory
``` swift
final class iPadUIFactoy: UIFactoryalbe {
    func createButton() -> Buttonalbe {
        return IPadButton()
    }

    func createLabel() -> Labelable {
        return IPadLabel()
    }
}

final class iPhoneUIFactory: UIFactoryalbe {
    func createButton() -> Buttonalbe {
        return IPhoneButton()
    }

    func createLabel() -> Labelable {
        return IPhoneLabel()
    }
}
```
   
AbstractProduct
``` swift
protocol Buttonalbe {
    func touchUP()
}

protocol Labelable {
    var title: String { get }
}
```
   
ConcreateProduct
``` swift
final class IPhoneButton: Buttonalbe {
    func touchUP() {
        print("iPhoneButton")
    }
}

final class IPadButton: Buttonalbe {
    func touchUP() {
        print("iPadButton")
    }
}

final class IPhoneLabel: Labelable {
    var title: String = "iPhoneLabel"
}

final class IPadLabel: Labelable {
    var title: String = "iPadLabel"
}
```   
   
Client
``` swift
import UIKit

class ViewController: UIViewController {

    //UI를 가지고 있는 인스턴스 기기별로 설정
    var iPadUIContent = UIContent(uiFactory: iPadUIFactoy())
    var iPhoneUIContent = UIContent()

    override func viewDidLoad() {
        super.viewDidLoad()
        touchUpButton()
        printLabelTitle()
    }

    func touchUpButton() {
        iPadUIContent.button?.touchUP()
        iPhoneUIContent.button?.touchUP()
    }

    func printLabelTitle() {
        print(iPadUIContent.label?.title ?? "")
        print(iPhoneUIContent.label?.title ?? "")
    }
}

//Factory를 통해 UI를 만들고 가지고 있는 Class
class UIContent {
    var uiFactory: UIFactoryalbe
    var label: Labelable?
    var button: Buttonalbe?

    //사용할 UI의 Default 값은 iPhone
    init(uiFactory: UIFactoryalbe = iPhoneUIFactory()) {
        self.uiFactory = uiFactory
        setUpUI()
    }

        //기기에 맞는 UI들 설정
    func setUpUI() {
        label = uiFactory.createLabel()
        button = uiFactory.createButton()
    }
}
```

## Abstract Factory Pattern의 한계?
- Abstract Factory Method 패턴은 Factroy가 추가되고 기존에 존재하는 Product로 Factory를 구성 할때는 매우 효과적인 패턴이 될 수 있습니다.
- 하지만 새로운 종류의 Product가 추가되면 각각의 Factory에도 추가해줘야 하는 경우가 생깁니다. Product의 추가나 변동이 잦아진다면 모든 Factory에 변동이 생길 위험이 있습니다.
