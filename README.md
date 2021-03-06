# iOSInterviewquestion

## iOS
<details>
<summary>Bounds 와 Frame 의 공통점과 차이점을 설명하시오. </summary>
<div markdown="1">

```
- 공통점
    - 사각형으로 그려짐 -> 둘 다  x,y좌표, width, height를 가짐

- 차이점
    - frame : 자신의 superview(부모뷰)를 기준으로 x,y위치를 정함
    - bound : 자신만의 좌표 시스템을 가져 x,y위치를 정함, default는 (0,0)

(참고 https://zeddios.tistory.com/203)

```
</div>
</details>






<details>
<summary>실제 디바이스가 없을 경우 개발 환경에서 할 수 있는 것과 없는 것을 설명하시오. </summary>
<div markdown="1">

```
 📌 할 수 없는 것
    - GPS
    - 카메라 촬영 (앨범은 가능)
    - 블루투스
    - 책상에 엎거나 올려놓은 상태인 faceup, facedown모드 체크 


 📌 할 수 있는 것
    - 페이스 ID (직접 얼굴 인식은 못해도 시뮬레이터의 메뉴상에서 인식됨/안됨 처리 가능)
    - 그 외 대부분의 것들 가능

(참고 https://yagom.net/forums/topic/%EC%8B%A4%EC%A0%9C-%EB%94%94%EB%B0%94%EC%9D%B4%EC%8A%A4%EA%B0%80-%EC%97%86%EC%9D%84%EB%95%8C-%ED%95%A0%EC%88%98%EC%9E%88%EB%8A%94%EA%B2%83%EA%B3%BC-%EC%97%86%EB%8A%94%EA%B2%83/)

```
</div>
</details>


<details>
<summary>앱의 콘텐츠나 데이터 자체를 저장/보관하는 특별한 객체를 무엇이라고 하는가? </summary>
<div markdown="1">

```
📌 UserDefaults
    -[데이터, 키]로 데이터 저장
    - 앱이 꺼져도 특정한 값이 저장되길 원하는 경우
    - 앱이 사라지면 같이 사라짐 
    - ex) 최근검색기록, 로컬알림설정 여부..

참고 : https://lemon-dev.tistory.com/entry/NSUserDefaults
```


```swift
// 데이터 저장
UserDefaults.standard.set(value, forKey: "키")

// 데이터 꺼내오기
UserDefaults.standard.string(forKey: "키")
```
</div>
</details>





<details>
<summary>앱 화면의 콘텐츠를 표시하는 로직과 관리를 담당하는 객체를 무엇이라고 하는가? </summary>
<div markdown="1">

```
 📌 ViewController
    - 주요한 데이터의 변화에 대한 응답으로 뷰들의 컨텐트들 업데이트함

    - 뷰들과 함께 사용자와의 대화에 응답 -> 이벤트 핸들링(클릭같은)

    - 뷰들의 사이즈 재조정과 인터페이스 레이아웃 관리

    - 종류는 두가지 1.일반적인 ContentViewController 
                 2. 여러개의 VC를 제어하는 ContainerViewController (ex 탭바)



(참고 https://o-o-wl.tistory.com/43)

```
</div>
</details>




<details>
<summary>App thinning에 대해서 설명하시오. </summary>
<div markdown="1">

```
📌 App Thinning
    - 앱이 설치될 때, 앱 스토어와 운영체제가 디바이스의 특성에 맞게 설치되도록 하는 설치 최적화 기술
    - 구성으로는 슬라이싱, 비트코드, 주문형 리소스가 있음

    📍 슬라이싱
        - 사용자가 앱스토어로 앱을 설치 -> 사용자의 기기와 운영체제 버전에 맞춰 가장 적합한 조각(variant)을 다운로드

    📍 비트코드
        - 기계언어로 번역되기 이전 단계의 중간표현 -> 앱의 새 버전을 앱스토어에 제출할 필요없이 알아서 최적화시킴

    📍 주문형 리소스(On-Demand Resource)
        - 이미지나 사운드같은 리소스를 키워드로 태그할 수 있고 태그별로 그룹을 요청할 수 있음
        - 필요할 때 다운로드를 하는 것 (ex 인앱 구매)
        
참고 - https://ttuk-ttak.tistory.com/42
```
</div>
</details>




###
<details>
<summary>앱이 시작할 때 main.c 에 있는 UIApplicationMain 함수에 의해서 생성되는 객체는 무엇인가? </summary>
<div markdown="1">

```
📌 Objective-C
    - C언어 기반 프로그램으로, 시작점은 main함수임
    
📌 swift
    - C언어 기반이 아니기 때문에 main파일이 존재하지 않음 
    - 따라서 시작 진입점도 존재하지 않음

하지만 시작 진입점이 없으면 안되기 때문에 annotation으로 표기
```

```swift
import UIKit

@UIApplicationMain // 어노테이션으로 표기

class AppDelegate: UIResponder, UIApplicationDelegate {

    var window: UIWindow?
    
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {

    }
}
```

```
📌 UIApplication 함수
    - 코코아 터치 프레임워크에서 앱의 lifecycle을 시작하는 함수
        -> UIApplication 객체의 인스턴스 생성, 
           앱의 기반을 마련 == 앱 로딩 프로세스

참고 - https://jinshine.github.io/2018/05/28/iOS/%EC%95%B1%EC%9D%98%20%EC%83%9D%EB%AA%85%EC%A3%BC%EA%B8%B0(App%20Life%20Cycle)%EC%99%80%20%EC%95%B1%EC%9D%98%20%EA%B5%AC%EC%A1%B0(App%20Structure)/
```
</div>
</details>


<details>
<summary>@Main에 대해 설명하시오. </summary>
<div markdown="1">

```
📌 @Main
    - 프로그램 실행 시작 시 진입점으로 타입을 지정하기 위한 Swift 언어의 기능
    - 사용자는 탑 레벨의 코드를 작성하는 대신 @main단일 유형의 속성을 사용
    - @UIApplicationMain 대신 @main을 사용함으로 타입 기반의 스위프트 코드에서 이상적인 진입점을 알려줌
```
</div>
</details>




<details>
<summary> 앱이 foreground에 있을 때와 background에 있을 때 제약사항 </summary>
<div markdown="1">

```
 📌 foreground
    - 사용자가 보고 있는 화면
    - CPU를 비롯한 시스템 자원의 우선순위가 높은 상태
    - 메모리 및 기타 시스템 리소스에 대해서 background보다 높은 우선순위를 가짐 -> 시스템은 이러한 리소스를 사용할 수 있도록 필요에 따라 background 앱을 종료




 📌 background
    - 홈화면에 들어가서 사용자한테 보이지 않는 상태
    - 가능한 적은 메모리공간을 사용해야함
    - 우선순위에 의해 foreground task보다 더 낮은 자원을 할당 

(참고 https://snowee.tistory.com/39)

```
</div>
</details>
- 상태 변화에 따라 다른 동작을 처리하기 위한 앱델리게이트 메서드들을 설명하시오.
- 앱이 In-Active 상태가 되는 시나리오를 설명하시오.
- scene delegate에 대해 설명하시오.
- UIApplication 객체의 컨트롤러 역할은 어디에 구현해야 하는가?
- App의 Not running, Inactive, Active, Background, Suspended에 대해 설명하시오.
###
- NSOperationQueue 와 GCD Queue 의 차이점을 설명하시오.
- GCD API 동작 방식과 필요성에 대해 설명하시오.
- Global DispatchQueue 의 Qos 에는 어떤 종류가 있는지, 각각 어떤 의미인지 설명하시오.
###
- iOS 앱을 만들고, User Interface를 구성하는 데 필수적인 프레임워크 이름은 무엇인가?
- Foundation Kit은 무엇이고 포함되어 있는 클래스들은 어떤 것이 있는지 설명하시오.
- Delegate란 무엇인지 설명하고, retain 되는지 안되는지 그 이유를 함께 설명하시오.
- NotificationCenter 동작 방식과 활용 방안에 대해 설명하시오.
- UIKit 클래스들을 다룰 때 꼭 처리해야하는 애플리케이션 쓰레드 이름은 무엇인가?
- App Bundle의 구조와 역할에 대해 설명하시오.
- 모든 View Controller 객체의 상위 클래스는 무엇이고 그 역할은 무엇인가?
- 자신만의 Custom View를 만들려면 어떻게 해야하는지 설명하시오.
- View 객체에 대해 설명하시오.
- UIView 에서 Layer 객체는 무엇이고 어떤 역할을 담당하는지 설명하시오.
- UIWindow 객체의 역할은 무엇인가?
- UINavigationController 의 역할이 무엇인지 설명하시오.
- TableView를 동작 방식과 화면에 Cell을 출력하기 위해 최소한 구현해야 하는 DataSource 메서드를 설명하시오.
- 하나의 View Controller 코드에서 여러 TableView Controller 역할을 해야 할 경우 어떻게 구분해서 구현해야 하는지 설명하시오.
- setNeedsLayout와 setNeedsDisplay의 차이에 대해 설명하시오.
###
- NSCache와 딕셔너리로 캐시를 구성했을때의 차이를 설명하시오.
- URLSession에 대해서 설명하시오.
- prepareForReuse에 대해서 설명하시오.
- 다크모드를 지원하는 방법에 대해 설명하시오.
- ViewController의 생명주기를 설명하시오.
- TableView와 CollectionView의 차이점을 설명하시오.

## Autolayout

<details>
<summary>스토리보드를 이용했을 때 장단점을 설명하시오.</summary>
<div markdown="1">

```
 📌스토리보드 장점
    - 앱의 흐름을 한 번에 볼 수 있음
    - 코드를 몰라도 UI 구현 가능


📌스토리보드 단점
    - 앱의 규모가 커지면 스토리보드 로딩 시간이 길어짐
    - 다수의 인원이 처리하게 되면 merge conflict가 나서 협업이 힘듦
    - 스토리보드로 만든 뷰는 재사용이 어렵
    - MVVM패턴 사용 불가능

```
</div>
</details>




<details>
<summary>Safearea에 대해서 설명하시오.</summary>
<div markdown="1">

```
 📌 Safearea
    - 컨텐츠가 가려지지 않는 것을 보장하는 영역

    - 어떤 content(status bar, navigation bar, toolbar, tab bar, etc) 에도 덮이지 않는 뷰를 그리기 위해서 제공

```
</div>
</details>

- 오토레이아웃을 코드로 작성하는 방법은 무엇인가? (3가지)
- hugging, resistance에 대해서 설명하시오.
- Intrinsic Size에 대해서 설명하시오.

- Left Constraint 와 Leading Constraint 의 차이점을 설명하시오.

## Swift



<details>
<summary>struct와 class와 enum의 차이를 설명하시오. </summary>
<div markdown="1">

```
- 공통점
    - 모두 extension(확장) 가능

- 차이점
    📌 class 
        - 참조 타입
        - 참조타입이기 때문에 let로 선언해도 내부 프로퍼티 변경 가능
        - 상속 가능(다중 상속은 불가능)
        - 기본값이 없으면 이니셜라이져 필수
        - 애플이 제공하는 Framework들(UIViewController..)는 대부분 클래스로 되어있음

    📌 struct
        - 값 타입
        - 이니셜라이저를 자동으로 만들어줌
        - 애플이 제공하는 Data타입들(Int, String..) 대부분 구조체로 되어있음

    📌 enum
        - 값 타입
        - 연관된 값들을 한 곳에 묶어놓은 타입
        - 상속 불가능

(참고 https://h4njun.tistory.com/entry/class-%EC%99%80-struct-%EA%B7%B8%EB%A6%AC%EA%B3%A0-enum)

```
</div>
</details>




<details>
<summary>Subscripts에 대해 설명하시오. </summary>
<div markdown="1">

```
📌 subscript
    - 특정 member elements에 간단하게 접근할 수 있는 문법

    subscript(index: Int) -> Int {
        get {
        // 반환 값
        }
        set(newValue) {
        // set 액션
        }
    }

    - 예를 들어, array[index]로 배열의 인스턴스 항목에 접근하는 것

    - read-write / read-only 만 가능 (write-only 불가능!!)

    - set에 대한 디폴트값 지정하지 않으면 기본값으로 newValue사용


(참고 https://medium.com/@jgj455/%EC%98%A4%EB%8A%98%EC%9D%98-swift-%EC%83%81%EC%8B%9D-subscript-2288551588f9)

```
</div>
</details>



<details>
<summary>Any와 AnyObject에 대해 설명하시오. </summary>
<div markdown="1">

```
📌 Any
    - 함수타입을 포함한 모든 타입의 인스턴스

📌 AnyObject
    - 모든 클래스 타입의 인스턴스

```

```swift
// Any -> 모든 타입이 인스턴스로 가능, 여러 자료형을 배열에 넣을 수 있음
var anyArray: [Any] = [1, "hi", true, 1.0] 


// AnyObject -> 클래스타입이 인스턴스로!
class aType { }
class bType { }
var anyObjectArray: [AnyObject] = [aType(), bType()]
```
</div>
</details>




- class의 성능을 향상 시킬수 있는 방법들을 나열해보시오.
- Copy On Write는 어떤 방식으로 동작하는지 설명하시오.
- Convenience init에 대해 설명하시오.
- Optional 이란 무엇인지 설명하시오.
- Struct 가 무엇이고 어떻게 사용하는지 설명하시오.
- String은 왜 subscript로 접근이 안되는지 설명하시오.
- instance 메서드와 class 메서드의 차이점을 설명하시오.
- class 메서드와 static 메서드의 차이점을 설명하시오.
- Delegate 패턴을 활용하는 경우를 예를 들어 설명하시오.
- Singleton 패턴을 활용하는 경우를 예를 들어 설명하시오.
- KVO 동작 방식에 대해 설명하시오.
- Delegates와 Notification 방식의 차이점에 대해 설명하시오.
- 멀티 쓰레드로 동작하는 앱을 작성하고 싶을 때 고려할 수 있는 방식들을 설명하시오.
- MVC 구조에 대해 블록 그림을 그리고, 각 역할과 흐름을 설명하시오.
- 프로토콜이란 무엇인지 설명하시오.
- Protocol Oriented Programming과 Object Oriented Programming의 차이점을 설명하시오.
- Hashable이 무엇이고, Equatable을 왜 상속해야 하는지 설명하시오.
- mutating 키워드에 대해 설명하시오.
- 탈출 클로저에 대하여 설명하시오.
- Extension에 대해 설명하시오.
- Extension 내부에서 함수를 override할 수 있는지 설명하시오.
- 접근 제어자의 종류엔 어떤게 있는지 설명하시오.
- defer란 무엇인지 설명하시오.
- defer가 호출되는 순서는 어떻게 되고, defer가 호출되지 않는 경우를 설명하시오.
- property wrapper에 대해서 설명하시오.
- Generic에 대해 설명하시오.
- some 키워드에 대해 설명하시오.
- Result타입에 대해 설명하시오.
- Codable에 대하여 설명하시오.
- Closure에 대하여 설명하시오.
- Closure와 함수와의 관계에 대해 설명하시오.

## ARC


<details>
<summary>ARC란 무엇인지 설명하시오. </summary>
<div markdown="1">

```
📌 ARC
    - Automatic Reference Counting의 약자
    - ARC는 더이상 필요하지 않은 클래스 인스턴스를 자동으로 메모리에서 해제함
        -> RC(Reference Count)를 통해 필요하지 않은 인스턴스를 알 수 있음
        -> 인스턴스를 참조되고 있는 count를 기록하고 0이되면 인스턴스를 참조하는 곳이 없는 것을 알고 자동으로 인스턴스를 메모리에서 해제시킴

    - 강한참조 : RC를 증가시킴
    - 약한참조 : RC를 증가시키지 않음, 다른 인스턴스를 먼저 할당 해제 할 수 있는 경우 사용 

참고 - https://zeddios.tistory.com/1213
```
</div>
</details>


- Retain Count 방식에 대해 설명하시오.
- Strong 과 Weak 참조 방식에 대해 설명하시오.
- 순환 참조에 대하여 설명하시오.
- 강한 순환 참조 (Strong Reference Cycle) 는 어떤 경우에 발생하는지 설명하시오.

## Functional Programming
- 순수함수란 무엇인지 설명하시오.
- 함수형 프로그래밍이 무엇인지 설명하시오.
- 고차 함수가 무엇인지 설명하시오.
- Swift Standard Library의 map, filter, reduce, compactMap, flatMap에 대하여 설명하시오.

## Architecture
- MVVM, MVI, Ribs, VIP 등 자신이 알고있는 아키텍쳐를 설명하시오.
- 의존성 주입에 대하여 설명하시오.

## SwiftUI
- @State에 대해서 설명하시오.

## Combine
- PassthroughSubject에 대해서 설명하시오
- @Published에 대해서 설명하시오
- AnyCancellable에 대해서 설명하시오
- sink에 대해서 설명하시오
- throttle과 debounce의 차이점을 설명하시오.

# Optional
아래부터는 추가로 공부를 하면 좋을 내용들입니다.

Objective-c나 rx는 회사, 팀마다 사용하는곳이 차이가있고 신입이나 주니어기준으로 필수라고 여겨지지않기에 옵셔널에 추가하였습니다.

## Rx
- Reactive Programming이 무엇인지 설명하시오.
- RxSwift를 왜 사용하는지 설명하시오.
- RxSwift의 단점을 설명하시오.
- RxSwift에서 Hot Observable과 Cold Observable의 차이를 설명하시오.
- Subject의 종류와 차이점에 대해 설명하시오.
- Subject와 Driver의 차이를 설명하시오.
- Single, Completable, Maybe의 차이점에 대해 설명하고, 언제 적용하면 좋을지 설명하시오.

## MRC
- ARC 대신 Manual Reference Count 방식으로 구현할 때 꼭 사용해야 하는 메서드들을 쓰고 역할을 설명하시오.
- retain 과 assign 의 차이점을 설명하시오.
- 특정 객체를 autorelease 하기 위해 필요한 사항과 과정을 설명하시오.
- Autorelease Pool을 사용해야 하는 상황을 두 가지 이상 예로 들어 설명하시오. 
- 다음 코드를 실행하면 어떤 일이 발생할까 추측해서 설명하시오.
Ball *ball = [[[[Ball alloc] init] autorelease] autorelease];

## Advanced
- method swizzling이 무엇이고, 어떨 때 사용하는지 설명하시오.
- NSCoder 클래스는 어떤 상황에서 어떻게 써야 하는지 설명하시오.
- Responder Chain 구조에 대해 설명하고, First Responder 역할에 대해 설명하시오.
- NSObject부터 UIButton 까지 상속 과정의 계층과 역할을 설명하시오.
- shallow copy와 deep copy의 차이점을 설명하시오.
- Push Notification 방식에 대해 설명하시오.
- Foundation 과 Core Foundation 프레임워크의 차이점을 설명하시오.
- NSURLConnection 에서 사용하는 Delegate 메서드들에 대해 설명하시오.
- Synchronous 방식과 Asynchronous 방식으로 URL Connection을 처리할 경우의 장단점을 비교하시오.
- Plist 파일 구조와 Plist 파일에 저장된 데이터를 다루기 적합한 클래스를 설명하시오.
- Core Data와 Sqlite 같은 데이터 베이스의 차이점을 설명하시오.
- JSON 데이터를 처리하는 방식과 파서, 객체 변환 방식에 대해 설명하시오.
- 웹 서버와 HTTP 연결을 사용해서 데이터를 주거나 받으려면 사용해야 하는 클래스와 동작을 설명하시오.
- Protocol에서는 왜 var만 되는지 설명하시요.
- DispatchQueue.main.sync를 사용하는 상황을 설명하시오.
- Run Loops에 대해 설명하시오.

## Objective-C
- Swift의 클로저와 Objective-C의 블록은 어떤 차이가 있는가?
- Mutable 객체과 Immutable 객체는 어떤것이 있는지 예를 들고, 차이점을 설명하시오.
- dynamic과 property 의미와 차이를 설명하시오.
- @property로 선언한 NSString* title 의 getter/setter 메서드를 구현해보시오.
- @property에서 atomic과 nonatomic 차이점을 설명하고, 어떤것이 안전한지, 어느것이 기본인지 설명하시오.
- @property로 선언한다는 것의 의미를 설명하고, .h에 넣을 경우와 .m에 넣을 경우 차이점을 설명하시오.
- -performSelector:withObject:afterDelay: 메시지를 보내면 인자값의 객체는 retain되는가? 그 이유를 함께 설명하시오.
- Objective-C 에서 캡슐화된 데이터를 접근하기 위한 방법들을 설명하시오.
- Fast Enumeration 이란 무엇인지 설명하시오. 
- unnamed category 방식에 대해 설명하시오.
- Category 확장과 Subclass 확장의 차이점을 설명하시오.
- Category 방식에 대해 설명하시오.
- Objective-C 에서 Protocol 이란 무엇인지 설명하시오.
- Objective-C++ 방식이 무엇인지 설명하고, 어떤 경우 사용해야 하는지 설명하시오.

