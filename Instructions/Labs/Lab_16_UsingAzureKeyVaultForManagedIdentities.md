---
lab:
  title: 16 - 관리 ID에 Azure Key Vault 사용
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# 랩 16 - 관리 ID에 Azure Key Vault 사용

**참고** - 이 랩에는 Azure Pass가 필요합니다. 지침은 랩 00을 참조하세요.

## 랩 시나리오

Azure 리소스의 관리 ID를 사용할 때 코드에서 Microsoft Entra 인증을 지원하는 리소스에 인증하기 위한 액세스 토큰을 가져올 수 있습니다.  그러나 모든 Azure 서비스가 Microsoft Entra 인증을 지원하는 것은 아닙니다. 이러한 서비스에서 Azure 리소스에 대한 관리 ID를 사용하려면 Azure Key Vault에 서비스 자격 증명을 저장하고 관리 ID로 Key Vault에 액세스하여 자격 증명을 검색합니다.

#### 예상 소요 시간: 20분

### 연습 1 - Azure Key Vault를 사용하여 가상 머신 ID 관리

#### 작업 1 - Windows 가상 머신 만들기

1. [https://portal.azure.com](https://portal.azure.com)으로 이동

1. **+ 리소스 생성**를 선택합니다.

1. Marketplace 검색 창에 **Windows 11**을 입력합니다.

1. **Windows 11**을 선택하고 계획 드롭다운에서 **Windows 11 Enterprise, 버전 21H2**를 선택합니다. 그런 다음, **만들기**를 선택합니다.

1. 기본 탭에서 VM의 관리자 사용자 이름과 암호를 만들어야 합니다.

1. **관리** 탭에서 **시스템 할당 관리 ID 사용** 확인란을 선택합니다.

1. 가상 머신을 만드는 과정의 나머지 단계를 진행합니다. 

1. 만들기를 선택합니다.

#### 작업 2: Key Vault 만들기

1. 전역 관리자 계정을 사용하여 [https://portal.azure.com]( https://portal.azure.com)에 로그인합니다.

1. 왼쪽 탐색 모음 맨 위에서 리소스 만들기를 선택합니다.

1. Marketplace 검색 상자에 **Key Vault**를 입력합니다.  

1. 결과 목록에서 **Key Vault**를 선택합니다.

1. **만들기**를 선택합니다.

1. 아래와 같이 필요한 모든 정보를 입력합니다. 이 랩에 사용 중인 구독을 선택했는지 확인하세요.
    **참고** Key Vault 이름은 고유해야 합니다. 필드 오른쪽에 있는 녹색 확인 표시를 찾습니다.

 - **리소스 그룹** - sc300KeyVaultrg
 - **Key vault 이름** - *anyuniquevalue*
 - **액세스 구성** 페이지에서 **Vault 액세스 정책** 라디오 단추를 선택합니다.
1. **검토 + 만들기**를 선택합니다.

1. **만들기**를 선택합니다.


#### 작업 3 - 비밀 만들기

1. 새로 만든 Key Vault로 이동합니다.

1. **비밀**을 선택합니다.

1. **+ 생성/가져오기**를 선택합니다.

1. 비밀 만들기 화면의 업로드 옵션에서 **수동**을 선택한 상태로 둡니다.

1. 비밀의 이름과 값을 입력합니다.  원하는 어떤 값이나 입력할 수 있습니다. 

1. 활성화 날짜와 만료 날짜는 비워 두고 사용 가능은 예로 유지합니다. 

1. **만들기**를 선택하여 비밀을 만듭니다.

#### 작업 4 - Key Vault에 대한 액세스 권한 부여

1. 새로 만든 Key Vault로 이동합니다.

1. 왼쪽 메뉴에서 **액세스 정책**을 선택합니다.

1. **+ 만들기**를 선택합니다.

1. 템플릿에서 구성(선택 사항) 아래의 액세스 정책 추가 섹션의 풀다운 메뉴에서 비밀 관리를 선택합니다.

1. **보안 주체 선택**에서 **선택하지 않음**을 선택하여 선택할 보안 주체 목록을 엽니다. 검색 필드에 작업 2에서 만든 VM의 이름을 입력합니다.  결과 목록에서 VM을 선택하고 선택을 선택합니다.

1. **추가**를 선택합니다.

1. **저장**을 선택합니다.

#### 작업 5 - PowerShell을 사용하여 Key Vault 비밀로 데이터 액세스

1. 랩 가상 머신에서 PowerShell을 엽니다.  

1. PowerShell에서 테넌트에 대해 웹 요청을 호출하여 VM의 특정 포트에서 로컬 호스트용 토큰을 가져옵니다.  

    ```
    $Response = Invoke-RestMethod -Uri 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fvault.azure.net' -Method GET -Headers @{Metadata="true"}
    ```

1. 다음으로는 응답에서 액세스 토큰을 추출합니다.  

    ```
    $KeyVaultToken = $Response.access_token
    ```

1. PowerShell의 Invoke-WebRequest 명령을 사용하여 앞에서 Key Vault에 만든 비밀을 검색하고 인증 헤더에서 액세스 토큰을 전달합니다.  Key Vault 개요 페이지의 기본 정보 섹션에 있는 Key Vault의 URL이 필요합니다.  미리 알림 - Key Vault 대한 URI가 개요 탭에 있습니다.

    ```
    Invoke-RestMethod -Uri https://<your-key-vault-URI>/secrets/<secret-name>?api-version=2016-10-01 -Method GET -Headers @{Authorization="Bearer $KeyVaultToken"}
    ```
1. 다음과 같은 응답을 받아야 합니다. 
    ```
    'My Secret' https://mi-lab-vault.vault.azure.net/secrets/mi-test/50644e90b13249b584c44b9f712f2e51 @{enabled=True; created=16…
    ```
1. 이 비밀은 이름과 암호가 필요한 서비스에 인증하는 데 사용할 수 있습니다.
