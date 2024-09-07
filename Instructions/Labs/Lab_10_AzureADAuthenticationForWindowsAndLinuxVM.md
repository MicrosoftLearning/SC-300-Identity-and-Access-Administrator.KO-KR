---
lab:
  title: 10 - Windows 및 Linux Virtual Machines에 대한 Microsoft Entra ID 인증
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# 랩 10 - Windows 및 Linux Virtual Machines에 대한 Microsoft Entra 인증

**참고** - 이 랩에는 Azure Pass가 필요합니다. 지침은 랩 00을 참조하세요.

## 랩 시나리오

회사에서는 원격 액세스를 위해 가상 머신에 로그인하는 데 Microsoft Entra ID를 사용해야 한다고 결정했습니다.  이 랩에서는 Windows 및 Linux 가상 머신에 대해 설정하는 방법을 보여 줍니다.

#### 예상 소요 시간: 30분

### 연습 1 - Microsoft Entra ID를 사용하여 Azure에서 Windows Virtual Machines에 로그인

#### 작업 1 - Microsoft Entra ID 로그인이 사용하도록 설정된 Windows 가상 머신 만들기

1. [https://portal.azure.com](https://portal.azure.com)으로 이동

1. **+ 리소스 생성**를 선택합니다.

1. Marketplace 검색 창에 **Windows 11**을 입력하고 **Enter** 키를 누릅니다.

1. **Windows 11** 상자에서 **v 만들기**를 선택하고 열리는 메뉴에서 **Windows 11 Enterprise 버전 22H2**를 선택합니다.

1. **기본 사항** 탭에서 다음 값을 사용하여 VM을 만듭니다.
  | 필드 | 사용할 값 |
  | :-- | :-- |
  | 구독 | Azure Pass - 스폰서쉽 |
  | 리소스 그룹 | 새로 만들기 - rgEntraLogin |
  | 가상 머신 이름 | vmEntraLogin |
  | 지역 | *default* |
  | 가용성 옵션 | 인프라 중복 필요 없음 |
  | 보안 유형 | 표준 |
  | 크기 | Standard DC1s_v3 - 1 vcpu, 8 GiB 메모리 |
  | 관리 사용자 이름 | vmEntraAdmin |
  | 관리자 암호 | 랩 환경에서 제공하는 암호를 사용하거나 기억할 수 있는 안전한 암호를 만듭니다. |
  | 라이선싱 | 라이선스가 있는지 확인 |

1. **디스크** 또는 **네트워킹** 탭에서 아무것도 변경할 필요가 없지만 값을 검토할 수 있습니다.

1. **관리** 탭으로 이동하여 Microsoft Entra ID 섹션에서 **Microsoft Entra ID로 로그인** 확인란을 선택합니다.

        NOTE: You will notice that the **System assigned managed identity** under the Identity section is automatically checked and turned grey. This action should happen automatically once you enable Login with Microsoft Entra ID.

1. **검토 및 만들기**를 선택합니다.

1. **만들기**를 선택하면 됩니다.

#### 작업 2 - 기존 Azure Virtual Machines에 대한 Microsoft Entra ID 로그인

1. [https://portal.azure.com](https://portal.azure.com)에서 **가상 머신**으로 이동합니다.

1. 작업 1에서 새로 만든 Virtual Machine을 선택합니다.

1. **액세스 제어(IAM)** 를 선택합니다.

1. **+ 추가**를 선택한 다음, **역할 할당 추가**를 선택하여 역할 할당 추가 페이지를 엽니다.

1. 다음 설정을 할당합니다.
    - **할당 유형**: 작업 기능 역할
    - **역할**: 가상 머신 관리자 로그인
    - **멤버**: 사용자, 그룹, 서비스 주체를 선택합니다.  그런 다음, **+ 멤버 선택**을 사용하여 **Joni Sherman**을 VM의 특정 사용자로 추가합니다.

1. **검토 + 할당**을 선택하여 프로세스를 완료합니다.

#### 작업 3 - Microsoft Entra ID 로그인을 지원하도록 서버 VM 업데이트

1. **연결** 메뉴에서 **연결** 항목을 선택합니다.

1. **RDP** 탭에서 **RDP 파일 다운로드**를 선택합니다.  메시지가 표시되면 파일에 대한 **유지** 옵션을 선택합니다.  다운로드 폴더에 저장됩니다.

1. 파일 관리자에서 **다운로드** 폴더를 엽니다.

1. RDP를 엽니다.

1. 대체 사용자로 로그인하도록 선택합니다.

1. 가상 머신을 설정할 때 만든 관리자 사용자 이름과 암호를 사용합니다.
   - 메시지가 표시되면 예라고 말하여 가상 머신 또는 RDP 세션에 대한 액세스를 허용합니다.

1. VM이 열리고 모든 소프트웨어가 로드되기를 기다립니다.

1. 가상 머신에서 **시작 단추**를 선택합니다.

1. **제어판**을 입력하고 제어판 앱을 시작합니다.

1. 설정 목록에서 **시스템 및 보안**을 선택합니다.

1. **시스템** 설정에서 **원격 액세스 허용** 옵션을 선택합니다.

  참고 - 시스템 하위 메뉴는 열 필요가 없습니다. 이 옵션은 시스템 헤더에서 사용할 수 있습니다.

1. 열리는 대화 상자 아래쪽에 **원격 데스크톱** 섹션이 표시됩니다.

1. **네트워크 수준 인증을 가진 원격 데스크톱을 실행 중인 컴퓨터에서만 연결 허용**이라고 레이블을 붙인 상자를 **선택 취소**합니다.

1. **적용**을 선택한 다음, **확인**을 선택합니다.

1. 가상 머신 RDP 세션을 **종료**합니다.

#### 작업 4 - Microsoft Entra ID 로그인을 지원하도록 RDP 파일 수정

1. 파일 관리자에서 **다운로드** 폴더를 엽니다.

1. RDP 파일의 **복사본을 만들고** 파일 이름의 끝에 **-EntraID**를 추가합니다.

1. 메모장을 사용하여 방금 복사한 RDP 파일의 새 버전을 편집합니다. 파일의 아래쪽에 이 두 줄의 텍스트를 추가합니다.
     ```
        enablecredsspsupport:i:0
        authentication level:i:2
     ```
 
 1. RDP 파일을 **저장**합니다.  이제 파일이 두 가지 버전으로 있어야 합니다.
      - <<virtual machine name>>.RDP
      - <<virtual machine name>>-EntraID.RDP

#### 작업 5 - Microsoft Entra ID 로그인을 사용하여 Windows 가상 머신에 연결

1. **<<virtual machine name>>-EntraID.RDP를 엽니다.

1. 대화 상자가 열리면 **연결**을 선택합니다.

1. 어떤 사용자 계정으로 로그인할지 묻는 메시지가 표시되는 대신 원격 컴퓨터에 연결할지 여부를 묻는 메시지가 표시됩니다.

1. 페이지 아래쪽에서 **예**를 선택합니다.

1. 원격 데스크톱 세션이 열리고 Windows Server 로그인 화면을 표시합니다.  확인 단추가 있는 **다른 사용자**가 표시되어야 합니다.

1. **확인**을 선택합니다.

1. 로그인 대화 상자에서 다음 정보를 입력합니다.
   - 사용자 이름 = **AzureAD\JoniS@ 도메인 이름**
   - 암호 = 랩 공급자가 제공한 암호 입력

   참고: JoniS는 작업 1 중에 관리자 권한으로 로그인할 수 있는 액세스 권한을 부여한 사용자입니다.

1. Windows에서 로그인을 확인하고 일반 화면으로 열어야 합니다.

#### 작업 6 -- Microsoft Entra ID 로그인을 탐색하는 선택적 테스트

1. 관리자 그룹에 추가된 사용자가 JoniS뿐인지 확인합니다.

1. 시작 단추에서 보조 마우스 클릭을 사용한 다음 팝업 메뉴에서 **컴퓨터 관리**를 선택합니다.

1. **로컬 사용자와 그룹**을 연 다음, **그룹, 관리자**를 탐색합니다.

1. 목록에 **Azure\JoniSherman....** 이 표시됩니다.

1. 다른 Microsoft Entra ID 멤버가 로그인할 수 있는지 확인합니다.

1. 원격 데스크톱 세션에서 로그아웃합니다.

1. **<<server name>>-EntraID.RDP** 파일을 다시 시작합니다.

1. AdeleV 또는 AlexW 또는 DiegoS와 같은 다른 Microsoft Entra 사용자로 로그인해 봅니다.

1. 이런 각 사용자는 액세스가 거부됩니다.

### 선택적 연습 2 - Microsoft Entra ID를 사용하여 Azure에서 Linux Virtual Machines에 로그인

#### 작업 1 - 시스템 할당 관리 ID를 사용하여 Linux VM 만들기

1. [https://portal.azure.com](https://portal.azure.com)으로 이동

1. **+ 리소스 생성**를 선택합니다.

1. **Ubuntu**를 검색합니다.

1. **Ubuntu Server 22.04 LTS**에서 **만들기**를 선택합니다. 이 테스트 랩에 다른 Linux 서버를 사용할 수도 있습니다.

1. **관리** 탭에서 **Microsoft Entra ID로 로그인**을 사용하도록 설정하는 확인란을 선택합니다.

1. **시스템이 할당한 관리 ID**가 선택되어 있는지 확인합니다.

1. 가상 머신을 만드는 과정의 나머지 단계를 진행합니다. 이 미리 보기 중에는 사용자 이름 및 암호 또는 SSH 공개 키를 사용하여 관리자 계정을 만들어야 합니다.

#### 작업 2 - 기존 Azure Virtual Machines에 대한 Microsoft Entra ID 로그인

1. [https://portal.azure.com](https://portal.azure.com)에서 **가상 머신**으로 이동합니다.

1. **액세스 제어(IAM)** 를 선택합니다.

1. 추가 > 역할 할당 추가를 선택하여 역할 할당 추가 페이지를 엽니다.

1. 다음 역할을 할당합니다. 
    - **역할**: Virtual Machine 관리자 로그인 또는 Virtual Machine 사용자 로그인
    - **다음에 대한 액세스 할당**: 사용자, 그룹, 서비스 주체 또는 관리 ID

1. 세부 단계에 대해서는 Azure Portal을 사용하여 Azure 역할 할당을 참조하세요.
