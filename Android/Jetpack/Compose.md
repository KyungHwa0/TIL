# Jetpack Compose 란?
``Jetpack Compose``는 Android 응용 프로그램의 사용자 인터페이스(UI)를 더 쉽게 작성하고 관리할 수 있게 해주는 최신 도구이다. 이는 과거의 XML 기반 Layout 또는 View와 비교되며, 선언적이고 프로그래밍적으로 유연하게 UI를 작성할 수 있게 해준다.
> 기존의 뷰를 업데이트하는 방식과 달리 ``Compose``를 사용하면 필요한 영역의 뷰를 다시 그려주는 방식으로 작업할 수 있다.

## Jetpack Compose의 특징

### 선언적 UI 
개발자는 UI의 현재 상태를 설명하고 **Compose**가 자동으로 UI를 업데이트하도록 한다. 이로 인하여 UI와 데이터 사이의 **일관성**이 유지되고 코드를 읽기 쉬워지며 **유지보수** 또한 쉬워진다.
### 리액티브 UI
데이터와 UI 간의 관계를 관리하기 위해 **리액티브 프로그래밍** 원칙을 사용한다. 상태 변경으로 인해 자동으로 UI 업데이트를 유도하므로 개발자는 복잡한 UI 동작을 쉽게 다룰 수 있다.
### 컴포저블(Composable)
UI의 구성 요소를 나타내는 **Composable** 함수를 작성한다. ``@Composable`` 어노테이션을 사용하여 **Composable** 함수를 정의하고, 이러한 함수들의 조합으로 UI를 작성하게 된다.
### 재사용성 및 모듈성
재사용 가능한 컴포넌트를 쉽게 작성하고 조합할 수 있도록 도와준다. 이로써 UI 코드를 **모듈화**하고 **재사용** 가능한 UI 요소를 만들 수 있다.
### Material
Google의 **Material Design** 가이드라인과의 완벽한 통합으로 **Material Design**에 따라 아름답고 일관된 UI를 만들 수 있다.
### Android 호환성
Android의 기존 View 시스템과 통합되므로 기존 Android 응용 프로그램에서도 사용할 수 있다. 기존 Android 응용 프로그램을 점진적으로 업데이트할 수도 있다.

## Jetpack Compose에서 자주 사용되는 요소
### Text
텍스트를 표시하기 위한 Composable
### Image 
이미지를 표시하고 조작하기 위한 Composable
### Layouts 
다양한 레이아웃을 정의하기 위한 Composable
* Column : **세로**로 배치
* Row : **가로**로 배치
* Box : 요소를 다른 요소 위에 놓는다.
* ConstraintLayout : 화면에 다른 컴포저블을 **기준**으로 컴포저블을 배치할 수 있는 레이아웃. 복잡한 정렬 요구사항이 있는 더 큰 레이아웃을 구현할 때 사용
### Material Design 컴포넌트
**Material Design** 스타일의 UI 요소를 작성하기 위한 Composable
* Button, TextField, AppBar, BottomNavigation 등
### State 관리
**상태를 관리**하기 위한 Composable 함수로, **remember** 함수를 사용하여 상태를 정의하고 관리
### Navigation
응용 프로그램 내에서 ``화면 간의 이동``을 관리하기 위한 Composable로 **NavHost** 및 **NavController**를 사용

---

### Compose Study 
[https://github.com/KyungHwa0/Compose](https://github.com/KyungHwa0/Compose)

