# SearchView
사용자가 검색어를 입력하고 검색 공급자에게 요청을 제출할 수 있는 사용자 인터페이스를 제공하는 위젯.

### SearchView 의 속성
* searchIcon : SearchView의 검색 아이콘을 지정하는 속성
```
app:searchIcon="@drawable/ic_search"
```
* closeIcon : 클릭 시 SearchView를 닫아주며 그것을 나타내는 아이콘을 지정하는 속성
```
app:closeIcon="@drawable/ic_baseline_clear_24"
```
* iconifiedByDefault : SearchView는 기본적으로 접혀 있는 상태로 시작하고 기본적으로 true로 설정되어있으며 boolean으로 SearchView의 상태를 나타내는 속성이다.
```
app:iconifiedByDefault="false"
```
* queryBackground : SearchView는 이미지 뷰처럼 백그라운드가 안 먹히는 뷰이다. 이를 해결하기 위한 속성이 바로 queryBackground이다.
queryBackground는 SearchView의 형태를 지정하는 속성이다.
```
app:queryBackground="@drawable/searchview_background"
```
* queryHint : SearchView에 hint를 표시해주는 속성
* maxWidth : SearchView의 최대 너비를 지정하는 속성( maxWidth는 보통 xml 보다는 java/kotlin으로 지정하는 경우가 많다. 이와 반대로 maxHeight도 있지만 잘 쓰지 않는다.)
```
searchView.maxWidth = Int.MAX_VALUE
```
* isSubmitButtonEnabled : SearchView 옆에 검색 버튼을 나타내는 코드(
해당 버튼을 클릭 시 검색 처리가 된다.)
```
searvhView.isSubmitButtonEnabled = true
```
* isIconified (kotlin) : SearchView가 펼쳐져있나 닫혀있나 Boolean으로 나타내는 값 -> 보통 뒤로 가기를 한 번 누르면 검색창이 닫히고 한 번 더 누르면 뒤로 가도록 설계하는데 쓰인다.
```kotlin
override fun onBackPressed() {
    if (!home_search_searchView.isIconified) {
        home_search_searchView.isIconified = true
    } else {
        super.onBackPressed()
    }
}
```
* setOnQueryTextListener : SearchView에서 검색 및 변경을 처리하는 코드
```kotlin
searchView.setOnQueryTextListener(object : SearchView.OnQueryTextListener {
        override fun onQueryTextSubmit(query: String?): Boolean {
            
            // 검색 버튼 누를 때 호출
            
            return true
        }

        override fun onQueryTextChange(newText: String?): Boolean {
            
            // 검색창에서 글자가 변경이 일어날 때마다 호출
            
            return true
        }
})
```