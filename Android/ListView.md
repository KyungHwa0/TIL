# ListView
어댑터 뷰의 대표 위젯으로서, 복수 개의 항목을 수직으로 표시

### 📔간단한 리스트 뷰를 만들어보자.
#### 1. 메인화면 레이아웃에 ListView 위젯 정의
* res/layout/activity_main.xml
```kotlin
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <ListView
        android:id="@+id/listView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
       />
</LinearLayout>
```

#### 2. 어댑터 객체 생성
* 데이터 원본이 배열인 경우에 ArrayAdapter객체 사용
* String 배열을 이용한 ArrayAdapter 객체 생성 예제
```kotlin
class MainActivity : AppCompatActivity() {

    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        // 데이터 원본 준비
        val items = arrayOf<String?>("item1", "item2", "item3", "item4", "item5", "item6", "item7", "item8", "item5", "item6", "item7", "item8", "item5", "item6", "item7", "item8", "item5", "item6",  "item7", "item8")

        //어댑터 준비 (배열 객체 이용, simple_list_item_1 리소스 사용
        val adapter = ArrayAdapter(this, android.R.layout.simple_list_item_1, items)

   }
}
```
#### 3. ListView객체에 어댑터 연결
* 현재 화면 레이아웃(activity_main.xml)에 정의 된 뷰 중에서 id가 listView인 ListView 객체를 ViewBinding을 통해서 얻어온다.
* 얻어온 ListView객체에 생성된 어댑터 객체(예,ArrayAdapter객체-adapter)를 연결한다.
```kotlin
class MainActivity : AppCompatActivity() {

    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        // 데이터 원본 준비
        val items = arrayOf<String?>("item1", "item2", "item3", "item4", "item5", "item6", "item7", "item8", "item5", "item6", "item7", "item8", "item5", "item6", "item7", "item8", "item5", "item6",  "item7", "item8")

        //어댑터 준비 (배열 객체 이용, simple_list_item_1 리소스 사용
        val adapter = ArrayAdapter(this, android.R.layout.simple_list_item_1, items)

        // 어댑터를 ListView 객체에 연결
        binding.listView.adapter = adapter

    }
}
```
![ListView](https://github.com/KyungHwa0/TIL/assets/124041716/9c6631cd-eb9d-4b2d-aca0-233e1e8a0df3)

