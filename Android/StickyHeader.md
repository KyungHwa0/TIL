# StickyHeader
사용자 인터페이스 요소 (보통 리스트나 스크롤 뷰 내부의 헤더)가 화면 상단에 **붙어** 있게 만들 때 사용된다. 사용자가 내용을 스크롤해도 해당 헤더는 화면의 상단에 계속 머무르게 된다.

## StickyHeader의 사용 예
### 리스트에서의 구분
많은 양의 정보나 항목이 있는 목록에서, StickyHeader는 섹션의 시작이나 카테고리별로 헤더를 제공하여 사용자에게 현재 어떤 섹션을 보고 있는지 명확하게 알려준다.
### 핵심 정보 표시
정보가 많은 페이지에서, 중요한 정보나 액션 버튼 (예: "저장" 버튼)을 StickyHeader에 배치하여 사용자가 언제든지 접근할 수 있게 한다.
섹션 정보: StickyHeader에 현재 사용자가 진행 중인 섹션의 이름 (예: "개인 정보", "직업 관련", "취미 및 관심사")을 표시합니다. 이렇게 하면 사용자가 어느 섹션에 있는지 쉽게 인식할 수 있습니다.
1. 진행률: StickyHeader에 설문의 전체 진행률을 바나 숫자로 표시. (예: "진행률: 45%"). 사용자는 언제든지 현재 설문의 진행 상태를 파악할 수 있다.

2. 액션 버튼: "다음 섹션으로", "이전 섹션으로" 및 "저장" 버튼을 StickyHeader에 추가한다. 이렇게 하면 사용자가 설문의 어느 부분에 있든, 필요한 액션을 쉽게 수행할 수 있다.

3. 도움말 및 문의: StickyHeader에 도움말 아이콘 또는 문의 버튼을 배치하여, 사용자가 질문이나 문제가 발생했을 때 즉시 도움을 받을 수 있게 한다.
</br></br>

> **Android (Kotlin/Java)** **RecyclerView**에서 **StickyHeader** 효과를 구현하려면 추가 작업이 필요할 수 있다. 여러 오픈 소스 라이브러리가 이 기능을 제공하며, **ItemDecoration** 클래스를 활용하여 직접 구현할 수도 있다.

#### StickyHeader RecylerView
* StickHeaderItemDecoration.kt
```kotlin
class StickyHeaderItemDecoration(private val sectionCallback: SectionCallback) : ItemDecoration() {

    override fun onDrawOver(c: Canvas, parent: RecyclerView, state: RecyclerView.State) {
        super.onDrawOver(c, parent, state)

        val topChild = parent.getChildAt(0) ?: return

        val topChildPosition = parent.getChildAdapterPosition(topChild)
        if (topChildPosition == RecyclerView.NO_POSITION) {
            return
        }

        /* 헤더 */
        val currentHeader: View = sectionCallback.getHeaderLayoutView(parent, topChildPosition) ?: return

        /* View의 레이아웃 설정 */
        fixLayoutSize(parent, currentHeader, topChild.measuredHeight)

        val contactPoint = currentHeader.bottom

        val childInContact: View = getChildInContact(parent, contactPoint) ?: return

        val childAdapterPosition = parent.getChildAdapterPosition(childInContact)
        if (childAdapterPosition == -1)
            return

        when {
            sectionCallback.isHeader(childAdapterPosition) ->
                moveHeader(c, currentHeader, childInContact)
            else ->
                drawHeader(c, currentHeader)
        }
    }

    private fun getChildInContact(parent: RecyclerView, contactPoint: Int): View? {
        var childInContact: View? = null
        for (i in 0 until parent.childCount) {
            val child = parent.getChildAt(i)
            if (child.bottom > contactPoint) {
                if (child.top <= contactPoint) {
                    childInContact = child
                    break
                }
            }
        }
        return childInContact
    }

    private fun moveHeader(c: Canvas, currentHeader: View, nextHeader: View) {
        c.save()
        c.translate(0f, nextHeader.top - currentHeader.height.toFloat())
        currentHeader.draw(c)
        c.restore()
    }

    private fun drawHeader(c: Canvas, header: View) {
        c.save()
        c.translate(0f, 0f)
        header.draw(c)
        c.restore()
    }

    /**
     * Measures the header view to make sure its size is greater than 0 and will be drawn
     * https://yoda.entelect.co.za/view/9627/how-to-android-recyclerview-item-decorations
     */
    private fun fixLayoutSize(parent: ViewGroup, view: View, height: Int) {
        val widthSpec = View.MeasureSpec.makeMeasureSpec(
            parent.width,
            View.MeasureSpec.EXACTLY
        )
        val heightSpec = View.MeasureSpec.makeMeasureSpec(
            parent.height,
            View.MeasureSpec.EXACTLY
        )
        val childWidth: Int = ViewGroup.getChildMeasureSpec(
            widthSpec,
            parent.paddingLeft + parent.paddingRight,
            view.layoutParams.width
        )
        val childHeight: Int = ViewGroup.getChildMeasureSpec(
            heightSpec,
            parent.paddingTop + parent.paddingBottom,
            height
        )
        view.measure(childWidth, childHeight)
        view.layout(0, 0, view.measuredWidth, view.measuredHeight)
    }

    interface SectionCallback {
        fun isHeader(position: Int): Boolean
        fun getHeaderLayoutView(list: RecyclerView, position: Int): View?
    }
}
```
* MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {

    private lateinit var adapter: StickyHeaderAdapter

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        adapter = StickyHeaderAdapter(events)

        val recyclerView = findViewById<RecyclerView>(R.id.recyclerView)

        recyclerView.layoutManager = LinearLayoutManager(this)
        recyclerView.adapter = adapter

        recyclerView.addItemDecoration(StickyHeaderItemDecoration(getSectionCallback()))
    }

    private fun getSectionCallback(): StickyHeaderItemDecoration.SectionCallback {
        return object : StickyHeaderItemDecoration.SectionCallback {
            override fun isHeader(position: Int): Boolean {
                return adapter.isHeader(position)
            }

            override fun getHeaderLayoutView(list: RecyclerView, position: Int): View? {
                return adapter.getHeaderView(list, position)
            }
        }
    }
```

[참고한 블로그](https://leveloper.tistory.com/198)

[블로그를 참고해서 만든 StickyHeader](https://github.com/KyungHwa0/KotlinPractice/commit/293a182e1d5aab9ee241d7d87ec4380bdc30373f)
