
<br>
<br>
<br>

# SwiftGrammarStudy

<br>
<br>

## Swift
- **Apple WWDC 2014에서 공개된 프로그래밍 언어.**
- **POP(Protocol Oriented Programming), OOP(Object Oriented Programming)를 동시에 지향하는 프로그래밍언어**
- Class, Struct, Enum, Protocol 등의 핵심 자료구조를 지원한다.
- ARC(Automatic Refernce Counting) : 힙(Heap) 영역의 동적할당을 자동으로 관리해준다.
- 단일상속을 지원한다. Protocol을 통해 다중상속의 효과를 구현할 수 있다. 
- 함수형 프로그래밍을 지향한다. 

<br>
<br>

## ✓ 프로토콜과 다형성 

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

<br>
<br>

## ✓ 제네릭
### 명확한 타입 정의
- 프로토콜 Protocol과 더불어 제네릭(Generic)은 Swift의 심장이라 할 수 있다.

- 제네릭에 대해 참고할만한 사이트 : Where to go from Here
  - Generics: Getting Started 
  - WWDC 2018 Swift Generics
  - Swift.org


<br>
<br>

## ✓ 가상 메모리의 구성

### 코드부 (Code, 정적)
- **함수와 상수가 저장되는 공간**
- 프로그램이 실행되는 중 변하지 않는 공간
- 컴파일(Compile) 중 할당 되는 영역

<br>

### 데이터부 (Data, 정적)
- **전역(Global), 정적(Static) 변수가 저장되는 공간**
- 프로그램 실행기간 동안(프로그램이 끝날 때까지) 메모리에 남아있는다.
- 컴파일(Compile) 중 할당 되는 영역

<br>

### 스택 (Stack)
- **지역(Local), 매개(Parameter)변수가 저장되는 공간**
- 각각 영역 내 함수 실행 완료 시 메모리를 반환하게 된다. 
- 컴파일(Compile) 중 할당 되는 영역

<br>

### 힙 (Heap, 동적)
- **개발자가 동적으로 할당하는 데이터가 저장되는 영역**
- 참조타입(Reference Type)들이 저장 되는 공간
- C, C++등에서는 개발자가 직접 동적할당을 관리할 수 있음(new, malloc, delete ... ans so on...)
- Swift에서는 ARC(Automatic Reference Counting)으로 자동 관리됨
- 런타임(RunTime) 중 할당 되는 영역

<br>
<br>

## ✓ '@...", Annotation
- 어노테이션(Annotation)은 기대하는 값과 대비되는 특정 값을 확실히 하기 위한 유용한 방법이다.
- 어노테이션을 통해 변수의 목적, 성질 등을 정의할 수 있다. 
- 종류 : @Designable, @Inspectable, @inline...

<br>

### @Inline
- 일반적인 함수(function)들은 홈출 될 시 해당 함수의 주소로 이동하여 실행하고 다시 호출했던 위치로 돌아오는 소요를 감수한다. 
  - 이때의 주소 이동, 이동할 주소 기억 등 비용이 생기는데...
  - **inline함수를 사용하면 컴파일 시간에 해당 함수를 호출부에 코드로 붙여주어 해당 비용을 절약**시킬 수 있다. 
- 적용 옵션
  - always : 해당 인라인 함수를 항상 적용한다.
  - never : 해당 인라인 함수를 적용하지 않는다.
- @inline 사용예시 
~~~ swift 
// 항상 적용되는(inline always) 인라인 함수 예시)
@inline(__always) func alwaysTest() {
    // inline 함수 작성하면 된다.
}

// 적용되지 않는(inline never) 인라인 함수 예시)
@inline(never) func neverTest() {
    // inline 함수 작성하면 된다.
}
~~~

<br>


<br>
