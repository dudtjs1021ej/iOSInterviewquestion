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




<details>
<summary> 상태 변화에 따라 다른 동작을 처리하기 위한 앱델리게이트 메서드들을 설명하시오. </summary>
<div markdown="1">

## 📌 AppDelegate

### **func application(_: didFinishLaunchingWithOptions: ) -> Bool**

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool	
```

- 애플리케이션이 **실행된 직후 사용자의 화면에 보여지기 직전**에 호출

<br>

### **func application(_: configurationForConnecting:options: ) -> UISceneConfiguration**

```swift
func application(_ application: UIApplication, configurationForConnecting connectingSceneSession: UISceneSession, options: UIScene.ConnectionOptions) -> UISceneConfiguration
```

- **사용자나 새로운 Scene이 생성될 때 호출**

<br>

### **func application (_ : didDiscardSceneSessions :)**

```swift
func application(_ application: UIApplication, didDiscardSceneSessions sceneSessions: Set<UISceneSession>)
```

- scene이 **background로 들어갔을 때** 시스템이 자원을 확보하기 위해 disconnect하려고 할 때 호출
- app 종료와 다르다고 함

<br>

## ‼️13.0부터 SceneDelegate로 나뉨

            

<img width="548" alt="image" src="https://user-images.githubusercontent.com/77915491/224705801-28274f3a-79d3-440a-ad6f-d0c6c838a89c.png">


- iPad OS에서 **multi- window**가 가능해지면서 AppDelegate가 혼자서 맡던 역할 중 일부가 **SceneDelegate**에게 나눠지게 됨
- **AppDelegate**는 앱의 생명주기를 관리 & **SceneDelegate** 스크린에 표시되어지는 UI의 생명주기를 관리하도록 변경

<br>

## 📌 ScenceDelegate

### sceneWillResignActive

```swift
func sceneWillResignActive(_ scene: UIScene)
```

- 애플리케이션이 **InActive 상태로 전환되기 직전**에 호출
- task 일시정지, 타이머 비활성화, 일시정지(게임)

<br>

### sceneDidEnterBackground

```swift
func applicationDidEnterBackground(_ application: UIApplication)	
```

- 애플리케이션이 **백그라운드 상태**로 전환된 직후 호출

<br>

### sceneWillEnterForeground

```swift
func sceneWillEnterForeground(_ scene: UIScene)
```

- 애플리케이션이 Active 상태가 되기 직전, **화면에 보여지기 직전**에 호출

<br>

### sceneDidBecomeActive

```swift
func applicationDidBecomeActive(_ application: UIApplication)
```

- 애플리케이션이 **Active 상태로 전환**된 **직후** 호출

<br>

### sceneDidDisconnect

```swift
func sceneDidDisconnect(_ scene: UIScene)
```

- 앱에서 **연결을 끊을 때** 호출

<br>

### Reference

[https://developer.apple.com/documentation/uikit/uiapplicationdelegate](https://developer.apple.com/documentation/uikit/uiapplicationdelegate)

[https://velog.io/@2dubu/iOS-AppDelegate-SceneDelegate](https://velog.io/@2dubu/iOS-AppDelegate-SceneDelegate)

<br>
<br>

</div>
</details>



<details>
<summary> GCD API 동작 방식과 필요성에 대해 설명하시오. </summary>
<div markdown="1">

```
 GCD
    - Grand Central Dispatch
    - 앱에서 어떠한 작업을 비동기적으로 동시에 수행할 수 있게 해줘서 필요

    
    - 앱 실행 -> 시스템이 자동으로 메인 스레드 위에 동작하는 Main Queue 만듦
        -> 추가적으로 Global Queue를 만들어서 관리


    - 보통 UI 관련 작업은 Main Queue에서 함 (Serial queue)
    - 그 외의 작업은 추가적으로 Global Queue(Concurrent Queue) 를 만들어서 작업 -> UI 와 관련없는 작업들 비동기적으로 관리


```
</div>
</details>



<details>
<summary> iOS 앱을 만들고, User Interface를 구성하는 데 필수적인 프레임워크 이름은 무엇인가? </summary>
<div markdown="1">

```
 UIKit 
 - 프레임워크는 사용자의 인터페이스를 관리하고, 이벤트를 처리하는게 주 목적인 프레임워크

 - UIkit에서 주로 처리하는 사용자 이벤트로는 제스처 처리, 애니메이션, 그림 그리기, 이미지 처리, 텍스트 처리 등이 있음

 - 테이블뷰, 슬라이더, 버튼, 텍스트 필드, 얼럿 창 등 애플리케이션의 화면을 구성하는 요소도 있음

 - UI를 구현하려면 반드시 UIKit를 상속해야 함

출처 : https://www.notion.so/iOS-User-Interface-bb50a802de9949e59563e3b5d8f4c8de


```
</div>
</details>


<details>
<summary> UIWindow 객체의 역할은 무엇인가? </summary>
<div markdown="1">

```
UIWindow
- 부모는 UIView

- 스크린에 나타나는 모든 View는 Window로 묶여 있으며, 각 Window는 앱의 다른 View와 독립적

- 기기의 기본화면에 앱의 콘텐츠를 표시하는 하나의 Window만 있으면 됨

- 뷰의 계층 구조에서 최상의 뷰의 역할을 하며 뷰들을 담는 컨테이너 역할

코드로 화면을 구현할 때
    -  window를 직접 생성
스토리보드를 통해 화면을 구현할 경우
    - window가 자동으로 생성

출처: https://zeddios.tistory.com/283 [ZeddiOS:티스토리]


```
</div>
</details>



<details>
<summary> UIKit 클래스들을 다룰 때 꼭 처리해야하는 애플리케이션 쓰레드 이름은 무엇인가? </summary>
<div markdown="1">

```
main스레드 에서만 UI를 처리해야 함

1) UIKit의 모든 속성을 Thread-safe하게 설계하면, 느려짐과 같은 성능저하가 발생할 수 있기 때문에 그렇게 설계할 수 없다. (Thread-safe하지 않게 설계한 것은 애플의 의도다.)

2) 메인 런루프(Runloop)가 뷰의 업데이트를 관리하는 View Drawing Cycle을 통해 뷰를 동시에 업데이트 하는 그런 설계를 통해 동작하고 있는데, (메인쓰레드가 아닌)백그라운드 쓰레드가 각자의 런루프로 그런 동작을 하게되었을때, 뷰가 제멋대로 동작할 수있다. (예를  들어, 기기를 회전 했을때, 동시에 뷰의 레이아웃이 재배치되는 그런 동작을 못하게 될 수도 있다.)

3) iOS가 그림의 그리는 렌더링 프로세스(코어애니메이션 -> 렌더서버 -> GPU -> 표시)가 있는데, 여러 쓰레드에서 각자의 뷰의 변경사항 GPU로 보내면 GPU는 각각의 정보를 다 해석해야하니 느려지거나, 비효율적이 될 수 있다.

4) Texture나 ComponentKit이라는 페이스북에서 개발한 비동기적 UI 프레임워크가 있긴 하지만, View Drawing Cycle가 유사한 방식으로 적절한 타이밍에 메인 쓰레드에서 동시에 업데이트 하도록 하고 있다.

출처 : https://www.inflearn.com/news/40327
```
</div>
</details>

<details>
<summary> App의 Not running, Inactive, Active, Background, Suspended에 대해 설명하시오. </summary>
<div markdown="1">

```
📌 Not Running
    - 앱이 아직 실행중이지 않은 상태

📌 Foreground - Inactive (비활성화)
    - 앱이 실행중이지만 사용자로부터 이벤트를 받을 수 없는 상태
    - ex) 전화가 와서 앱을 실행 못하는 상황

📌 Foreground - active (활성화)
    - 앱이 실제 실행중이고 사용자에게 이벤트를 받아서 상호작용을 할 수 있는 상황

📌 Background - running
    - 홈화면으로 나가거나 다른 앱을 실행해 현재 앱이 실질적으로 동작하지 않는 상황
    - ex) 음악앱을 닫아도 노래는 재생됨

 📌 Background - suspensed
    - 앱을 다시 시작했을 때 최근 작업을 빠르게 보여주기 위해 메모리 관련 데이터만 저장되어 있는 상황

```
</div>
</details>

<details>
<summary> Global DispatchQueue 의 Qos 에는 어떤 종류가 있는지, 각각 어떤 의미인지 설명하시오. </summary>
<div markdown="1">

```

📍QoS (Quality-of-service)
Qos는 원래 네트워크에서 사용하는 용어로 서비스의 중요도에 따라 중요한 서비스에 더 많은 자원을 할당하는 것, 또는 이 중요도를 뜻하는 말

📌userInteractive
메인 스레드에서 작업하거나 사용자 인터페이스를 새로 고치거나 애니메이션을 수행하는 등 사용자와 상호 작용하는 작업

📌Initiated
사용자가 시작한 작업으로 저장된 문서를 열거나 사용자가 사용자 인터페이스에서 무언가를 클릭 할 때 작업을 수행하는 등 즉각적인 결과가 필요할 때 사용

📌default
기본값

📌utility
완료하는데 약간의 시간이 걸리고 데이터 다운로드 또는 가져오기와 같이 즉각적인 결과가 필요하지 않은 작업

📌background
인덱싱, 동기화 및 백업과 같이 백그라운드에서 작동하고 사용자에게 표시되지 않는 작업

```
</div>
</details>

<details>
<summary> 앱이 In-Active 상태가 되는 시나리오를 설명하시오. </summary>
<div markdown="1">

```
1. 전화나 메시지 같은 인터럽트가 발생
2. 미리알림 같은 특정 알림창이 화면을 덮어서 앱이 실질적으로 event를 받지 못하는 상태 
3. 앱을 처음 킨 상태
4. foreground에서 background, background에서 foreground 상태가 될 때
-> in-Active 상태가 됨

```
</div>
</details>

<details>
<summary> scene delegate에 대해 설명하시오. </summary>
<div markdown="1">

## 📌 iOS 13 이전

iOS 13이전에는 SceneDelegate가 존재하지 않았다..! 

대신 **AppDelegate**가 존재했는데 **AppDelegate**는 두가지 역할이 있었다.

![image](https://user-images.githubusercontent.com/77915491/225007943-93038605-fc37-47a2-8e98-f760b6b09a84.png)

1. 시스템이 프로세스가 시작되거나 종료될 때 appdelegate에게 알림
2. 앱에 UI 상태를 알림 (예를 들어 앱이 포그라운드에 있거나 이제 active상태가 될거나 같은 걸 알려줌)

사실 이런 역할은 12버전 이전에는 괜찮았다. 

왜냐면 1개의 앱엔 1개의 사용자 인터페이스가 있었기때문!

<br>

## 📌 iOS 13 이후

![image](https://user-images.githubusercontent.com/77915491/225008182-16b88cef-5493-4200-8905-06d2893892bc.png)


but 13버전 이후부터는 1개의 앱이 여러개의 창(scene)을 가질 수 있게 되었다.

그러면서 **SceneDelegate**가 등장하게 된 것이다!!

위에 말했던 AppDelegate의 2번 역할을 씬딜리겟이 맡게 된다.


추가로 AppDelegate는 **새로운 역할**을 받게 되는데
 새**로운 Scene세션이 생기거나 삭제될 때** 시스템이 AppDelegate에게 알리게 된다.

(여기서 Session이 Discard된다 = 사용자가 앱을 위로 스와이프해 지웠을 때를 말함)

<br>

## 📌 Scene Delegate의 메소드

### sceneWillResignActive

```swift
func sceneWillResignActive(_ scene: UIScene)
```

- 애플리케이션이 **InActive 상태로 전환되기 직전**에 호출
- task 일시정지, 타이머 비활성화, 일시정지(게임)

### sceneDidEnterBackground

```swift
func applicationDidEnterBackground(_ application: UIApplication)	
```

- 애플리케이션이 **백그라운드 상태**로 전환된 직후 호출

### sceneWillEnterForeground

```swift
func sceneWillEnterForeground(_ scene: UIScene)
```

- 애플리케이션이 Active 상태가 되기 직전, **화면에 보여지기 직전**에 호출

### sceneDidBecomeActive

```swift
func applicationDidBecomeActive(_ application: UIApplication)
```

- 애플리케이션이 **Active 상태로 전환**된 **직후** 호출

### sceneDidDisconnect

```swift
func sceneDidDisconnect(_ scene: UIScene)
```

- 앱에서 **연결을 끊을 때** 호출

### Reference

[https://developer.apple.com/videos/play/wwdc2019/258/](https://developer.apple.com/videos/play/wwdc2019/258/)
<br>
<br>

</div>
</details>
- UIApplication 객체의 컨트롤러 역할은 어디에 구현해야 하는가?




<details>
<summary>NSOperationQueue 와 GCD Queue 의 차이점을 설명하시오.</summary>
<div markdown="1">

## **멀티스레딩을 위한 API**

- 쉽고 편한 멀티 스레딩 처리를 위해 GCD & NSOperation 사용
- NSOperation은 GCD보다 약간의 오버헤드가 더 발생되고 느리지만
 GCD에서는 직접 처리해야 하는 작업들을 지원 하고 있기 때문에 (KVO관찰, 작업취소 등등) 그정도는 감수하고 사용할만함
<br>

### ⁉️ 왜 DispatchQueue를 GCD라 할까?
<br>

```swift
💡Dispatch, also known as Grand Central Dispatch (GCD), contains language features,
 runtime libraries, and system enhancements that provide systemic, 
comprehensive improvements to the support for concurrent code execution 
on multicore hardware in macOS, iOS, watchOS, and tvOS.
```

- GCD는 멀티코어 시스템에서 동시성 실행을 제공하는 프로그래밍 언어 요소, 런타임 라이브러리
- 그래서 엄밀히 말하면 GCD ≠ DispatchQueue
GCD 개념으로 동시성 프로그래밍을 지원하는 스위프트의 API == DispatchQueue
<br>

| GCD (Grand Central Dispatch) | NSOperationQueue |
| --- | --- |
| C기반 저수준 API | Obj-C 기반 고수준 API |
| NSOperation보다 빠르고 오버헤드가 적음 | GCD보다 느리고 조금의 오버헤드 발생 |
| Block Coding으로 단순 구현이 쉬움 | 다양한 작업들에 의존성 추가 가능 |
| KVO 관찰, 작업 취소 등을 지원 | Task 재사용, 취소, 중지 가능 (GCD는 불가능) |
|  | 대기열에 들어갈 수 있는 작업의 숫자를 지정함으로써 동시에 작업의 수를 지정할 수 있음 |

(참고 https://zeddios.tistory.com/203)

<br>
<br>
</div>
</details>



<details>
<summary> Foundation Kit은 무엇이고 포함되어 있는 클래스들은 어떤 것이 있는지 설명하시오. </summary>
<div markdown="1">

```
📌 Foundation Kit
- Cocoa Touch framework에 포함되어 있는 프레임워크 중 하나로 String, Int 등의 원시 데이터 타입과 컬렉션 타입 및 운영체제 서비스를 사용해 앱의 기본적인 기능을 관리하는 프레임워크


기본
- Number : Data, String : 원시 데이터 타입 사용
- Collection : Array, Dictionary, Set 등과 같은 컬렉션 타입 사용
- Date and Time : 날짜와 시간을 계산하거나 비교하는 작업
- Unit and Measuerment : 물리적 차원을 숫자로 표현 및 관련 단위간 변환 기능
- Data Formatting : 숫자, 날짜, 측정값 등을 문자열로 변환 또는 반대 작업
- Filter and Sorting : 컬렉션의 요소를 정렬하거나 검사
 
애플리케이션 지원
- Resource : 애플리케이션의 에셋과 번들 데이터 접근 지원
- Notification : 정보를 퍼트리거나 받아들이는 작업
- App Extension : 확장 애플리케이션과의 상호작용 지원
- Error and Extension : API 상호작용에서 발생할 수 있는 예외 처리
 
파일 및 데이터 관리
- File System : 파일 또는 폴더를 생성하고 읽고 쓰는 관리
- Archive and Serialization : 속성, 목록, JSON, 바이너리 파일들을 객체로 변환 혹은 반대
- iCloud : 사용자의 iCloud 계정을 이용해 데이터를 관리
 
네트워킹
- URL Loading System : 표준 인터넷 프로토콜을 통해 URL과 상호 작용하고 서버와 통신
- Bonjour : 로컬 네트워크를 위한 작업


출처 : https://lazyowl.tistory.com/entry/Foundation-Kit%EC%9D%B4%EB%9E%80

```

</div>
</details>


<details>
<summary> Delegate란 무엇인지 설명하고, retain 되는지 안되는지 그 이유를 함께 설명하시오. </summary>
<div markdown="1">

## Delegate란?

- 대리자라는 뜻
- **객체 지향 프로그래밍에서 하나의 객체가 모든 일을 처리하는 것이 아니라 
처리 해야 할 일 중 일부를 다른 객체에 넘기는 것**

```swift
extension ViewController: UITextFieldDelegate {

		func textFieldShouldReturn(_ textField: UITextField) -> Bool {
		      label.text = textField.text
		      return true
		}
}
```

- `UITextFieldDelegate` 를 채택하고 리턴키가 작동될 때 호출되는 `textFieldShouldReturn` 메소드 안에서 처리할 코드를 작성

```swift
textField.delegate = self
```

- 역할을 넘겨 누가 수행할 것인지에 대해 작성
- 이 delegate은 self(=ViewController)가 수행할 것이란 의미

### retain

- 메모리가 해제되지 않아서 **낭비**되는 현상을 의미 (Memory Leak, 메모리 누수)
- **Retain은 객체를 만들어냈을때 즉 ,인스턴화를 시켜줄때 생김**
- **인스턴스는 클래스로부터 생성된 객체**

## Delegate은 retain될까?

- **Delegate는 Protocol을 채택 → class가 아님 → retain안되겠군 → 아님!**
- **프로토콜을 채택할 때는 Class - Only - Protocol 이라는 클래스 전용 프로토콜을 사용해야함 
→프로토콜이 class타입으로 바뀌게 됨 → retain 됨**
- `weak`를 사용해 retain 방지함

### Reference

[https://fomaios.tistory.com/entry/iOS-면접질문-Delegate는-retain이-될까](https://fomaios.tistory.com/entry/iOS-%EB%A9%B4%EC%A0%91%EC%A7%88%EB%AC%B8-Delegate%EB%8A%94-retain%EC%9D%B4-%EB%90%A0%EA%B9%8C)

</div>
</details>




<details>
<summary> NotificationCenter 동작 방식과 활용 방안에 대해 설명하시오. </summary>
<div markdown="1">

### `NotificationCenter`란?

- observer(관찰자)에게 정보를 전달해주는 알림 발송 메커니즘

<br>

### 언제 Notification 센터를 사용?

- 앱 내에서 공식적인 연결이 없는 두 개 이상의 컴포넌트들이 상호작용이 필요할 때
- 상호작용이 반복적으로 그리고 지속적으로 이루어져야 할 때
- 일대다 또는 다대다 통신을 사용하는 경우

<br>

### 1. `Observer`(관찰자) 등록

```swift
NotificationCenter.default.addObserver(
            self,
            selector: #selector(scrollToBottom), // 알림을 받을 때 수행할 action
            name: NSNotification.Name("TestNotification"),
            object: nil
)
```

- 알림을 받고 싶은 부분에 observer를 등록한다.

<br>

### 2. 알림 발송

```swift
NotificationCenter.default.post(
name: NSNotification.Name("TestNotification"),
 object: nil
)
```

- observer에게 알림을 발송한다. 이때 object에 데이터도 함께 전달할 수 있다.

<br>

### 3. `Observer` 제거

```swift
NotificationCenter.default.removeObserver(
            self,
            name: NSNotification.Name("TestNotification"),
            object: nil
)
```

- observer를 제거하지 않으면 메모리에 계속 남아있게 때문에 remove해준다.

<br>

### +`extension`을 활용하여 NotificationName 관리

```swift
extension Notification.Name {
    static let testNotification = Notification.Name("TestNotification")
}
```

```swift
NotificationCenter.default.post(
		name: .testNotification,
		 object: nil
)
```

- `Notification.Name` 에게 익스텐션을 붙여주면 코드가 간결해지고 휴먼 에러를 줄일 수 있다.

<br>

</div>
</details>



- App Bundle의 구조와 역할에 대해 설명하시오.
<details>
<summary> 모든 View Controller 객체의 상위 클래스는 무엇이고 그 역할은 무엇인가? </summary>
<div markdown="1">

```
📍 모든 View Controller 객체의 상위 클래스는 UIViewController

- 뷰의 내용 업데이트
- 뷰와 사용자의 상호작용에 응답
- 뷰의 크기 조정 & 전체적인 레이아웃 관리

```
</div>
</details>






<details>
<summary>자신만의 Custom View를 만들려면 어떻게 해야하는지 설명하시오. </summary>
<div markdown="1">

## 1. xib 사용

<img width="311" alt="image" src="https://user-images.githubusercontent.com/77915491/222644391-e9fe4364-9c48-4df2-8dec-5623e9935e2e.png">

swift, xib파일을 만들어 사용하려는 UIView의 클래스를 CustomView로 연결

## 2. code로만 구현

### UIView를 상속한 CustomView

```swift
class CustomView: UIView {

    override init(frame: CGRect) {
        super.init(frame: frame)
        print(#function)
        loadView()
    }
    
    required init?(coder: NSCoder) {
        super.init(coder: coder)
        print(#function)
        loadView()
    }
    
    private func loadView() {
        let purpleView = makeView()
        purpleView.frame = CGRect(x: 0, y: 0, width: bounds.width, height: 30)
        addSubview(purpleView)
        
        let label = makeLabel()
        label.frame = CGRect(x: 0, y: 50, width: bounds.width, height: 20)
        addSubview(label)
    }
    
    private func makeView() -> UIView {
        let view = UIView()
        view.backgroundColor = .purple
        return view
    }
    
    private func makeLabel() -> UILabel {
        let label = UILabel()
        label.text = "커스텀2"
        label.textAlignment = .center
        return label
    }
}
```

### ViewController

```swift
class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        
        let customView = CustomView(frame: CGRect(x: 0, y: 300, width: UIScreen.main.bounds.width, height: 200))
        
        view.addSubview(customView)
    }
}
```

</div>
</details>


- View 객체에 대해 설명하시오.
- UIView 에서 Layer 객체는 무엇이고 어떤 역할을 담당하는지 설명하시오.
- UIWindow 객체의 역할은 무엇인가?
- UINavigationController 의 역할이 무엇인지 설명하시오.

<details>
<summary>TableView를 동작 방식과 화면에 Cell을 출력하기 위해 최소한 구현해야 하는 DataSource 메서드를 설명하시오. </summary>
<div markdown="1">

## TableView의 Datasource와 Delegate
<img width="704" alt="image" src="https://user-images.githubusercontent.com/77915491/224035017-8814dcc1-0ac3-4228-b12d-a005352e16b2.png">


- DataSoruce - 데이터를 받아 이를 뷰에 그려주는 역할
- Delegate - 사용자가 보이는 것들 중 무언가에 대한 액션을 취한다면 그에 대한 동작 수행

<br>

## UITableViewDataSource 프로토콜 정의

```swift
@MainActor public protocol UITableViewDataSource : NSObjectProtocol {

    
    @available(iOS 2.0, *)
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int

    
    // Row display. Implementers should *always* try to reuse cells by setting each cell's reuseIdentifier and querying for available reusable cells with dequeueReusableCellWithIdentifier:
    // Cell gets various attributes set automatically based on table (separators) and data source (accessory views, editing controls)
    
    @available(iOS 2.0, *)
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell

    
    @available(iOS 2.0, *)
    optional func numberOfSections(in tableView: UITableView) -> Int // Default is 1 if not implemented

    
    @available(iOS 2.0, *)
    optional func tableView(_ tableView: UITableView, titleForHeaderInSection section: Int) -> String? // fixed font style. use custom view (UILabel) if you want something different

    @available(iOS 2.0, *)
    optional func tableView(_ tableView: UITableView, titleForFooterInSection section: Int) -> String?

    
    // Editing
    
    // Individual rows can opt out of having the -editing property set for them. If not implemented, all rows are assumed to be editable.
    @available(iOS 2.0, *)
    optional func tableView(_ tableView: UITableView, canEditRowAt indexPath: IndexPath) -> Bool

    
    // Moving/reordering
    
    // Allows the reorder accessory view to optionally be shown for a particular row. By default, the reorder control will be shown only if the datasource implements -tableView:moveRowAtIndexPath:toIndexPath:
    @available(iOS 2.0, *)
    optional func tableView(_ tableView: UITableView, canMoveRowAt indexPath: IndexPath) -> Bool

    
    // Index
    
    @available(iOS 2.0, *)
    optional func sectionIndexTitles(for tableView: UITableView) -> [String]? // return list of section titles to display in section index view (e.g. "ABCD...Z#")

    @available(iOS 2.0, *)
    optional func tableView(_ tableView: UITableView, sectionForSectionIndexTitle title: String, at index: Int) -> Int // tell table which section corresponds to section title/index (e.g. "B",1))

    
    // Data manipulation - insert and delete support
    
    // After a row has the minus or plus button invoked (based on the UITableViewCellEditingStyle for the cell), the dataSource must commit the change
    // Not called for edit actions using UITableViewRowAction - the action's handler will be invoked instead
    @available(iOS 2.0, *)
    optional func tableView(_ tableView: UITableView, commit editingStyle: UITableViewCell.EditingStyle, forRowAt indexPath: IndexPath)

    
    // Data manipulation - reorder / moving support
    
    @available(iOS 2.0, *)
    optional func tableView(_ tableView: UITableView, moveRowAt sourceIndexPath: IndexPath, to destinationIndexPath: IndexPath)
}
```

`func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int`

`func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell`

위 메소드 두가지는  `optional` 이 붙지 않아 필수적으로 구현해야 한다.

```swift
  override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
   return 0
}
```

- 각 섹션에 표시할 행의 개수를 묻는 메서드

```swift
override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
 
   let cell = tableView.dequeueReusableCell(withIdentifier: "cellTypeIdentifier", for: indexPath)
   cell.textLabel!.text = "Cell text"
       
   return cell
}
이 프로토콜의
```

- 특정 위치에 표시할 셀을 리턴하는 메서드

<br>
<br>

</div>
</details>


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


<details>
<summary>hugging, resistance에 대해서 설명하시오.</summary>
<div markdown="1">

```
 - 뷰의 제약사항을 걸어줄 때 우선순위 지정

📌 hugging priority
	- hugging이 크면 자신의 크기 유지, 작으면 크기가 커짐

📌 resistance priority
	- resistance가 크면 자신의 크기 유지, 작으면 크기가 작아짐

```
</div>
</details>


<details>
<summary>오토레이아웃을 코드로 작성하는 방법은 무엇인가? (3가지)</summary>
<div markdown="1">

## 1. `Anchor` 사용하기

```swift
myView.leadingAnchor.constraint(equalTo: margins.leadingAnchor).active = true
myView.trailingAnchor.constraint(equalTo: margins.trailingAnchor).active = true
```

<br>

## 2. `NSLayoutConstraints` 사용하기

```swift
NSLayoutConstraint.activate([
            navigationBarView.topAnchor.constraint(equalTo: view.topAnchor),
            navigationBarView.leadingAnchor.constraint(equalTo: view.safeAreaLayoutGuide.leadingAnchor),
            navigationBarView.trailingAnchor.constraint(equalTo: view.safeAreaLayoutGuide.trailingAnchor),
            navigationBarView.heightAnchor.constraint(equalToConstant: 76)
        ])
```

<br>

## 3. `Visual Format` 사용하기

```swift
let views = ["redView": redView,
             "blueView": blueView,
             "greenView": greenView]

let format1 = "V:|-[redView]-8-[greenView]-|"
let format2 = "H:|-[redView]-8-[blueView(==redView)]-|"
let format3 = "H:|-[greenView]-|"

var constraints = NSConstraint.constraints(withVisualFormat: format1,
                    options: alignAllLeft,
                    matrics: nil,
                    views: views)
constraints += NSConstraint.constraints(withVisualFormat: format2,
                    options: alignAllTop,
                    matrics: nil,
                    views: views)
constraints += NSConstraint.constraints(withVisualFormat: format3,
                    options: []
                    matrics: nil,
                    views: views)
NSConstraint.activateConstraints(constraints)
```

- 마치 아스키 아트처럼 보이는 문자열을 이용해서 제약요소값들을 생성하는 방식
- 완전성보다는 좋은 시각화에 집중한 방식

<br>

### +`SnapKit` 라이브러리 사용

```swift
redBox.snp.makeConstraints { (make) in
            make.width.height.equalTo(100) 
            make.center.equalToSuperview()
}
```

<br>

</div>
</details>


<details>
<summary>Intrinsic Size에 대해서 설명하시오.</summary>
<div markdown="1">

## **intrinsic content size란?**

- 보통 UILabel의 사이즈는 따로 지정하지 않아도 에러가 뜨지 않는다. 
why? → 콘텐츠의 크기만큼 기본사이즈가 있기 때문
- **intrinsic content size == 고유 콘텐츠 크기**

<br>

## 만약에 고유 콘텐츠 크기에서 height만 늘리고 싶다면?

```swift
class Button: UIButton {
	override var intrinsicContentSize: CGSize {
			let height = self.contentSize.height + 10
			return CGSize(width: self.contentSize.width, height: height)
	}
}
```

- `intrinsicContentSize` 를 오버라이딩하고 height만 현재 크기에서 원하는 크기만큼 늘려준다.
<br>

</div>
</details>

<details>
<summary>Left Constraint 와 Leading Constraint 의 차이점을 설명하시오.</summary>
<div markdown="1">

### leading / trailing

- 글자가 시작하는 방향 / 글자가 끝나는 방향

### left / right

- 화면 기준 왼쪽 / 화면 기준 오른쪽

**leading, trailing을 권장**함 왜일까?

<img width="698" alt="image" src="https://user-images.githubusercontent.com/77915491/223102322-8a1795e4-ad94-465a-9445-36575695772f.png">

우리나라는 상관없지만 **아랍어**는 **오른쪽에서 왼쪽**으로 읽으므로 leading, trailing을 써 
사용자 경험에 차이가 없게 구현
<br>
<br>
</div>
</details>


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


<details>
<summary>mutating 키워드에 대해 설명하시오. </summary>
<div markdown="1">

```
📌 mutating
struct, enum 같은 값 타입은 인스턴스 메소드 내부에서 수정x
따라서 값 타입 속성을 수정할 때 mutating 키워드 사용
```

```swift
struct Point {
	var x = 0.0, y = 0.0
    
	mutating func moveXY(x: Double, y: Double {
		self = Point(x: self.x + x, y: self.y + y)
	}
}
```

</div>
</details>



<details>
<summary>Convenience init에 대해 설명하시오.</summary>
<div markdown="1">

```
📌 Convenience init
	- 보조 이니셜라이저로, 클래스의 원래 이니셜라이저인 init을 도와주는 역할
	- 같은 클래스에서 다른 이니셜라이저를 호출해야함
	- init의 파라미터 중 일부를 기본값을 설정해서, convenience init안에서 init을 호출하여 초기화 진행할 수 있음

```

```swift
class Person {
    var name: String
    var age: Int
    var gender: String

    init(name: String, age: Int, gender: String) {
        self.name = name
        self.age = age
        self.gender = gender
    }
		
		convenience init(age: Int, gender: String) {
        self.init(name: "zedd", age: age, gender: gender)
    }
}
```

</div>
</details>



<details>
<summary> class의 성능을 향상 시킬수 있는 방법들을 나열해보시오. </summary>
<div markdown="1">

```

- heap보다는 stack메모리를 할당하려고 노력
    * class보단 struct나 enum을 사용
    * class는 heap할당, struct나 enum은 stack할당

- referecn counting을 적게 만듦
    * 클래스에서 스트링 타입의 변수 사용을 줄임
    * string은 struct타입이지만 문자열의 콘텐츠를 heap에 저장하기 때문

- dynamic dispatch(런타임에 정해짐)(다형성때문에 사용)보다 static dipatch(컴파일 타임에 정해짐)를 지향
    * 클래스를 선언할 때 상속되지 않는 클래스에 final을 붙이면 성능이 향상

```
</div>
</details>

<details>
<summary>Copy On Write는 어떤 방식으로 동작하는지 설명하시오. </summary>
<div markdown="1">

```
📌 Copy On Write 동작방식
값타입의 데이터는 값을 참조하지 않고 복사함 
But 매번 복사 -> 값이 변경될 필요가 없어도 새로운 메모리 공간을 할당 -> 메모리 낭비, 오버헤드

따라서 Copy on write 사용
-> 데이터 복사하면 실제로 값을 복사x 동일한 값을 참조함
-> 값이 변경(Write)될 때, 값을 복사해 변경을 적용

즉, 데이터 복사 시 실제로 값을 복사하지 않고
동일한 값을 참조하다가 데이터 변경이 발생될 시에 복사해 값을 변경하는 기법
```
</div>
</details>

<details>
<summary> Optional 이란 무엇인지 설명하시오. </summary>
<div markdown="1">

```
📌 Optional
nil을 사용할 수 있는 타입과 사용할 수 없는 타입을 구분하고, 사용할 수 있는 타입을 가리켜 옵셔널 타입이라고 부름

* 자료형 뒤에 ?를 붙여 옵셔널 타입으로 만듦
* nil은 값이 없음을 의미하는 값


```
</div>
</details>

<details>
<summary> Struct 가 무엇이고 어떻게 사용하는지 설명하시오. </summary>
<div markdown="1">

```
📌 struct

구조체란, 인스턴스의 값(프로퍼티)을 저장하거나, 기능(메소드)를 제공하고 이를 캡슐화할 수 있도록 스위프트가 제공하는 타입

📌 Struct 사용 권장
애플은 다음 조건 중 하나 이상에 해당한다면 구조체를 사용하는 것을 권장
1. 연관된 간단한 값의 집합을 캡슐화하는 것만이 목적일 때
2. 캡슐화한 값을 참조하는 것보다 복사하는 것이 합당할때
3. 구조체에 저장된 프로퍼티가 value 타입이며 참조하는 것보다 복사하는 것이 합당할 때
4. 다른 타입으로부터 상속받거나 자신을 상속할 필요가 없을 때


```

```swift

struct [구조체 이름] { 
    [프로퍼티와 메서드들]
}

```
</div>
</details>



<details>
<summary>String은 왜 subscript로 접근이 안되는지 설명하시오. </summary>
<div markdown="1">

### 애플문서에 따르면 `String`은 `유니코드 문자열 값`이기 때문

- 유니코드는 `가변 길이 문자 인코딩`으로 눈에 보이는 문자열이 하나더라도 실제 길이는 다름
- ex) 🥰같은 이모지는 보이는 건 하나지만 실제로 print해보면 여러 개의 unicodeScalars가 찍힘
- 따라서 `Int`로는 `subscript`를 사용할 수 없는 것

<br>

만약에 String의 subscript를 사용하고 싶다면 

```swift
let str = "hello sun"
let index = str.index(str.startIndex, offsetBy: 2)
print(str[index])
```

`String.Index`로 subscript를 사용해주면 됨

<br>

</div>
</details>

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
- 탈출 클로저에 대하여 설명하시오.
<details>
<summary> Extension에 대해 설명하시오. </summary>
<div markdown="1">

```
📌 extension
- 기존 존재하는 클래스,구조체,열거형,프로토콜 타입에 새로운 기능을 추가할 수 있게 해줌
- 내부 소스를 접근할 수 없는 원본 타입들에 대해 새로운 기능을 부여할 수 있고, 특정 타입의 기능 및 준수하는 프로토콜별 구현부를 분리 -> 가독성 높일 수 있음

```

</div>
</details>

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

<details>
<summary> Strong 과 Weak 참조 방식에 대해 설명하시오. </summary>
<div markdown="1">

```
강한참조(Strong)
- 레퍼런스 카운트가 증가됨

약한참조(Weak)
- 객체를 참조하고 레퍼런스 카운트에 변화 없음
- ARC에서 자동으로 객체의 메모리 해제시켜줌
(참고 https://velog.io/@wook4506/iOS-Swift-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EC%B0%B8%EC%A1%B0-%EB%B0%A9%EB%B2%95-strong-weak-unowned)

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

<details>
<summary> 의존성 주입에 대하여 설명하시오. </summary>
<div markdown="1">

```
📌 의존성이란?
- 의존성은 쉽게 말해 함수에 필요한 클래스나 참조 변수에 의존하는 것
```

(1) B클래스가 A클래스에 의존성이 있는 경우

```swift
class A{
    var num: Int = 1
}

class B{
    var internalVariable = A()
}

let b = B()
print(b.internalVariable.num) // 1
```

```
B클래스는 A클래스를 내부에 변수로 사용하고 있음
이로써 B클래스는 A클래스에 의존성이 생김
-> 만일 A클래스에 문제가 생긴다면 이를 의존하고 있는 B클래스에도 문제가 생길 수 있어 재사용성이 낮아짐
```

(2) 주입 (injection)

```swift
class A{
    var num: Int

    init(num : Int){
        self.num = num
    }

    func setNum(num: Int){
        self.num = num
    }
}

let a = A(Int(3)) // 외부에서 객체 생성
print(a.num)

a.setNum(Int(5)) // 객체 생성
```

```
내부가 아닌 외부에서 객체를 생성해서 넣어주는 것을 주입
-> 외부에서 객체를 생성해 주입시킴
```



(3) 의존성 주입 (dependency injection) -> 하지만 DIP는 만족하지 않음

```swift
class A{
    var aNum: Int = 1
}
class B{
    var bNum: A
    init(num: A){
        self.bNum = num
    }
}
let b = B(A())
```

```
의존 관계 역전 법칙 (DIP)
1. 상위 모듈은 하위 모듈에 의존해서는 안된다. 상위 모듈과 하위 모듈 모두 추상화에 의존해야 한다.
2. 추상화는 세부 사항에 의존해서는 안된다. 세부사항이 추상화에 의존해야 한다.

```



(4) DIP 만족하는 의존성 주입

```swift
protocol DIInterface: AnyObject{
    var num: Int{get set}
}
class A: DIInterface{
    var aNum = 1
}
class B{
    var bNum: DIInterface
    init(num: DIInterface){
        self.bNum = num
    }
}

let b = B(A())
```

```
A, B 객체가 모두 의존(A → 프로토콜 ← B)하고 있는 구조
```

[참고](https://silver-g-0114.tistory.com/143)


</div>
</details>


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

