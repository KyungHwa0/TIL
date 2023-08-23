# 뷰 바인딩 (View Binding)
* 뷰와 상호작용하는 코드를 쉽게 작서할 수 있다.
* 모듈에서 사용 설정된 뷰 바인딩은 모듈에 있는 각 XML 레이아웃 파일의 결합 클래스를 생성한다.
* 바인딩 클래스의 인스턴스에는 상응하는 레이아웃에 ID가 있는 모든 뷰의 직접 참조가 포함된다.
* 대부분의 경우 뷰 바인딩이 findViewById를 대체한다.

## findViewById 와의 차이점
### 1. NullSafe
* 뷰 바인딩은 뷰의 Direct References 즉 직접 참조를 생성하므로 유효하지 않은 뷰ID로 인해 null포인터 예외(NPE)가 발생 할 위험이 없다.
* 즉, 레이아웃에 아직 생성되지 않은 뷰의 참조를 얻어(null상태)해당 뷰의 속성을 사용하려 할 때 발생하는 NPE를 방지 한다는 것이다.
* 레이아웃의 일부 구성에만 뷰가 있는 경우 결합 클래스에서 참조를 포함하는 필드가@Nullable로 표시된다.
### 2. Type safety
* 각 바인딩 클래스에 있는 필드의 유형이 XML파일에서 참조하는 뷰와 일치한다.
* 즉,클래스 변환 예외가 발생할 위험이 없다.
* 쉽게말해 타입을 가지고 있기 때문에 imageView.text같이 타입이 다른 경우 발생하는 오류를 방지 할 수 있다.

## 코틀린에서 뷰바인딩 설정 방법
### 1. gradle 설정
```kotlin
android{
	...
    
    // AndroidStudio 3.6 ~ 4.0
    viewBinding{
    	enabled = true
    }
    
    // AndroidStudio 4.0 ~
    buildFeatures{
    	viewBinding = true
    }
}
```
### 2. Activity에서 설정
```kotlin
class MainActivity : AppCompatActivity() {
    // 뷰 바인딩
    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        // 뷰 바인딩
        binding = ActivityMainBinding.inflate(layoutInflater)
        val view = binding.root
        setContentView(view)
    }
}
```

## 뷰 바인딩의 예제
### LayoutXML
```kotlin
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/myTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/myButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="32dp"
        android:text="Button"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/myTextView" />

</androidx.constraintlayout.widget.ConstraintLayout>
```
### Activity
```kotlin
class MainActivity : AppCompatActivity() {

    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        binding.myButton.setOnClickListener{
            binding.myTextView.text = "바인딩이 잘 되네요!"
        }
    }
}
```
