# UI 설계
## View
안드로이드 앱의 UI를 구성하는 기본 단위

### View의 구성
#### 위젯(Widget)
* View의 서브 클래스로서, 앱 화면을 구성하는 시각적인 모양을 지닌 UI요소  
    - 버튼, 메뉴, 리스트 등
#### 레이아웃(Layout)
* ViewGroup의 서브 클래스로서, 다른 뷰(위젯 or 레이아웃)를 포함하면서
이들을 정렬하는 기능을 지닌 UI요소

<br>

# UI 설계 방법
## XML을 사용
### AndroidStudio의 Layout Editor를 이용
* 드래그 앤 드롭 방식의 WYSIWYG(what you see is what you get) 에디터
* 다양한 디바이스 / 안드로이드 버전에 대한 Preview
* XML코드 자동 변환 및 동기화
<br>

### Layout Editor
![Layout Editor](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F05f8e160-4718-4b42-ba27-5f73df4aacbd%2FUntitled.png?table=block&id=c7ff641a-4361-412e-9e95-71e813ba6fb8&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=2000&userId=&cache=v2)

1. Palette - 레이아웃으로 드래그 할 수 있는 다양한 뷰 및 뷰 그룹을 포함
2. Component Tree - 레이아웃에서 구성요소의 계층 구조를 표시
3. 툴바 - 편집기에서 레이아웃 모양을 구성하고 레이아웃 속성을 변경하려면 이 버튼을 클릭
4. 디자인 편집기 - 디자인 뷰나 청사진 뷰 또는 두 뷰 모두에서 레이아웃을 수정
5. Attributes - 선택한 뷰의 속성을 제어할 수 있는 영역
6. 뷰 모드 - 레이아웃을 코드, 디자인, 분할 모드 중 하나로 표시
7. 확대/축소 및 화면 이동 컨트롤 - 편집기 내에서 미리보기의 크기와 위치를 제어


## XML file을 직접 편집
* 필요한 XML 태그나 속성을 잘 모를 경우 불편
* Copy & paste를 이용한 편집이 효율적인 경우가 많음
  
![XML file](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fff1af51c-e4e2-4863-add9-0b8ce20a78a8%2FUntitled.png?table=block&id=4a531e2a-fdb9-404f-9110-8d69bffd11de&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=2000&userId=&cache=v2)
