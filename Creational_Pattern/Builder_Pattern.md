# Builder Pattern

## 빌더 패턴 (Builder Pattern)
복합 객체의 생성과정과 표현 방법을 분리하여 동일한 생성 절차에서 서로 다른 표현 결과를 만들 수 있게하는 패턴이다. - 위키 백과   
빌더 패턴은 복잡한 객체를 생성할 때 유용한 패턴이다.   
   
기본적으로 product와 이를 만드는 Builder으로 구성되어 있다. 필요에 따라 추가 및 변형될 수 있다.   
Builder는 어떤 값을 세팅하는 메서드와 Product를 만드는 Build() 메서드를 갖는다.   
Product를 만드는 모든 과정은 Builder가 담당한다.   
   
## 빌더 패턴을 사용하면 좋을 때
**Swift**에선 그렇게 유효한 패턴은 아니다.   
대부분 초기화 메서드와 프로퍼티 기본 값을 통해 해결할 수 있다.   
굳이 빌더 패턴의 사용처를 생각해본다면, 프로퍼티의 개수가 엄청많아지고 복잡해지는 경우다.   
    
## 빌더 패턴 예제
옷은 다양한 종류가 있으므로 빌더 패턴으로 적합하기에 예제로 만들었다.
   
입을 옷 정의
``` swift
struct Clothes {
    let outer : Outer1
    let top : Top
    let pants : Pants
    let bag : Bag
    let shoes : Shoes
    
    func printClothes(){
        print(outer)
        print(top)
        print(pants)
        print(bag)
        print(shoes)
    }
}

enum Outer1 : String {
    case jacket
    case overcoat
    case trenchCoat
}

enum Top : String {
    case shirt
    case T_shirt
    case flannelShirt
}

enum Pants : String {
    case cargoPants
    case joggerPants
    case bluejeans
    case slacks
}

enum Bag : String {
    case clutchBag
    case crossBag
    case backPack
}

enum Shoes : String {
    case sneakers
    case runningShoes
    case flipFlops
}
```
   
Bilder정의
``` swift
class ClothesBuilder {
    private var outer : Outer1 = .jacket
    private var top : Top = .T_shirt
    private var pants : Pants = .slacks
    private var bag : Bag = .backPack
    private var shoes : Shoes = .sneakers
    
    func choiceOuter(_ outer : Outer1) -> ClothesBuilder {
        self.outer = outer
        return self
    }
    
    func choiceTop(_ top : Top) -> ClothesBuilder {
        self.top = top
        return self
    }
    
    func choicePants(_ pants : Pants) -> ClothesBuilder {
        self.pants = pants
        return self
    }
    
    func choiceBag(_ bag : Bag) -> ClothesBuilder {
        self.bag = bag
        return self
    }
    
    func choiceShoes(_ shoes : Shoes) -> ClothesBuilder {
        self.shoes = shoes
        return self
    }
    
    func Build() -> Clothes {
        return Clothes(outer: outer, top: top, pants: pants, bag: bag, shoes: shoes)
    }
}
```
   
실행
``` swift
let builder = ClothesBuilder()
var clothes = builder.Build()
clothes.printClothes()

var clothes2 = 
    builder.choiceOuter(.overcoat)
    .choiceBag(.backPack)
    .choicePants(.bluejeans)
    .choiceTop(.shirt)
    .choiceShoes(.runningShoes)
    .Build()
clothes2.printClothes()
```
