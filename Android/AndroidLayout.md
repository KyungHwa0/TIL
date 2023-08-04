# Layout
ViewGroup의 파생 클래스로서, 포함 된 View를 정렬하는 기능

## Layout의 종류
### Linear Layout
컨테이너에 포함 된 뷰들을 수평 또는 수직으로 일렬 배치하는 레이아웃
* 자식 뷰를 수평,수직으로 일렬 배치하는 레이아웃으로, 가장 단순하고 직관적이며  사용빈도가 높다.
* LinearLayout의 자식(Children)으로 배치되는 View위젯들은 오직 한 방향 (가로 또는세로)으로만 배치
* 위젯의 크기(높이 또는 너비)와 관계없이 한 줄로만 배열
* 아래 그림과 같이 가로 방향으로 배치 될 때는 가로로 한 줄(onlyonerow)
* 세로 방향으로 배치될 때는 세로로 한 줄(onlyonecolumn)로 표시
![](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F6c96c5de-5b1a-4ff8-bf50-59bebda8e008%2FUntitled.png?table=block&id=73d34df1-61e6-4768-bac5-3c9b1844a013&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=1660&userId=&cache=v2)
* LinearLayout의 자식들은 중첩(overrap)되지 않고,지정한 방향으로 쌓이는(stacked)형태로 표시
* LinearLayout은 자식(Children)들이 배치 될 때,전체 영역 대비 비율의개념으로지정할수있는Weight(가중치)를 설정
* ex) 전체 크기를 10으로 본다면, 첫 번째 View위젯은 3, 두 번째View위젯은7의영역을차지하도록 만듦
![](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ffe929b20-eeb7-440c-a105-f3213204f75e%2FUntitled.png?table=block&id=e38897bf-38b0-4dec-a71b-3c357801f9a1&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=2000&userId=&cache=v2)