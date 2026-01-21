# Windows Server 2022 .NET Framework 재설치 가이드

이 가이드는 Windows Server 2022(영문 버전) GUI 환경에서 **Server Manager**를 사용하여 .NET Framework 기능(Features)을 제거하고 다시 설치하는 방법을 설명합니다.

> **주의**: .NET Framework 4.8은 운영 체제의 일부로 포함되어 있는 경우가 많으며, 이를 제거하면 의존성이 있는 다른 역할(예: IIS, PowerShell 등)이나 응용 프로그램 작동이 중단될 수 있습니다. 진행 전 의존성을 확인하고 서버 백업을 권장합니다.

## 1단계: .NET Framework 제거 (Uninstall/Remove)

1.  **Server Manager**를 실행합니다.
2.  대시보드 우측 상단의 **Manage** 메뉴를 클릭합니다.
3.  **Remove Roles and Features**를 선택합니다.
4.  **Before you begin** 화면에서 **Next**를 클릭합니다.
5.  **Server Selection** 화면에서 대상 서버가 선택된 것을 확인하고 **Next**를 클릭합니다.
6.  **Server Roles** 화면은 변경 없이 **Next**를 클릭하여 넘어갑니다.
7.  **Features** 화면에서 제거하려는 .NET Framework 버전을 찾습니다.
    *   **[.NET Framework 3.5 Features]** (보통 2.0 및 3.0 포함)
    *   **[.NET Framework 4.8 Features]** (4.x 버전)
    *   해당 항목의 체크박스를 **해제(Uncheck)**합니다.
    *   *(참고: 만약 해당 프레임워크를 사용하는 다른 역할(예: IIS의 ASP.NET 4.8)이 설치되어 있다면, 종속성 때문에 해당 역할도 함께 제거해야 한다는 팝업이 뜰 수 있습니다. **Remove Features**를 클릭하여 동의합니다.)*
8.  **Next**를 클릭합니다.
9.  **Confirmation** 화면에서 **Remove** 버튼을 클릭합니다.
    *   필요 시 "Restart the destination server automatically if required"를 체크합니다.
10. 제거가 완료되면 **Close**를 클릭하고, 필요한 경우 서버를 **재부팅(Restart)**합니다.

---

## 2단계: .NET Framework 재설치 (Reinstall/Add)

1.  **Server Manager**를 실행합니다.
2.  대시보드 우측 상단의 **Manage** 메뉴를 클릭합니다.
3.  **Add Roles and Features**를 선택합니다.
4.  **Before you begin**, **Installation Type**, **Server Selection** 화면에서 각각 **Next**를 클릭합니다.
5.  **Server Roles** 화면은 변경 없이 **Next**를 클릭하여 넘어갑니다.
6.  **Features** 화면에서 설치하려는 .NET Framework 버전을 찾습니다.
    *   **[.NET Framework 3.5 Features]**
    *   **[.NET Framework 4.8 Features]**
    *   **ASP.NET 4.8** (하위 항목을 펼쳐서 필요한 경우 체크)
    *   **WCF Services** (필요한 경우 체크)
    *   해당 항목의 체크박스를 **선택(Check)**합니다.
7.  **Next**를 클릭합니다.
8.  **Confirmation** 화면에서 내용을 확인합니다.
    *   *(참고: .NET 3.5 설치 시 소스 파일이 없다는 오류가 발생할 수 있습니다. 이 경우 하단의 "Specify an alternate source path"를 클릭하고 Windows Server 설치 미디어(ISO)의 `\sources\sxs` 경로를 지정해야 할 수 있습니다.)*
9.  **Install** 버튼을 클릭합니다.
10. 설치가 완료되면 **Close**를 클릭합니다.

## 설치 확인
*   명령 프롬프트(cmd) 또는 PowerShell을 열고 다음 명령어로 설치된 버전을 확인할 수 있습니다.
    *   PowerShell: `Get-WindowsFeature -Name *Framework*`
