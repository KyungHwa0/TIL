# AdapterView
### 1. 여러개의 항목을 다양한 형식으로 나열하고 선택 할 수 있는 기능을 제공하는 뷰
* 리스트뷰(ListView)는 항목을 수직으로 나열시키는 방식
* 그리드뷰(GridView)는 항목을 격자 형태로 나열시키는 방식

### 2. 어탭터(Adapter)
* 데이터를 관리하며 데이터 원본과 어댑터뷰(ListView, GridView) 사이의 중계 역할
* 어댑터뷰 데이터 항목 표시방법
    1. 어댑터뷰가 어댑터를 사용하기 위해서는 먼저 데이터 원본이 어댑터에 설정되어야 하고, 어댑터뷰에는 어댑터가 설정되어야 한다.
    2. 어댑터뷰는 항목을 표시하기 위해서 먼저 표시할 항목의 총 개수를 알 아야한다. 이 때, 어댑터 뷰는 어댑터의 getCount()란 메소드를 통해 현재 어뎁터가 관리하는 데이터 항목의 총 개수를 반환한다.
    3. 어댑터 뷰는 어댑터의 getView()란 메소드를 통해서 화면에 실제로 표시할 항목뷰를 얻고, 이를 화면에 표시한다.
* 사용자가 어댑터뷰의 특정 위치의 항목을 선택하였을 때, 어댑터뷰는 선택된 항목, 항목ID, 항목뷰를 어댑터의 getItem(), getItemId(), getView() 메소드를 통해 얻어와서 이를 항목선택 이벤트 처리기에 넘겨준다.
<img width="955" alt="어댑터" src="https://github.com/KyungHwa0/TIL/assets/124041716/9e6ab885-4c4e-4139-b54c-7b8c1248e737">
* 어댑터에 정의된 인터페이스를 바탕으로 필요한 정보를 요청하여 항목뷰를 화면에 표시하거나 선택된 항목뷰를 처리한다.

### 3. 어댑터 종류
1. BaseAdapter
    * 어댑터 클래스의 공통 구현
    * 사용자 정의 어댑터 구현 시 사용
2. ArrayAdapter
    * 객체 배열이나 리소스에 정의된 배열로부터 데이터를 공급받음
3. CursorAdapter
    * 데이터베이스로부터 데이터를 공급받음
4. SimpleAdapter
    * 데이터를 Map(키,값)의 리스트로 관리
    * 데이터를 XML파일에 정의된 뷰에 대응시키는 어댑터
    
![어댑터종류](https://github.com/KyungHwa0/TIL/assets/124041716/08f4b31c-d491-4355-8328-fddf8ca0f48c)