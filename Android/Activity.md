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
모든 Activity컴포넌트는 Android Manifest파일에 등록되어야 함
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