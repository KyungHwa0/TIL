# GridView
GridView는 2차원 스크롤 가능한 그리드에 항목을 표시

### 📔간단한 그리드 뷰를 만들어보자.

#### 1. 메인화면 레이아웃에 GridView 위젯 정의
* res/layout/activity_main.xml
```kotlin
<?xml version="1.0" encoding="utf-8"?>
<GridView xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/gridview"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:columnWidth="100dp"
    android:numColumns="auto_fit"
    android:verticalSpacing="10dp"
    android:horizontalSpacing="10dp"
    android:stretchMode="columnWidth"
    android:gravity="center"
    />
```
* **android:columnWidth=“100dp”** : 그리드 항목 하나의 폭을 100dp로 설정
* **android:numColumns=“auto_fit”** : 열의 폭과 화면 폭을 바탕으로 자동 계산
* **android:verticalSpacing** : 항목 간의 간격 설정
* **android:stretchMode=“columnWidth”** : 열 내부의 여백을 폭에 맞게 채움

#### 2. ArrayAdapter 객체를 생성하고 GridView 객체에 연결
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

        // 어댑터를 GridView 객체에 연결
        binding.gridView.adapter = adapter

    }
}
```
1. 간단한 리스트뷰 만들어 보기 예제와 마찬가지로, ArrayAdapter 객체를 생성
2. id를 바탕으로 메인화면 레이아웃(activity_main.xml)에 정의된 GridView 객체 로딩
3. 생성된 ArrayAdapter 객체를 GridView 객체에 연결
<img width="320" alt="그리드뷰" src="https://github.com/KyungHwa0/TIL/assets/124041716/e9e26fa4-57f4-4b4f-8c4e-d00aed3e3779">

### 📔간단한 이미지 그리드 뷰를 만들어보자.

#### 1. 메인화면 레이아웃에 GridView 위젯 정의
* res/layout/activity_main.xml
```kotlin
<GridView xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/gridview"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:columnWidth="100dp"
    android:gravity="center"
    android:horizontalSpacing="10dp"
    android:numColumns="auto_fit"
    android:stretchMode="columnWidth"
    android:verticalSpacing="10dp" />
```

#### 2. Adapter 정의
그리드 뷰의 항목으로 간단한 텍스트가 아닌 이미지를 사용하고자 하는 경우에는 그리드뷰의 항목으로 이미지를 공급하는 ImageAdapter를 BaseAdapter로부터 파생하여 정의한다.
```kotlin
class ImageAdapter : BaseAdapter() {
    override fun getCount(): Int {
        return mThumbIds.size
    }

    override fun getItem(position: Int): Any {
        return mThumbIds[position]
    }

    override fun getItemId(position: Int): Long {
        return position.toLong()
    }

    override fun getView(position: Int, convertView: View?, parent: ViewGroup?): View {
        val imageView: ImageView
        if (convertView == null) {
            imageView = ImageView(parent!!.context)
            imageView.layoutParams = AbsListView.LayoutParams(200, 200)
            imageView.scaleType = ImageView.ScaleType.CENTER_CROP
            imageView.setPadding(8, 8, 8, 8)
        } else {
            imageView = convertView as ImageView
        }

        imageView.setImageResource(mThumbIds.get(position))
        return imageView
    }

    private val mThumbIds = arrayOf<Int>(
        R.drawable.sample_2, R.drawable.sample_3,
        R.drawable.sample_4, R.drawable.sample_5,
        R.drawable.sample_6, R.drawable.sample_7,
        R.drawable.sample_0, R.drawable.sample_1,
        R.drawable.sample_2, R.drawable.sample_3,
        R.drawable.sample_4, R.drawable.sample_5,
        R.drawable.sample_6, R.drawable.sample_7,
        R.drawable.sample_0, R.drawable.sample_1,
        R.drawable.sample_2, R.drawable.sample_3,
        R.drawable.sample_4, R.drawable.sample_5,
        R.drawable.sample_6, R.drawable.sample_7
    )
}
```
* app>res>drawable 하위에 이름이 sample_0에서 sample_7까지인 8개의 이미지 파일을 추가한다.

* ImageAdapter가 관리하는 데이터는 편의상 직접 ImageAdapter 내부에 Image 리소스 ID의 배열로 설정
* BaseAdapter의 **getCount()**, **getItem()**, **getItemId()**, **getView()** 메소드를 재정의함
    * getCount()는 항목의 총 개수를 반환하기 위해 *mThumbIds* 배열의 크기를 반환
    * getItem()는 특정 위치의 항목을 반환하기 위해 *mThumbIds* 배열의 지정된 위치의 항목을 반환
    * getItemId()는 특정 위치의 항목 아이디를 반환하는 것인데, 여기서는 배열의 위치(순서)를 항목의 아이디로 간주한다.
    * getView()는 getView 메소드는 첫번째 파라미터로 주어진 위치의 항목 뷰를 반환하는 것이므로, *mThumbIds* 배열의 position 위치에 있는 이미지 리소스를 ImageView의 이미지로 설정하고, 이 설정된 ImageView 객체를 그리드 뷰의 항목뷰로 반환한다.
        * getView() 메소드의 두번째 파라미터인 convertView는 이전에 생성된 항목뷰 (여기서는 ImageView)를 의미한다. 만약 해당 위치의 항목뷰가 처음 만들어지는 경우라면, 새로운 이미지뷰 객체를 만들고 크기와 스케일타입, 패팅을 설정한다. 만약 이전에 이미 만들어진 것이라면, 이를 재사용한다.
        * 이미지 뷰의 scaleType은 원본 이미지를 이미지 뷰에 맞게 확대 및 축소시킬 때, 어떻게 처리할 지를 지정하는 것인데, 여기서 CENTER_CROP은 종횡비를 유지하여 스케일링하며 뷰의 크기 이상으로 채우게 됨을 의미한다. 따라서 이미지 일부가 잘릴 수 있다.

#### 3. Adapter를 생성하고 GridView객체에 연결
1. 그리드 뷰 설정의 마지막 단계는 ImageAdapter객체를 생성
2. 이를 GridView객체에 연결 하는 것
```kotlin
class MainActivity : AppCompatActivity() {

    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        // ImageAdapter 객체를 생성하고 GridView 객체에 연결
        binding.gridview.adapter = ImageAdapter()
    }
}
```
#### 4. 항목 클릭 이벤트 처리
```kotlin
class MainActivity : AppCompatActivity() {

    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        // ImageAdapter 객체를 생성하고 GridView 객체에 연결
        binding.gridview.adapter = ImageAdapter()

        // 항목 클릭 이벤트 처리 <- 추가된 내용
        binding.gridview.setOnItemClickListener{ parent, view, position, id ->
            Toast.makeText(this@MainActivity,"" + (position + 1) + "번째 선택",           
                Toast.LENGTH_SHORT).show()
        }
    }
}
```
<img width="320" alt="이미지그리드뷰" src="https://github.com/KyungHwa0/TIL/assets/124041716/06eeb169-6e27-4f66-bb4c-e6b238e1d849">


