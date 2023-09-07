# Fragment
Fragment는 Android 애플리케이션에서 사용자 인터페이스의 일부 또는 행동을 나타낸다. Fragment는 재사용 가능하며 여러 액티비티와 함께 존재할 수 있다. 특히 태블릿과 같은 큰 화면 크기에 대한 더 유연하고 적응적인 UI 디자인을 허용.

## Fragment를 사용하는 이유
* **모듈성**: 복잡한 UI를 더 작고 재사용 가능한 부분으로 분해
* **적응성**: 별도의 활동을 만들지 않고도 다양한 화면 크기에 맞게 UI를 조정한다.
* **재사용성**: 여러 활동에서 동일한 fragment를 사용한다.

## Fragment 생명주기
Activity와 마찬가지로 Fragment에는 생명주기 메서드가 있다.
- **`onCreate()`**
- **`onCreateView()`**
- **`onActivityCreated()`**
- **`onStart()`**
- **`onResume()`**
- **`onPause()`**
- **`onStop()`**
- **`onDestroyView()`**
- **`onDestroy()`**