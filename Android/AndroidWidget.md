# Widget
## Widget이란?
* View의 서브 클래스 중에서 화면에 보이는 것들
* 대표적인 위젯으로 TextView, EditText, Button 등이 있다.
![widget](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fdf1dae2c-2162-4a63-b048-d05e8e2e9201%2FUntitled.png?table=block&id=0bdbe125-1351-47b5-bcb2-4f8837396864&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=2000&userId=&cache=v2)

## View
### View 란?
* View클래스는 모든 UI 컴포넌트들의 부모 클래스
* View클래스의 속성은 모든 UI컴포넌트들에서 공통적으로 사용 할 수 있다.
![](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F116e9176-fecc-43ec-a5ea-b3359a045770%2FUntitled.png?table=block&id=43f86067-7201-4667-aefc-00138694eb8b&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=2000&userId=&cache=v2)

### layout_width, layout_height
* match_parent(혹은fill_parent) : 부모 UI컴포넌트의 크기에 맞춤
* wrap_content : UI컴포넌트의 내용물 크기에 맞춤
![](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fffdc91c7-fb81-43a0-8455-4ff5107ad17e%2FUntitled.png?table=block&id=d856212b-326d-445b-9d76-b656482f7831&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=2000&userId=&cache=v2)

## TextView
화면에 text를 표시 하는 용도
### 주요속성 
* View 속성 상속 : id, layout_width, layout_hight, background, etc.
* text : 출력할 문자를 지정
* textSize : 폰트크기
* textStyle : 텍스트 스타일(normal, bold, italic)
* typeface : 텍스트폰트(normal, sans, serif, monospace)
* textColor : 문자열 색상
* singleLine : 속성값이 "true"이면 텍스트가 위젯의 폭보다 길 때 강제로 한줄에 출력

## EditText
입력이 가능한 Text창
### 주요속성 
* TextView의 모든 속성 상속(EditText는TextView의 서브클래스이다.)
* inputType: 입력 시 허용되는 키보드 타입 설정 및 키보드 행위를 설정
#### 키보드 설정 값
* “text”:일반적인 텍스트 키보드
* “phone”:전화번호 입력 키보드
* “textEmailAddress”:@문자를 가진 텍스트 키보드
* “textCapWords” : 문장의 시작을 대문자로 변환
* “textAutoCorrect” : 입력된 단어와 유사한 단어를 제시하고 제시된 단어 선택 시,입력된 단어를 대치
* “textMultiLine”:여러 줄을 입력 받을 수 있다.

## Button
일반적으로 많이 사용되는 푸시 버튼으로 사용자가 버튼을 클릭하였을 때, 어떤 행동을 수행 하고자 할 때 사용된다.
* Button클래스는 TextView의 서브클래스이므로, TextView의 모든 속성을 사용 할 수 있다.
* 버튼 내에 텍스트,아이콘을 표시 할 수 있다.
    * 버튼 전체를 이미지로 그리기 위해서는 ImageButton 을 사용한다.

### 버튼 클릭 이벤트 처리
사용자가 버튼 위젯을 클릭 할 때, 지정된 행동을 수행하기 위해서는 다음 두 가지 방법 중 하나를 사용 할 수 있다.

### 버튼 위젯의 onClick속성 활용 방법
버튼 위젯을 정의한 화면을 contentView로 설정한 액티비티 클래스에 새로운 메소드(예,doAction())를 추가한다.
![](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fe8e2c9ce-6673-42e7-b17e-722dd3a8b4b7%2FUntitled.png?table=block&id=d77adc38-d6d7-4ab2-950f-d4adac5e933e&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=1680&userId=&cache=v2)

### 이벤트 처리 객체를 이용하는 방법
* 이벤트를 처리하는 객체를 생성하여 해당 이벤트를 발생시키는 위젯에 등록한다.
* 위젯에서 이벤트가 발생하면 등록된 이벤트 처리 객체가 정의된 일을 수행한다.
![](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F8ed78d20-b10d-4fb3-9830-7f7b34f498f2%2FUntitled.png?table=block&id=b979dc8d-fb73-4dcf-b959-9119ae8ccc9c&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=2000&userId=&cache=v2)
![](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F816103af-1031-4ee6-815d-d6925ada48bb%2FUntitled.png?table=block&id=4690126b-a3e5-48bc-bfde-d61b861f07bb&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=2000&userId=&cache=v2)
> **참고**  (findViewByID()함수)  
Activity클래스에 정의된 메소드로 Activity 하위 클래스에 사용가능하다.  
해당 액티비티와 연결된 XML layout 리소스 요소 중에서 id속성을 바탕으로 해당 Java 객체를 가져온다.  
따라서 다른 액티비티와 연결된 XML layout 리소스에 정의된 위젯을 findViewByID() 메소드로 가져올 수는 없다.

## ImageView
### ImageView 란?
앱 화면에 이미지를 표시하는 용도

### ImageVIew기본 사용법
* Layout리소스 XML파일에 ImageView를 추가
* 화면에 표시 할 이미지를 Drawable리소스에 추가
* 화면에 표시 할 이미지(Drawable)리소스 ID를 ImageView의"src"속성에 지정

### Drawable리소스에 이미지 추가
* 이미지 파일의 형식은 .jpg,.png가 가능하나 대부분.png를 사용함(투명도 때문)
* 이미지 파일을 /res/drawable에 추가한다.
* 해상도에 따른 다른 크기의 이미지는 별도의 폴더를 생성하고 복사(drawable-xhdpi등..)

### 🚨[주의]이미지 파일 명
![](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F1a0445b3-46f5-4a89-8037-a2ced4cf4417%2FUntitled.png?table=block&id=4852a6a1-3fa8-4f04-ab17-f37b5b3dc8c5&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=1310&userId=&cache=v2)