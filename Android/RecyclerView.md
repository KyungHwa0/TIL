# RecyclerView
RecyclerView는 안드로이드 앱에서 리스트 형태의 데이터를 표시하는데 사용되는 위젯이다. 여러 아이템을 스크롤 가능한 리스트로 표현하며, 많은 아이템을 효율적으로 관리하고 보여주는 역할을 한다.

## RecyclerView 기본 구조
1. **Adapter** : 데이터를 아이템 뷰와 연결하는 역할
2. **ViewHolder** : 아이템 뷰를 보유하고 표시하는 역할
3. **LayoutManager** : 아이템들의 배치 방식을 관리

## Adapter란?
Adapter는 안드로이드에서 리스트나 그리드 같은 데이터를 화면에 표시하는 데 도움을 주는 중요한 역할을 한다. 리스트나 그리드에 표시할 데이터와 레이아웃을 연결하는 역할을 하며, 데이터의 변경에 따라 화면을 업데이트한다.

> 참고  
[AdapterView](https://github.com/KyungHwa0/TIL/blob/main/Android/AdapterView.md)

## RecyclerView 사용 단계
1. 의존성 추가: build.gradle 파일에 RecyclerView 의존성을 추가
```kotlin
implementation ("androidx.recyclerview:recyclerview:1.3.1")
```
2. **아이템 레이아웃 생성**: 아이템 하나의 레이아웃을 작성
3. **Adapter 생성**: RecyclerView.Adapter 클래스를 상속한 Adapter 클래스를 생성
4. **ViewHolder 생성**: RecyclerView.ViewHolder 클래스를 상속한 ViewHolder 클래스를 생성
5. **LayoutManager 설정**: RecyclerView에 사용할 레이아웃 매니저를 설정

## Adapter 및 ViewHolder
```kotlin
class MyAdapter(private val items: List<String>) : RecyclerView.Adapter<MyAdapter.MyViewHolder>() {

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): MyViewHolder {
        val binding = ItemRecyclerviewBinding.inflate(LayoutInflater.from(parent.context), parent, false)
        return Holder(binding)
    }

    override fun onBindViewHolder(holder: MyViewHolder, position: Int) {
        holder.bind(items[position])
    }

    override fun getItemCount(): Int {
        return items.size
    }

    inner class MyViewHolder(itemView: View) : RecyclerView.ViewHolder(itemView) {
        fun bind(item: String) {
            itemView.textView.text = item
        }
    }
}
```

## RecyclerView 및 LayoutManager 설정
```kotlin
class MainActivity : AppCompatActivity() {
		private lateinit var binding:ActivityMainBinding
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        val items = listOf("Item 1", "Item 2", "Item 3", "Item 4", "Item 5")
        val adapter = MyAdapter(items)
        binding.recyclerView.adapter = adapter
        binding.recyclerView.layoutManager = LinearLayoutManager(this)

    }
}
```