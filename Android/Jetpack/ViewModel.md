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
![viewModel생명주기](https://github.com/KyungHwa0/TIL/assets/124041716/affe0603-4419-4c7b-876e-1c06bc921a95)


### ViewModel은 언제 종료되는가??
Activity가 더이상 사용하지 않는 상태가 되었을 때, onCleared() 를 호출하려 내부 데이터를 초기화하고 파괴한다.

## ViewModel 프로세스
![ViewModel 프로세스](https://github.com/KyungHwa0/TIL/assets/124041716/3ce60eff-6a75-47df-b30e-321c462b2f5d)
```kotlin
ViewModelProvider (ViewModelStoreOwner owner, ViewModelProvider.Factory factory)
```
- 첫번째 매개변수는 ViewModelStoreOwner인데 ViewModelStore의 정보를 가지고 온다.
ViewModelStore는 ViewModel이 어떤 Activity와 연관이 있나를 알고 있는 얘로
Activiy나 Fragment를 넣어주면 된다.
- 두번째 매개변수는 ViewModelProvider.Factory로 실질적으로 ViewModel 인스턴스를 생성하는 역할을 하는 factory를 넣어 주면 된다. (여기서 알 수 있듯이 ViewModel은 팩토리패턴으로 구현된다!)

## ViewModel 구현하기
### 1. 클래스 정의
- MyViewModel.kt
```kotlin
class MyViewModel : ViewModel(){
    private val users: MutableLiveData<List<User>> by lazy {
        MutableLiveData<List<User>>().also {
            loadUsers()
        }
    }

    fun getUsers(): LiveData<List<User>> {
        return users
    }

    private fun loadUsers() {
        // Do an asynchronous operation to fetch users.
    }
  }
```
### 2. ViewModel 객체 생성
#### 1. Android Devlepers 에 나와있는 방법으로 커스텀은 불가능
```kotlin
class MyActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        val myViewModel: MyViewModel by viewModels()
    }
}
```

#### 2. ViewModelProvider 사용
gradle에 lifecycle에 대한 의존성을 추가해 주어야 사용할 수 있음

```kotlin
class MyActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        val myViewModel = ViewModelProvider(this).get(MyViewModel::class.java)
    }
}

```

#### 3. ViewModelProvider.NewInstanceFactory 사용
안드로이드에서 제공해주는 팩토리 클래스. ViewModel에 파라미터가 없을 경우 사용하면 되고 의존성 주입은 필요 없음
```kotlin
class MyActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        val myViewModel = ViewModelProvider(this, ViewModelProvider.NewInstanceFactory())
            .get(MyViewModel::class.java)
    }
}
```
#### 4. ViewModelProvider.Factory 사용
ViewModel에 파라미터가 있을 경우, 직접 Factory 클래스를 만들어서 사용하는 방법
- ViewModelFactory.kt
```kotlin
class ViewModelFactory(private val param: String) : ViewModelProvider.Factory {
    override fun <T : ViewModel> create(modelClass: Class<T>): T {
        return if (modelClass.isAssignableFrom(MyViewModel::class.java)) {
            MyViewModel(param) as T
        } else {
            throw IllegalArgumentException()
        }
    }
}

```
- MainActivity.kt
```kotlin
class MyActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        val myViewModel = ViewModelProvider(this, ViewModelFactory("wagzack"))
            .get(MyViewModel::class.java)
    }
}

```


