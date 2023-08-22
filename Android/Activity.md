# 목차
[1. 액티비티](#activity)  
[2. 액티비티 생명주기](#activity-생명주기)

# Activity
* 사용자와 상호 작용 할 수 있는 화면을 제공하는 애플리케이션의 구성요소
    * ex) 전화걸기, 사진찍기, 이메일 보내기, 지도보기 등
* 액티비티마다 창(Window)이 하나 씩 주어져 이곳에 사용자 인터페이스를 끌어올(draw)수있다.
    * 사용자 인터페이스는View객체들로 구성
* 안드로이드앱은 화면에 UI를 표시하기 위해 최소 하나의Activity를 가져야 하며, 앱 실행시 지정된 Activity를 실행하여 사용자에게 UI를 표시

### 액티비티와 사용자 인터페이스 연결
setContentView()를 이용하여 액티비티에 사용자 인터페이스를 정의한View를 설정
![액티비티 연결](https://github.com/KyungHwa0/TIL/assets/124041716/db2b3129-ca09-45ef-9bb4-1d152fa91a39)

### 액티비티 등록
모든 Activity컴포넌트는 Android Manifest파일에 등록되어야 한다.
```kotlin
<manifest>
    <application>
        <activity android name=".FirstActivity"
        android:label="First Activity>
        </activity>
    </application>
</manifest>
```

### Android Manifest 역할
* 애플리케이션 패키지 이름 (애플리케이션의 고유한 식별자 역할) 설정
* 애플리케이션 구성요소들을 설명
* 이 애플리케이션과 상호작용하는 다른 애플리케이션이 가져야할 권한 설정
* 애플리케이션에서 사용하는 라이브러리 설정
* 애플리케이션이 필요로 하는 Android API의 최소 수준 설정

# Activity 생명주기
![액티비티생명주기](https://github.com/KyungHwa0/TIL/assets/124041716/abbee239-6a75-48b8-97ee-3dea70fb30b3)

### 액티비티의 수명
* onCreate()호출과 onDestroy()호출 사이에 있다.
    <details>
        <summary>onCreate()란?</summary>
            <div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;액티비티가 생성되어 레이아웃 설정 등을 수행</div>
    </details>
    <details>
        <summary>onDestroy()란?</summary>
            <div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;호출되는 시점에 사용하고 있는 리소스를 모두 해제하고 생을 마감</div>
    </details>

### 화면이 눈에 보이게 되는 Visibility
* onStart()에서 onStop()호출 사이에 있다.
* 이 기간 중에는 사용자가 액티비티를 화면에서 보고 이와 상호 작용 할 수 있다.
* onStop()이 호출되어 새 액티비티가 시작되면 이 액티비티는 더 이상 표시되지 않는다.
* 시스템은 액티비티의 전체 수명 내내 onStart() 및 onStop()을 여러 번 호출 할 수 있다.
* 이때 액티비티는 사용자에게 표시되었다 숨겨지는 상태를 오가게 된다.

### 액티비티가 foreground에서 동작하는 구간
* onResume()에서 onPause()호출 사이를 말한다.
* 이 기간 중에는 이 액티비티가 화면에서 다른 모든 액티비티 앞에 표시된다.
* 사용자 입력도 여기에 집중된다.
* 액티비티는 전경에 나타났다 숨겨지는 전환을 자주 반복할 수 있다.
* 예를 들어, 기기가 절전모드에 들어가거나 대화상자가 나타나면 onPause()가 호출된다.


### 생명주기 콜백 메소드
* 액티비티가 생성되면서 해제될 때 까지 액티비티의 상태에 따라서 불려지는 메소드를  라이프 사이클 콜백 메소드라 부른다.
* 애플리케이션 개발자는 필요한 경우에 해당 콜백 메소드를 재 정의하여 필요한 일을 수행하게 할 수 있다.
    <details>
        <summary>주요 콜백 메소드</summary>
                <ul>
                    <li>onCreate() : 반드시 구현해야 하는 메소드로서 액티비티가 생성되면서 호출된다.
                        <ul>
                            <li>가장 중요한 작업은 화면을 setContentView()를 호출하여 설정</li>
                        </ul>
                    </li>
                    <li>onPause() : 사용자가 액티비티를 떠나고 있을 때 호출된다.
                        <ul>
                            <li>액티비티가 완전히 소멸되는 것은 아니지만 사용자가 돌아오지 않을 수 있기 때문에 그 동안 이루어졌던 변경사항을 저장</li>
                        </ul>
                    </li>
                </ul>
    </details>

### 액티비티 전환 시 수명주기 콜백 메소드 호출 순서
#### FirstActivity에서 SecondActivity 시작
1. FirstActivity의 onPause()
2. SecondActivity의 onCreate() -> onStart() -> onResume()
3. FirstActivity의 onStop()

#### 단말기의 뒤로가기 버튼 누름
1. SecondActivity의 onPause()
2. FirstActivity의 onRestart(), onStart(), onResume()
3. SecondActivity의 onStop(), onDestroy()

#### 결과코드
```kotlin
class FirstActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_first)
        Log.i(TAG, “onCreate()")
        //생략..

    }
    val TAG = "FirstActivity_Lifrcycle"

    override fun onStart() {
        super.onStart()
        Log.i(TAG, "onStart()")
    }
    override fun onResume() {
        super.onResume()
        Log.i(TAG, "onResume()")
    }
    override fun onPause() {
        super.onPause()
        Log.i(TAG, "onPause()")
    }
    override fun onStop() {
        super.onStop()
        Log.i(TAG, "onStop()")
    }
    override fun onRestart() {
        super.onRestart()
        Log.i(TAG, "onRestart()")
    }
    override fun onDestroy() {
        super.onDestroy()
        Log.i(TAG, "onDestroy()")
    }
}
```
```kotlin
class SecondActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_second)
        Log.i(TAG, "onCreate()")
        // 생략..
    }

    val TAG = "SecondActivity_Lifrcycle"

    override fun onStart() {
        super.onStart()
        Log.i(TAG, "onStart()")
    }
    override fun onResume() {
        super.onResume()
        Log.i(TAG, "onResume()")
    }
    override fun onPause() {
        super.onPause()
        Log.i(TAG, "onPause()")
    }
    override fun onStop() {
        super.onStop()
        Log.i(TAG, "onStop()")
    }
    override fun onRestart() {
        super.onRestart()
        Log.i(TAG, "onRestart()")
    }
    override fun onDestroy() {
        super.onDestroy()
        Log.i(TAG, "onDestroy()")
    }
}
```