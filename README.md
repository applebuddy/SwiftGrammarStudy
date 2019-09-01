# SwiftGrammarStudy

- 2015 WWDC에서 스위프트는 첫 Protocol oriented programming Language

- When you use the override keyword you tell the compiler to allow changing an inherited method in your subclass.
override 
- -> 키워드를 쓰는 순간 상속받은 메서드를 서브클래스에서 바꿀 수 있게 한다. 


## 프로토콜과 다형성 
### Protocol, Polymorphism
### Swift의 클래스 상속, 오버라이딩 시 특성
- This means that the subclass instances will have no knowledge about the implementation of the overriden superclass method.
- -> 수퍼클래스의 메서드를 서브클래스에서 오버라이드 하는 순간 해당 메서드의 인스턴스는 서브클래스의 오버라이딩 한 메서드로 인식하게 된다. 
  - 이러한 특성 때문에 viewDidLoad, viewWillAppear 등 에서 super.viewDidLoad() 를 명시하여, 부모클래스의 메서드를 적용하면서 오버라이딩을 하는 것이다. 

### 프로그래밍 타입 별 구성 테이블
- 객체 지향 프로그래밍 : OOP(Object Oriented Programming) & V - Table 
- 프로토콜 지향 프로그래밍 : POP(Protocol Oriented Programming) & Witness table
  - *둘다 동적인 의미의 테이블

- Dynamic Dispatch : **다형성을 활용한 프로토콜 메서드의 사용**

~~~ swift 
//Dynamic Dispatch 사용 예시) 
다형성.... RetroActive

protocol Geometry {
func area() -> CGFloat
func perimeter() -> CGFloat
}

extension Circle: Geometry {
func area() -> CGFloat {
return .pi * radius * radius
}

func perimeter() -> CGFloat {
return .pi * radius * 2
}
}

extension CGRect: Geometry {
func perimeter() -> CGFloat {
return (width+height) * 2
}

func area() -> CGFloat {
return size.width * size.height
}
}

let shapes: [Geometry] = [circle, rect]


// Compute the total perimeter of the shapes array
// You may add to the Geometry formal protocol

print(shapes.reduce(0) { $0 + $1.perimeter() })

~~~

## 제네릭
### 명확한 타입 정의
- 프로토콜 Protocol과 더불어 제네릭(Generic)은 Swift의 심장이라 할 수 있다.

- 제네릭에 대해 참고할만한 사이트 : Where to go from Here
  - Generics: Getting Started 
  - WWDC 2018 Swift Generics
  - Swift.org
