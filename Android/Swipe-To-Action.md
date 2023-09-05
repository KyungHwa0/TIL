# Swipe-to-Action
사용자가 화면에서 특정 항목 또는 아이템을 스와이프하여 관련된 작업을 수행할 수 있는 기능이다.
이 기능은 주로 리스트나 그리드와 같은 데이터 표시 형식에서 사용되며, 사용자가 편리하게 아이템을 삭제, 수정, 공유 또는 다른 작업을 수행할 수 있도록 도와준다.

## Swipe-to-Action를 구현해보기

1. RecyclerView 또는 ListView 구성: Swipe-to-Action를 구현하려면 먼저 데이터를 표시하는 RecyclerView 또는 ListView를 액티비티 레이아웃에 추가해야 한다. 이러한 뷰는 사용자가 스와이프할 수 있는 아이템 목록을 표시한다.

2. **ItemTouchHelper** 클래스 사용: Android에서 Swipe-to-Action을 구현하기 위해 ItemTouchHelper 클래스를 사용한다. 이 클래스는 스와이프 및 드래그 동작을 처리하는데 도움이 되며, RecyclerView 또는 ListView와 함께 사용된다.

3. Swipe 동작 설정: ItemTouchHelper를 사용하여 아이템 스와이프 동작을 설정한다. 이때 스와이프 방향, 제스처 감도, 배경 효과 등을 정의할 수 있다.

4. Swipe 액션 정의: 스와이프할 때 수행할 작업에 대한 액션을 정의한다. 예를 들어, 오른쪽으로 스와이프하면 "삭제" 액션을 수행하고 왼쪽으로 스와이프하면 "수정" 액션을 수행하도록 정의할 수 있다.

5. 아이템 데이터 업데이트: Swipe 동작으로 인해 아이템이 삭제되거나 수정되는 경우, 해당 작업을 수행하고 RecyclerView 또는 ListView를 업데이트하여 변경 사항을 반영한다.

6. Swipe-to-Action UI 구성: 스와이프할 때 나타나는 백그라운드 또는 버튼과 같은 UI 요소를 디자인한다. 이러한 요소는 사용자가 스와이프를 완료하면 표시되며, 해당 액션을 수행하는 데 사용된다.

> Swipe-to-Action를 구현하는 방법은 앱의 디자인 및 요구 사항에 따라 다를 수 있으며, 이를 구현하기 위해 다양한 라이브러리 및 커스텀 솔루션을 사용할 수 있다. Android 개발 문서 및 오픈 소스 라이브러리를 참고하여 원하는 Swipe-to-Action 동작을 구현할 수 있다.

> 참고  
 https://github.com/16-team/16-team/commit/ebdc4f574fbc5d9a3bbc646c2f188349b1effc15