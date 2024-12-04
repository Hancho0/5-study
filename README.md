# 5주차 Study [ 2024-12-01 ~ 2024-12-06 ]

**[ 목표 ]**
- 이번주 목표 : 
-----

**[ 진행 사항 ]**

[ 이벤트에 따른 메시지 처리 과정 ]
이벤트 발생 -> 윈도우 시스템 -> 메시지 전송 -> 애플리케이션 -> 메시지 처리

[ 메시지의 종류 ]
* 윈도우 메시지(Windows Message)<br>
WM_로 시작하는 메시지로 매개변수를 가지고 있어 메시지를 어떻게 처리할 것인지를 결정하는 데 사용한다. (WM_COMMAND는 제외)

윈도우 관리 메시지 : 윈도우의 상태가 바뀔 때 발생한다.<br>
초기화 메시지 : 응용 프로그램이 메뉴나 대화상자를 구성할 때 발생한다.<br>
입력 메시지 : 마우스, 키보드로 입력할 때 발생한다.<br>

* 컨트롤 통지 메시지(Control Notification Message)<br>
컨트롤 통지 메시지는 Button, Combo Box와 같은 제어 객체나 자식 윈도우에서 부모 윈도우로 보내는 메시지다.

* 명령 메시지(Command Message)<br>
명령 메시지는 메뉴, 툴바, 액셀러레이터 키와 같은 사용자 인터페이스 객체로부터 발생하는 WM_COMMANd 메시지이다. 명령 메시지는 윈도우뿐만 아니라 도큐먼트, 도큐먼트 탬플릿, 뷰, 다른 애플리케이션 객체에 의해 발생할 수도 있다.

* 자주 사용하는 윈도우 관리 메시지와 메시지 핸들러 함수
  <table>
    <tr>
      <th scope="col">메시지 유형</td>
      <th scope="col">발생 상황</td>
      <th scope="col">메시지 핸들러 함수</td>
    </tr>
    <tr>
      <td>WM_CREATE</td>
      <td>윈도우가 생성될 때</td>
      <td>OnCreate()</td>
    </tr>
    <tr>
      <td>WM_ACTIVE</td>
      <td>윈도우가 활성화될 때</td>
      <td>OnActive()</td>
    </tr>
    <tr>
      <td>WM_PAINT</td>
      <td>윈도우가 다시 그려져야 될 때</td>
      <td>OnPaint()</td>
    </tr>
    <tr>
      <td>WM_SIZE</td>
      <td>윈도우가 생성될때<br>윈도우 크기가 변경될 때</td>
      <td>OnSize()</td>
    </tr>
    <tr>
      <td>WM_MOVE</td>
      <td>윈도우가 움직일 때</td>
      <td>OnMove()</td>
    </tr>
    <tr>
      <td>WM_TIMER</td>
      <td>설정된 타이머 시간이 됐을 때</td>
      <td>OnTimer()</td>
    </tr>
    <tr>
      <td>WM_DESTORY</td>
      <td>윈도우가 종료될 때</td>
      <td>OnDestroy()</td>
    </tr>
  </table>

메시지 박스 출력 : AfxMessageBox()

<table>
  <tr>
    <td>
      int AfxMessageBox(LPCTSTR lpszText, UINT nType = MB_OK, UINT nIDHelp =0);
    </td>
  </tr>
  <tr>
      <td>
      lpszText : 출력하고자 하는 문자열</td>
      </td>
    </tr>
  <tr>
    <td>
      nType : 메시지 박스 출력 스타일(버튼, 아이콘)
    </td>
  </tr>
  <tr>
    <td>
      nIDHelp : 현재 상태에서 F1 키를 눌러 도움말을 실행하였을 때의 도움말 ID
    </td>
  </tr>
</table>

[ 실습 ]

클래스 마법사 : Ctrl + Shift + X

클래스 마법사 실행 후 클래스 이름을 CMFCApplication1View 으로 선택합니다.
메시지 선택 후 WM_CREATE 를 추가합니다.

```ruby
int CMFCApplication1View::OnCreate(LPCREATESTRUCT lpCreateStruct)
{
	if (CView::OnCreate(lpCreateStruct) == -1)
		return -1;

	// TODO:  여기에 특수화된 작성 코드를 추가합니다.
	///윈도우가 생성될 때 메시지 박스 출력
	AfxMessageBox(_T("윈도우가 생성되었습니다."), MB_OKCANCEL | MB_ICONINFORMATION);

	return 0;
}
```
코드를 입력 후 메시지 박스 버튼 스타일은 MB_OKCANCEL로, 메시지 박스 아이콘 스타일은 MB_ICONINFORMATION으로 설정한다.

WM_LBUTTONDBLCLK 를 추가후
```ruby
void CMFCApplication1View::OnLButtonDblClk(UINT nFlags, CPoint point)
{
	// TODO: 여기에 메시지 처리기 코드를 추가 및/또는 기본값을 호출합니다.
	// 왼쪽 마우스를 더블 클릭할 때 메시지 박스 출력
	AfxMessageBox(_T("왼쪽 마우스를 더블클릭했습니까?"), MB_YESNO | MB_ICONQUESTION);

	CView::OnLButtonDblClk(nFlags, point);
}
```
코드를 입력 후 메시지 박스 버튼 스타일은 MB_YESNO로, 메시지 박스 아이콘 스타일은 MBB_ICONQUESTION으로 설정한다.

WM_DESTORY를 추가한 후
```ruby
void CMFCApplication1View::OnDestroy()
{
	CView::OnDestroy();

	// TODO: 여기에 메시지 처리기 코드를 추가합니다.
	//윈도우가 종료될 때 때 메시지 박스 출력
	AfxMessageBox(_T("윈도우가 종료되었습니다."), MB_OK | MB_ICONWARNING);
}
```
코드를 입력 후 메시지 박스 버튼 스타일은 MB_OK, 메시지 박스 아이콘 스타일은 MB_ICONWARNING으로 설정한다.

