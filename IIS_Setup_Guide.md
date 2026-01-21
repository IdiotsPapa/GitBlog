# Windows Server 2022 IIS 역할 서비스(Role Services) 설치 가이드

이 가이드는 Windows Server 2022(영문 버전) GUI 환경에서 IIS(Internet Information Services) 역할 서비스를 설치하고 구성하는 상세 절차를 설명합니다.

## 사전 준비 (Prerequisites)

*   Windows Server 2022 (Desktop Experience 포함)
*   관리자 권한 (Administrator privileges)

## 단계별 설치 절차 (Step-by-Step Instructions)

### 1. Server Manager 실행
*   Windows 시작 메뉴를 클릭하거나 작업 표시줄에서 **Server Manager** 아이콘을 클릭하여 실행합니다.

### 2. 역할 및 기능 추가 마법사 시작
1.  Server Manager 대시보드 우측 상단의 **Manage** 메뉴를 클릭합니다.
2.  드롭다운 메뉴에서 **Add Roles and Features**를 선택합니다.
3.  **Before you begin** 화면이 나타나면 내용을 확인하고 **Next**를 클릭합니다.

### 3. 설치 유형 선택 (Installation Type)
*   **Role-based or feature-based installation** 라디오 버튼이 선택되어 있는지 확인하고 **Next**를 클릭합니다.

### 4. 대상 서버 선택 (Server Selection)
*   **Select a server from the server pool**이 선택된 상태에서, 목록에 있는 로컬 서버를 선택하고 **Next**를 클릭합니다.

### 5. 서버 역할 선택 (Server Roles)
1.  **Roles** 목록에서 **Web Server (IIS)**를 찾아 체크박스를 클릭합니다.
2.  "Add features that are required for Web Server (IIS)?"라는 팝업 창이 나타나면 **Add Features** 버튼을 클릭합니다.
3.  체크된 것을 확인하고 **Next**를 클릭합니다.

### 6. 기능 선택 (Features)
*   일반적인 웹 서버 구성의 경우, 특별히 추가할 기능이 없다면 **Next**를 클릭하여 넘어갑니다.
*   (.NET Framework 3.5 등이 필요한 경우 여기서 선택합니다.)

### 7. 웹 서버 역할 (Web Server Role (IIS))
*   IIS에 대한 소개 페이지가 나오면 **Next**를 클릭합니다.

### 8. 역할 서비스 선택 (Select Role Services)
이 단계가 가장 중요합니다. **Role services** 목록에서 **Web Server**를 펼쳐(Expand) 필요한 구성 요소를 선택합니다.

일반적으로 웹 서버 운영을 위해 권장되거나 자주 사용되는 항목들은 다음과 같습니다:

*   **Web Server**
    *   **Common HTTP Features** (일반 HTTP 기능)
        *   [x] Default Document
        *   [x] Directory Browsing
        *   [x] HTTP Errors
        *   [x] Static Content
        *   [ ] HTTP Redirection (필요 시 선택)
    *   **Health and Diagnostics** (상태 및 진단)
        *   [x] HTTP Logging
        *   [ ] Logging Tools (상세 로깅 필요 시)
        *   [ ] Request Monitor
    *   **Performance** (성능)
        *   [x] Static Content Compression
        *   [ ] Dynamic Content Compression (동적 콘텐츠 압축 필요 시)
    *   **Security** (보안)
        *   [x] Request Filtering
        *   [ ] Basic Authentication (기본 인증 필요 시)
        *   [ ] Windows Authentication (Windows 통합 인증 필요 시)
    *   **Application Development** (응용 프로그램 개발)
        *   [ ] .NET Extensibility 4.8
        *   [ ] ASP.NET 4.8 (ASP.NET 애플리케이션 구동 시 필수)
        *   [ ] ISAPI Extensions
        *   [ ] ISAPI Filters
        *   [ ] WebSocket Protocol

*   **Management Tools** (관리 도구)
    *   [x] IIS Management Console (IIS 관리자를 사용하기 위해 필수)

모든 필요한 항목을 체크한 후 **Next**를 클릭합니다.

### 9. 설치 확인 (Confirmation)
1.  선택한 역할 및 기능 목록을 검토합니다.
2.  필요한 경우 **Restart the destination server automatically if required** 옵션을 체크합니다. (IIS 설치는 보통 재부팅이 필요 없으나, 일부 기능은 요구할 수 있습니다.)
3.  **Install** 버튼을 클릭합니다.

### 10. 설치 완료 (Completion)
1.  설치 진행 상황 바(Progress bar)가 완료될 때까지 기다립니다.
2.  "Installation succeeded on [Server Name]" 메시지가 표시되면 **Close**를 클릭합니다.

## 설치 확인
1.  웹 브라우저를 열고 주소창에 `http://localhost`를 입력합니다.
2.  파란색의 IIS 시작 페이지(IIS Windows Server)가 보이면 설치가 성공적으로 완료된 것입니다.
