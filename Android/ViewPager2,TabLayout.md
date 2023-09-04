# ViewPager2
스와이프로 화면전환을 할 수 있는 기존 ViewPager의 개선버전 ViewPager2는 기존 ViewPager 대비 기능 개선 및 세로 방향으로도 페이징이 되는 등의 장점이 있다. 
> ViewPager2를 사용해야 하는 이유는 구글에서 기존 ViewPager는 더 이상 개발 지원을 하지 않고, ViewPager2의 사용을 권고하고 있기 때문임.

## Gradle 설정
ViewPager2를 사용하기 위해 Gradle에 아래와 같이 추가
```
dependencies {
    ...
    implementation 'androidx.viewpager2:viewpager2:1.0.0'
}
```

## 각 뷰페이지에 등록할 Fragment 생성
* FirstFragment.kt
```kotlin
class FirstFragment : Fragment() {
    override fun onCreateView(
        inflater: LayoutInflater,
        container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        return inflater.inflate(R.layout.fragment_first, container, false)
    }

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
    }
}
```
* fragment_first.xml
```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".FirstFragment">
    <TextView
        android:id="@+id/textView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:gravity="center"
        android:background="#E53935"
        android:text="First Fragment"
        android:textSize="40dp"/>
</LinearLayout>
```

## FragmentStateAdapter를 상속받은 ViewPager2용 Adapter 생성
createFragment( ) 메소드에서는 각 화면에 나타낼 fragment를 생성하여 반환하고, getItemCount( ) 메소드에서는 화면에 나타낼 페이지 수를 반환해 줍니다. 

```kotlin
class ViewPager2 (
    fragmentManager: FragmentManager,
    lifecycle: Lifecycle
) : FragmentStateAdapter(fragmentManager, lifecycle) {
    override fun createFragment(position: Int): Fragment {
        return when(position) {
            0 -> FirstFragment()
            1 -> SecondFragment()
            else -> throw IllegalArgumentException("Invalid position: $position")
        }
    }

    override fun getItemCount(): Int {
        return 2 // 페이지 수
    }
}
```

## MainActivity에서 ViewPager2와 TabLayout 설정 등록
1. MainActivity Layout에서 ViewPager2와 TabLayout 화면을 구성. 
2. MainActivity에서 ViewPager2 객체를 생성하여 ViewPager2와 연결. 
3. TabLayout 사용을 위해서는 MainAcitivity에서 TabLayoutMediator( ) 객체를 생성한 후 TabLayout을 ViewPager2에 연결.

* MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val viewPager2Adapter = ViewPager2Adapter(supportFragmentManager, lifecycle)
        val viewPager2: ViewPager2 = findViewById(R.id.pager)
        viewPager2.adapter = viewPager2Adapter

        // TabLayout
        val tabLayout: TabLayout = findViewById(R.id.tabLayout)
        TabLayoutMediator(tabLayout, viewPager2) { tab, position ->
            tab.text = "Tab ${position + 1}"
        }.attach()
    }
}
```

* activity_main.xml
```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">
    <com.google.android.material.tabs.TabLayout
        android:id="@+id/tabLayout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />
    <androidx.viewpager2.widget.ViewPager2
        android:id="@+id/pager"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1" />
</LinearLayout>
```