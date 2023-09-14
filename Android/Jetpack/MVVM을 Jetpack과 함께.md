# MVVM
* Model: 애플리케이션의 데이터와 비즈니스 로직을 담당
* View: 사용자에게 보여지는 UI를 담당
* ViewModel: View와 Model 사이의 데이터를 처리하며, UI와 관련된 비즈니스 로직을 담당

## Jetpack과 MVVM 연관성
1. ViewModel: Jetpack의 ViewModel 클래스를 사용하면 UI 관련 데이터를 관리하고 저장하는데 도움을 받을 수 있다. 이는 화면 회전과 같은 구성 변경 중에 데이터를 유지하게 도와준다.

2. LiveData: LiveData는 관찰 가능한 데이터 홀더 클래스로, 생명주기를 인식한다. 데이터 변경이 발생하면 View가 자동으로 업데이트된다.

3. Data Binding: Jetpack의 Data Binding 라이브러리를 사용하면 UI 구성 요소를 직접 코드로 참조하지 않고 XML 레이아웃에서 데이터를 직접 바인딩할 수 있다.

4. Room: Room은 SQLite의 추상화 레이어를 제공하는 Jetpack의 데이터베이스 라이브러리로, MVVM의 Model 부분에 해당하는 데이터베이스 작업을 쉽게 할 수 있도록 돕는다.

