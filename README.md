# 5주차 Study [ 2024-12-01 ~ 2024-12-06 ]

**[ 목표 ]**
- 이번주 목표 : 메시지 처리 배우기기
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

| 메시지 유형 | 발생 상황 | 메시지 핸들러 함수 |
|---|---|---|
| WM_CREATE | 윈도우가 생성될 때 | OnCreate() |
| WM_ACTIVE | 윈도우가 활성화될 때 | OnActive() |
| WM_PAINT | 윈도우가 다시 그려져야 될 때 | OnPaint() |
| WM_SIZE | 윈도우가 생성될때<br>윈도우 크기가 변경될 때 | OnSize() |
| WM_MOVE | 윈도우가 움직일 때 | OnMove() |
| WM_TIMER | 설정된 타이머 시간이 됐을 때 | OnTimer() |
| WM_DESTORY | 윈도우가 종료될 때 | OnDestroy() |

메시지 박스 출력 : AfxMessageBox()

| int AfxMessageBox(LPCTSTR lpszText, UINT nType = MB_OK, UINT nIDHelp =0); |
|--|
| lpszText : 출력하고자 하는 문자열 |
| nType : 메시지 박스 출력 스타일(버튼, 아이콘) |
| nIDHelp : 현재 상태에서 F1 키를 눌러 도움말을 실행하였을 때의 도움말 ID |

* 자주 사용하는 마우스 메시지와 메시지 핸들러 함수

| 메시지 유형 | 발생 상황 | 메시지 핸들러 함수 |
| --- | --- | --- |
| WM_MOUSEMOVE | 마우스를 이동 | OnMouseMove() |
| WM_LBUTTONDBLCLK | 왼쪽 마우스 버튼을 더블 클릭 | OnLButtonDblClk() |
| WM_LBUTTONDOWN | 왼쪽 마우스 버튼을 누름 | OnLButtonDown() |
| WM_LBUTTONUP | 왼쪽 마우스 버튼을 놓음 | OnLButtonUp() |
| WM_RBUTTONDBLCLK | 오른쪽 마우스 버튼을 더블 클릭 | OnRButtonDblClk() |
| WM_RBUTTONDOWN | 오른쪽 마우스 버튼을 누름 | OnRButtonDown() |
| WM_RBUTTONUP | 오른쪽 마우스 버튼을 놓음 | OnRButtonUp() |
| WM_MOUSEWHEEL | 마우스 휠을 움직임 | OnMouseWheel() |

마우스의 메시짖 핸들러 함수들을 살펴보면 nFlags 와 point라는 매개변수를 제공한다.<br>
nFlags는 버튼이 눌리면서 키보드에서 특정한 키가 눌러졌을 때의 값이나 마우스 눌린 값이다.<br>
point는 클라이언트 영역의 현재 마우스 좌표값을 CPoint 클래스 형식으로 제공한다.<br>
윈도우의 클라이언트 영역은 좌측 상단 좌표가 (0, 0)인 상대좌표이다. 다음은 nFlags가 가질 수 있는 값이다.

* MB_CONTROL : Ctrl 키가 눌림
* MB_LBUTTON : 왼쪽 마우스 버튼 눌림
* MB_MBUTTON : 가운데 마우스 버튼 눌림
* MB_RBUTTON : 오른쪽 마우스 버튼 눌림
* MB_SHIFT : Shift 키가 눌림

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

![캡처](https://github.com/user-attachments/assets/ee808fad-7151-45c1-be77-25a54827f484)
![캡처2](https://github.com/user-attachments/assets/189ddc3a-e9e7-40b2-a1f7-fbeff63def9a)
![캡처3](https://github.com/user-attachments/assets/ad38b90b-526c-4ed3-8b60-38fbedd3769b)

[ 실습 2 ]

CMFC2 클래스에 bool 형식의 m_bTimerRun 변수와 m_bTimerType을 추가해줍니다.
```ruby
CMFC2View::CMFC2View() noexcept
{
	// TODO: 여기에 생성 코드를 추가합니다.
	m_bTimerRun = false;
	m_bTimerType = true;
}
```

m_bTimerRun 은 FALSE 로 초기화 하고 m_bTimerType 은 TRUE 로 초기화 해줍니다.

다음으로 OnCreate 메시지 핸들러 함수 추가후 코드를 입력해줍니다.
```ruby
int CMFC2View::OnCreate(LPCREATESTRUCT lpCreateStruct)
{
	if (CView::OnCreate(lpCreateStruct) == -1)
		return -1;

	// TODO:  여기에 특수화된 작성 코드를 추가합니다.
	SetTimer(0, 1000, NULL); //타이머 설정
	m_bTimerRun = TRUE; //타이머 동작

	return 0;
}
```

| SetTimer() 함수 |
|---|
| SetTimer() 함수는 지정된 시간 간격마다 WM_TIMER 메시지를 발생시켜 타이머를 설정하는 함수이다. 함수의 원형은 다음과 같다. |
| UINT SetTImer(UINT nIDEvent UINT nElapse, TIMERPROC lpTimerFunc) |
| nIDEvent : 타이머 ID이다. 이 타이머 ID는 OnTimer() 함수의 인자로 전달되며 이를 이용하여 여러 개의타이머를 설정할 수 있다. |
| nElapse : WM_TIMER 메시지를 발생시킬 시간 간격이다. 사용되는 단위는 1000분의 1초 1000을 적어주면 1초에 한번 씩 WM_TIMER 메시지를 발생시킨다. |
| lpTimerFunc : WM_TIMER 메시지가 발생하였을 때 실행되는 함수이다. NULL이 설정되면 OnTimer()함수가 호출된다. |

CMFC2 클래스에 CString 형식의 m_strTimer 변수를 추가해줍니다.

그 후 클래스 마법사에서 WM_TIMER 메시지를 선택하여 OnTimer() 함수를 생성합니다.

```ruby
void CMFC2View::OnTimer(UINT_PTR nIDEvent)
{
	// TODO: 여기에 메시지 처리기 코드를 추가 및/또는 기본값을 호출합니다.

	CView::OnTimer(nIDEvent);
	int hour;
	CString str;
	CTime timer; //타이머 변수 선언
	timer = CTime::GetCurrentTime(); //현재 시각을 얻음

	if (m_bTimerType){ //년,월,일,시,분,초 형태일 경우
		m_strTimer.Format(_T("현재는 %d년 %d월 %d일 %d시 %d분 %d초"), timer.GetYear(), timer.GetMonth(), timer.GetDay(), timer.GetHour(), timer.GetMinute(), timer.GetSecond());
	}
	else {
		hour = timer.GetHour();
		if (hour >= 12)
		{
			str = _T("PM");
			if (hour >= 13)
				hour = hour - 12;
		}
		else
		{
			str = _T("AM");
		}
		m_strTimer.Format(_T("지금은 %s %d시 %d분 %d초"), str, hour, timer.GetMinute(), timer.GetSecond());
	}
	Invalidate();
	CView::OnTimer(nIDEvent);
}
```

```ruby
void CMFC2View::OnDraw(CDC* pDC) //주석 처리 해제
{
	CMFC2Doc* pDoc = GetDocument();
	ASSERT_VALID(pDoc);
	if (!pDoc)
		return;

	// TODO: 여기에 원시 데이터에 대한 그리기 코드를 추가합니다.
	CRect rect;
	GetClientRect(&rect); //윈도우 클라이언트 영역을 얻는다.
	//윈도우의 중앙에 현재 시각을 출력
	pDC->DrawText(m_strTimer, rect, DT_SINGLELINE | DT_CENTER | DT_VCENTER);
}
```

그 후 왼쪽 마우스 버튼을 눌렀을 때 시계 표시 형태를 변경하는 코드를 작성합니다.

OnLButtonDown 메시지 핸들러 함수를 선택하고 코드를 작성해줍니다.
```ruby
void CMFC2View::OnLButtonDown(UINT nFlags, CPoint point)
{
	// TODO: 여기에 메시지 처리기 코드를 추가 및/또는 기본값을 호출합니다.

	if (m_bTimerType) //년, 월, 일, 시 ,분, 초 형태로 출력 중
	{
		if (AfxMessageBox(_T("시 분 초 형태로 표시하겠습니까?"), MB_YESNO | MB_ICONQUESTION) == IDYES) {
			m_bTimerType = FALSE;
		}
	}
	else {
		if (AfxMessageBox(_T("년, 월, 일, 시, 분, 초 형태로 표시하겠습니까?"), MB_YESNO | MB_ICONQUESTION) == IDYES) {
			m_bTimerType = TRUE;
		}
	}
	CView::OnLButtonDown(nFlags, point);
}
```

오른쪽 마우스 버튼을 눌렀을 때 시계의 동작 여부를 결정합니다.
```ruby
void CMFC2View::OnRButtonDown(UINT nFlags, CPoint point)
{
	// TODO: 여기에 메시지 처리기 코드를 추가 및/또는 기본값을 호출합니다.
	
	if (m_bTimerRun == FALSE) // 타이머가 동작 안 할 때 메시지 박스 출력
	{
		if (AfxMessageBox(_T("디지털시계를 동작시키겠습니까?"), MB_YESNO | MB_ICONQUESTION) == IDYES)
		{
			SetTimer(0, 1000, NULL); //타이머 설정
			m_bTimerRun = TRUE; //타이머 동작 => true
		}
	}
	else { //타이머가 동작 중일 때 메시지 박스 출력
		if (AfxMessageBox(_T("정말로 디지털 시계 동작을 멈추겠습니까?"), MB_YESNO | MB_ICONQUESTION) == IDYES)
		{
			KillTimer(0);
			m_bTimerRun = FALSE;
		}
	}

	CView::OnRButtonDown(nFlags, point);
}
```

마지막으로 WM_DESTORY 를 추가하고 코드를 작성합니다
```ruby
void CMFC2View::OnDestroy()
{
	CView::OnDestroy();

	// TODO: 여기에 메시지 처리기 코드를 추가합니다.
	if (m_bTimerRun) KillTimer(0); //타이머 해제
}
```

![1](https://github.com/user-attachments/assets/45401040-265d-4fc1-af8c-e08ac0ebde43)<br>
![2](https://github.com/user-attachments/assets/1085c2c0-fc83-40fb-b511-05521ec63042)<br>
![3](https://github.com/user-attachments/assets/e46cdfb5-7b01-45b9-9e40-59642ba4bb62)<br>
![4](https://github.com/user-attachments/assets/6effc489-11be-4202-b2f2-dafd90cf015a)<br>

-------

