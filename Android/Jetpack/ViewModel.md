>ViewModel에는 MVVM 패턴 에서 언급되는 ViewModel과,
테스트와 유지보수가 쉬운 앱을 만들 수 있도록 도와주는 AAC(Android Architecture Components) ViewModel

### MVVM 패턴의 ViewModel
View와 Model 사이의 매개체 역할을 하고 View에 보여지게 되는 데이터를 가공하는 역할

### AAC의 ViewModel
앱의 Lifecycle을 고려하여 UI 관련 데이터를 저장하고 관리하는 역할

# ViewModel 이란?
Activity와 fragment와 같은 UI 컨트롤러의 로직에서 데이터를 다루는 로직을 분리하기 위해 등장한 Android JetPack 라이브러리

## 분리하는 이유
### 1. UI 컨트롤러의 목적
데이터를 표시해주거나, 사용자가 어떤 작업을 했을때 반응을 보여주거나, 권한 요청과 같은 OS커뮤니케이션을 처리하는 것이 UI컨트롤러의 목적

따라서, UI 컨트롤러에서 데이터를 다루는 로직을 책임지게 되면 많은 유지보수가 필요한 비동기 호출과 같은 작업들을 해야하기 때문에 UI 컨트롤러에 과도한 책임이 생기게 됨

### 2. 데이터 손실 방지
UI 컨르롤러에서는 생명주기에 따라 앱이 활동중에 제거될 때마다 데이터를 저장시키고, 다시 생성될 때마다 데이터들을 다시 불러와야 한다.

## ViewModel의 생명주기
Activity의 생명주기와 상관없이 살아있다면 데이터가 쭉 유지되면 데이터의 손실을 방지할 수 있을 것이다. 그래서 ViewModel은 Activity의 생명주기 보다 긴 수명을 가지는 생명주기를 갖게 된다.
ViewModel의 Scope(생명주기의 범위)는 ViewModel을 가져올 때 ViewModelProvider에 의해 결정 된다.  
<그림>

### ViewModel은 언제 종료되는가??
Activity가 더이상 사용하지 않는 상태가 되었을 때, onCleared() 를 호출하려 내부 데이터를 초기화하고 파괴한다.


