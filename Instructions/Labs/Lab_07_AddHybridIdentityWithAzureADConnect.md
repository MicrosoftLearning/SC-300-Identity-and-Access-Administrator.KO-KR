---
lab:
  title: 07 - Azure AD Connect를 사용하여 하이브리드 ID 추가
  learning path: '01'
  module: Module 01 - Implement an identity management solution
---

# 랩 07: Azure AD Connect를 사용하여 하이브리드 ID 추가

**참고** - 이 랩에는 Azure Pass가 필요합니다. 지침은 랩 00을 참조하세요.

**참고 2** - 이 랩의 제목은 선택 사항입니다.  완료하는 데 최소 1시간 이상이 걸리며 랩 단계에서 자세히 설명해야 합니다.  시간이 허락하는 대로 자유롭게 컴퓨터로 작성해 주세요.  회사에서 하이브리드 구성을 이미 설정했거나 Azure AD Connect를 사용할 계획이 없는 경우 이 랩을 건너뛰세요.

## 랩 시나리오

회사 작업에는 온-프레미스에 Active Directory Domain Services가 있습니다.  ID 및 액세스 관리 솔루션으로 온-프레미스 Active Directory를 계속 사용하려고 하지만 사용자가 동일한 사용자 이름 및 암호를 사용하여 클라우드 애플리케이션에 액세스할 수 있는 기능도 필요합니다.

#### 예상 시간: 60분

### 연습 1 - 온-프레미스 인프라 설정

#### 작업 1 - 온-프레미스 Active Directory 인프라 만들기

1. 배포 템플릿은 다음 링크에서 액세스할 수 있습니다. [온-프레미스 테스트 랩 가이드](https://github.com/maxskunkworks/TLG/tree/master/tlg-base-config_3-vm).

    **학습자 및 MCT 참고 사항** - 이 템플릿의 배포에는 30~60분이 걸릴 수 있으므로 이 단계에서 휴식을 취하거나 과정의 강의 섹션 전에 배포를 실행할 준비를 합니다.

    **랩 공급자 참고 사항** - 가능하면 랩 환경 설정의 일부로 완료하고 배포하는 것이 학생에게 도움이 됩니다.

2. **TLG(테스트 랩 가이드) - 3개의 VM 기본 구성(v1.0)** 페이지에서 **Azure에 배포**를 선택합니다.

   **참고** - 3개의 VM 기본 구성은 지정한 도메인 이름을 사용하여 DC1이라는 Windows Server 2016 Active Directory 도메인 컨트롤러와 Windows Server 2016을 실행하는 APP1이라는 도메인 구성원 서버를 프로비저닝합니다. 또한 이는 Windows 10을 실행하는 클라이언트 VM을 프로비저닝하는 옵션을 제공하지만 랩에서 사용하지 않습니다(주로 Azure에서 Windows 10 VM을 실행할 때 적용되는 라이선스 요구 사항으로 인해). 도메인 구성원 서버(APP1)에 .NET 4.5 및 IIS가 자동으로 설치됩니다.  
   
   **참고** - 이 랩에 필요한 VM은 **DC1**입니다.  Azure Pass를 사용하는 경우 VM이 2개로 제한되어 클라이언트 VM이 실패할 수 있습니다.  이 랩에서는 필요하지 않습니다.

3. **사용자 지정 배포** 페이지에서 다음 설정을 지정한 다음, **검토 + 만들기**를 선택한 다음, **만들기**를 선택합니다.

   -   구독: 랩 환경 Azure VM을 프로비저닝할 대상 Azure 구독의 이름입니다.
   -   리소스 그룹: (새로 만들기) **hybrididentity-RG**
   -   위치: 랩 환경 Azure VM을 호스트할 Azure 지역의 이름입니다.
   -   구성 이름: **TlgBaseConfig-01**
   -   도메인 이름: **corp.contoso.com**
   -   서버 OS: **2016-Datacenter**
   -   관리 사용자 이름: **demouser**
   -   관리자 암호: **기억할 수 있는 안전한 암호 입력**
   -   클라이언트 VM 배포: **‘아니요’**
   -   클라이언트 VHD URI: **비워 둠**
   -   VM 크기: **Standard_D2s_v3**
   
   **참고** - 구독이 나열된 크기를 지원하지 않는 경우 비슷한 VM 크기를 사용합니다. 설명서는 <https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sizes>에 링크되어 있습니다.

   -   DNS 레이블 접두사: **유효하고 전역적으로 고유한 DNS 이름(문자, 숫자, 하이픈으로 구성된 고유한 문자열, 문자로 시작하여 최대 47자 길이).**

   -   _artifacts 위치: **‘기본값을 그대로 적용’**
   -   _artifacts 위치 SAS 토큰: **비워 둠**

4. **검토 + 만들기**를 선택합니다.

5. 유효성 검사를 통과하면 **만들기**를 선택합니다.
    
6. 배포가 완료될 때가지 기다립니다. 약 60분이 소요될 수 있습니다.


### 작업 2 - 랩 환경 Azure VM 구성

1. Azure Portal을 표시하는 브라우저 창에서 **DC1** Azure VM으로 이동하여 원격 데스크톱을 통해 연결합니다. 메시지가 표시되면 다음 자격 증명을 사용하여 로그인합니다.

   -   사용자 이름: **demouser**
   -   암호: **작업 1에서 만든 안전한 암호 사용**

2.  **DC1**에 대한 원격 데스크톱 세션 내에서 **Windows PowerShell ISE**를 시작하고 스크립트 창에 다음 스크립트를 추가한 다음, 실행하여 **DC1** 및 **APP1** Azure VM 모두에서 Internet Explorer 보안 강화 구성 및 사용자 액세스 제어를 사용하지 않도록 설정합니다.

    ```pwsh

    $vmNames = @('dc1','app1')
    Invoke-Command -ComputerName $vmNames {Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0}
    Invoke-Command -ComputerName $vmNames {Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A8-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0}
    Invoke-Command -ComputerName $vmNames {Set-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "ConsentPromptBehaviorAdmin" -Value 00000000}
    ```

    **참고:** 동일한 파일에서 여러 PowerShell 스크립트를 실행하려면 특정 스크립트를 강조 표시하고 녹색 재생 단추 옆에 있는 **선택 영역 실행**을 선택할 수 있습니다. 

3.  **Windows PowerShell ISE** 창 내에서 스크립트 창에 다음 스크립트를 추가하고 실행하여 **DC1* 및 **APP1** Azure VM 모두에 원격 서버 관리 도구를 설치합니다.

    ```pwsh

    $vmNames = @('dc1','app1')
    Invoke-Command -ComputerName $vmNames {Install-WindowsFeature RSAT -IncludeAllSubFeature} 
    ```

4.  **Windows PowerShell ISE** 창 내에서 스크립트 창에 다음 스크립트를 추가하고 실행하여 **DC1* 및 **APP1** Azure VM 모두에 TLS 1.2를 사용하도록 설정합니다.

    ```pwsh

    $vmNames = @('dc1','app1')
    Invoke-Command -ComputerName $vmNames {New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -Force}
    Invoke-Command -ComputerName $vmNames {New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -Force}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'Enabled' -value 1 –PropertyType DWORD}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'DisabledByDefault' -value 0 –PropertyType DWORD}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'Enabled' -value 1 –PropertyType DWORD}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'DisabledByDefault' -value 0 –PropertyType DWORD}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319' -name 'SchUseStrongCrypto' -value 1 –PropertyType DWORD}
    ```

5.  **Windows PowerShell ISE** 창 내에서 스크립트 창에 다음 스크립트를 추가하고 실행하여 **APP1** Azure VM에서 호스트되는 기본 웹 사이트에서 Windows 통합 인증을 구성합니다.

    ```pwsh

    $vmNames = @('app1')
    Invoke-Command -ComputerName $vmNames {Enable-WindowsOptionalFeature -Online -FeatureName IIS-WindowsAuthentication}
    Invoke-Command -ComputerName $vmNames {Set-WebConfigurationProperty -Filter "/system.webServer/security/authentication/anonymousAuthentication" -Name Enabled -Value False -PSPath IIS:\ -Location "Default Web Site"}
    Invoke-Command -ComputerName $vmNames {Set-WebConfigurationProperty -Filter "/system.webServer/security/authentication/windowsAuthentication" -Name Enabled -Value True -PSPath IIS:\ -Location "Default Web Site"}
    ```

### 작업 3 - Azure VM 다시 시작

1. **Windows PowerShell ISE** 창의 콘솔 창에서 다음을 실행하여 **APP1**을 다시 시작합니다.

    ```pwsh

    Restart-Computer -ComputerName 'APP1'
    ```

2. **Windows PowerShell ISE** 창의 콘솔 창에서 다음을 실행하여 **DC1**을 다시 시작합니다.

    ```pwsh
    Restart-Computer -ComputerName 'DC1'
    ```

### 작업 5 - contoso.local Active Directory 구성

1. 원격 데스크톱을 통해 **DC1** Azure VM에 다시 연결합니다. 메시지가 표시되면 다음 자격 증명을 사용하여 로그인합니다.

    -   사용자 이름: **demouser**

    -   암호: **demo\@pass123**
       - **기억할 수 있는 보안 암호를 입력하는 것이 좋습니다.**

2.  **DC1**에 대한 원격 데스크톱 세션 내에서 Internet Explorer를 시작하고 아래 링크로 이동합니다.

    ```
    https://github.com/microsoft/MCW-Hybrid-identity/tree/main/Hands-on%20lab/studentfiles
    ```

3. **Active Directory 데모/테스트 환경용 사용자/그룹 만들기** 페이지에서 **CreateDemoUsers.ps1** 링크를 선택하고, 사용 조건에 동의하고, 해당 스크립트를 로컬 파일 시스템에 저장합니다.

4. **Active Directory 데모/테스트 환경용 사용자/그룹 만들기** 페이지에서 **CreateDemoUsers.csv** 링크(PowerShell 코드 섹션 바로 위)를 선택하고 해당 csv 파일을 **CreateDemoUsers.ps1** 파일과 동일한 위치에 저장합니다.

5. **DC1**에 대한 원격 데스크톱 세션 내에서 파일 탐색기를 시작하고, 두 파일을 모두 다운로드한 폴더로 이동하고, **CreateDemoUsers.ps1** 파일을 마우스 오른쪽 단추로 선택하고, **속성**을 선택하고, **CreateDemoUsers.ps1 속성** 대화 상자에서 **차단 해제** 확인란을 선택하고, **확인**을 선택합니다.

6. 파일 탐색기 창에서 **CreateDemoUsers.ps1** 파일을 다시 마우스 오른쪽 단추로 선택하고 **편집**을 선택합니다. 

7. **관리자: Windows PowerShell ISE** 창에서 다음에서 줄 **148**을 변경합니다.

    ```pwsh
    $UserCount = 1000 #Up to 2500 can be created
    ```

   을
    ```pwsh
    $UserCount = 2500 #Up to 2500 can be created
    ```

8. **Windows PowerShell ISE** 창에서 변경 사항을 저장하고 **CreateDemoUsers.ps1** 스크립트를 실행하여 랩 환경 조직 구성 단위 계층 구조를 만들고 테스트 사용자 계정으로 채웁니다. 

9.  **Windows PowerShell ISE** 창 내에서 스크립트 창에 다음 스크립트를 추가하고 실행하여 이 랩에서 사용할 AD 사용자 계정의 설정을 수정합니다.

    ```pwsh

    $adUser1 = Get-ADUser -Filter {samAccountName -eq "AGAyers"}
    $adUser1groups = $adUser1 | Get-ADPrincipalGroupMembership 
    $adUser1groups | foreach { if ($_.name -ne 'Domain Users') {Remove-ADPrincipalGroupMembership -MemberOf $_.name -Identity $adUser1.DistinguishedName} }
    Add-ADPrincipalGroupMembership -MemberOf 'Engineering' -Identity $adUser1.DistinguishedName
    Move-ADObject -Identity $adUser1.DistinguishedName -TargetPath 'OU=NJ,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'

    Set-ADAccountPassword -Identity 'CN=Ayers\, Ann,OU=NJ,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com' -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "demo@pass123" -Force)

    $adUser2 = Get-ADUser -Filter {samAccountName -eq "TFBell"}
    $adUser2groups = $adUser2 | Get-ADPrincipalGroupMembership 
    $adUser2groups | foreach { if ($_.name -ne 'Domain Users') {Remove-ADPrincipalGroupMembership -MemberOf $_.name -Identity $adUser2.DistinguishedName} }
    Add-ADPrincipalGroupMembership -MemberOf 'Engineering' -Identity $adUser2.DistinguishedName
    Move-ADObject -Identity $adUser2.DistinguishedName -TargetPath 'OU=VT,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'

    Set-ADAccountPassword -Identity 'CN=Bell\, Teresa,OU=VT,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com' -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "demo@pass123" -Force)
    Get-ADGroup -Identity 'Domain Admins' | Add-ADGroupMember -Members 'CN=Ayers\, Ann,OU=NJ,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'
    Get-ADGroup -Identity 'Enterprise Admins' | Add-ADGroupMember -Members 'CN=Ayers\, Ann,OU=NJ,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'
    ```

10. **Windows PowerShell ISE** 창 내에서 스크립트 창에 다음 스크립트를 추가하고 실행하여 **서버** 및 **클라이언트**라는 추가 조직 구성 단위를 만들고 **APP1** 컴퓨터 계정을 첫 번째 구성 요소로 이동합니다.

    ```pwsh

    New-ADOrganizationalUnit -Name 'Servers' -Path 'OU=Demo Accounts,DC=corp,DC=contoso,DC=com'
    New-ADOrganizationalUnit -Name 'Clients' -Path 'OU=Demo Accounts,DC=corp,DC=contoso,DC=com'

    Move-ADObject -Identity 'CN=APP1,CN=Computers,DC=corp,DC=contoso,DC=com' -TargetPath 'OU=Servers,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'
    ```

11. **DC1**에서 로그아웃합니다.

## 연습 2: Azure Active Directory 테넌트와 Active Directory 포리스트 통합

### 작업 1: Azure Active Directory 테넌트 만들기 및 EMS E5 평가판 활성화

이 작업에서는 다음 설정을 사용하여 Azure Active Directory 테넌트를 만듭니다. 

-   조직 이름: **Contoso**

-   초기 도메인 이름: 유효하고 고유한 도메인 이름입니다.

-   국가/지역: **미국**

1. 랩 컴퓨터에서 새 웹 브라우저 창을 시작하고 아직 시작하지 않은 경우 <https://portal.azure.com>에서 Azure Portal로 이동합니다.

2. 메시지가 표시되면 이전 실습 랩 연습에서 리소스를 배포한 Azure 구독에 로그인합니다.

3. 랩 컴퓨터의 Azure Portal에서 **+ 리소스 만들기**를 선택합니다.

4. **새** 페이지의 **Marketplace 검색** 텍스트 상자에 **Azure Active Directory**를 입력하고 결과 목록에서 **Azure Active Directory**를 선택합니다.

5. **Azure Active Directory** 페이지에서 **만들기**를 선택합니다.

6. **디렉터리 만들기** 페이지에서 다음 설정을 지정하고 **만들기**를 선택합니다.

기본 탭:
    -   테넌트 유형 선택에서 **Azure Active Directory**를 선택합니다.

구성 탭:
    -   조직 이름: **Contoso**

    -   초기 도메인 이름: 유효하고 고유한 도메인 이름입니다.

    -   국가/지역: **미국**

7. 만들어지면 **Azure Active Directory**를 엽니다.

8. 개요 페이지에서 **테넌트 관리**를 선택합니다.

9. 새로 만든 디렉터리에 확인 표시를 합니다.

10. 페이지 위쪽에서 **전환**을 선택합니다.

    >**참고**: 모든 항목이 제대로 표시되려면 몇 분 정도 걸릴 수 있습니다.

11. **Contoso - 개요** 페이지에서 **사용자**를 선택합니다.

12. 이 새 테넌트에서는 ExternalAzureAD 사용자가 한 명 있습니다.

### 작업 2: 이 디렉터리를 관리하도록 Azure AD 사용자 만들기 및 구성

1. 랩 컴퓨터의 Azure Portal에서 **Contoso - 개요** 페이지로 다시 이동합니다.

2. **Contoso - 개요** 페이지의 왼쪽 탐색 창에서 **관리** 아래에서 **사용자**를 선택합니다.

3. **사용자 - 모든 사용자** 페이지에서 사용자 계정을 나타내는 항목을 선택합니다.

4. 사용자 계정의 **프로필** 페이지에서 **편집**을 선택합니다.

5. **설정** 섹션의 **사용 위치** 드롭다운 목록에서 **미국** 항목을 선택하고 **저장**을 선택합니다.

#### 새 관리자 만들기

6. **새 사용자** 페이지에서 **사용자 만들기** 옵션이 선택되어 있는지 확인하고 다음 설정을 지정한 다음, **만들기**를 선택합니다.

    - 사용자 이름: **john.doe @your Azure AD 테넌트 도메인 이름 ** 여기서 ***Azure AD 테넌트 도메인 이름***은 Contoso Azure AD 테넌트를 만들 때 지정한 도메인 이름입니다.

    - 이름: **john.doe**

    - 이름: **John**

    - 성: **Doe**
    
    - 암호: **자동 생성 암호**
    
    - 암호 표시: **사용**을 선택한 다음, 암호를 복사해야 합니다.

    - 그룹: **선택한 그룹 0개**
    
    - 역할: **전역 관리자**
    
    - 로그인 차단: **아니요**
    
    - 사용 위치: **미국**
    
    - 직위: **비워 둠**
    
    - 부서: **비워 둠**

    > **참고**: **사용자 이름** 및 **암호** 값을 메모장에 복사합니다. 이 랩의 뒷부분에서 계정 이름이 필요합니다.


### 작업 5: Contoso Active Directory 포리스트에서 DNS 접미사 구성

이 작업에서는 새로 확인된 Azure AD 사용자 지정 도메인 이름과 일치하도록 Contoso Active Directory 포리스트의 DNS 접미사를 구성합니다.

1. 랩 컴퓨터에서 Azure Portal의 이전 실습 랩 연습(**기본 디렉터리**)에서 리소스를 배포한 Azure 구독과 연결된 Azure AD 테넌트에 로그인했는지 확인합니다. 그렇지 않은 경우 Azure Portal의 도구 모음에서 **디렉터리 + 구독** 아이콘(**Cloud Shell** 아이콘 오른쪽)을 선택하여 해당 Azure AD 테넌트로 전환합니다. 

2. Azure Portal에서 **DC1** 가상 머신의 페이지로 이동합니다.

3. **DC1** 가상 머신 페이지에서 원격 데스크톱을 통해 **DC1**에 연결합니다. 로그인하라는 메시지가 표시되면 **demouser** 이름과 **demo\@pass123** 암호를 사용합니다. 

4. **DC1**에 대한 원격 데스크톱 세션의 **서버 관리자** 창에서 **도구** 아래에서 **Active Directory 도메인 및 트러스트** 콘솔을 시작합니다. 

5. **Active Directory 도메인 및 트러스트** 콘솔에서 왼쪽에서 **Active Directory 도메인 및 트러스트[DC1.corp.contoso.com]** 를 마우스 오른쪽 단추로 선택하고 **속성**을 선택합니다.

6. **Active Directory 도메인 및 트러스트[DC1.corp.contoso.com]** 창의 **UPN 접미사** 탭의 **대체 UPN 접미사** 텍스트 상자에 이전 작업에서 확인한 사용자 지정 도메인의 이름을 입력하고 **추가**를 선택한 다음, **확인**을 선택합니다.

7. **DC1**에 대한 원격 데스크톱 세션의 **서버 관리자** 창에서 **도구** 아래에서 **Active Directory 사용자 및 컴퓨터** 콘솔을 시작합니다. 

8. **Active Directory 사용자 및 컴퓨터** 콘솔에서 왼쪽의 **corp.contoso.com**을 확장하고 도메인의 조직 구성 단위 계층 구조와 도메인 그룹의 그룹 멤버 자격을 검사합니다. 

9.  **DC1**에 대한 원격 데스크톱 세션 내에서 Windows PowerShell ISE를 시작하고 스크립트 창에서 다음을 실행하여 **엔지니어링** 그룹의 구성원인 모든 사용자의 UPN 접미사를 Contoso Azure AD 테넌트의 사용자 지정 확인된 도메인 이름과 일치하는 것으로 바꿉니다(`<custom_domain_name>` 자리 표시자를 Contoso Azure AD 테넌트에 할당한 사용자 지정 확인된 도메인 이름의 실제 이름으로 바꿈). 

    ```pwsh
    $domainName = '<custom_domain_name>'
    $users = Get-ADGroupMember -Identity 'Engineering' -Recursive | Where-Object {$_.objectClass -eq 'user'}

    foreach ($user in $users) {
        $user = Get-ADUser -Identity $User.SamAccountName
        $userName = $user.UserPrincipalName.Split('@')[0] 
        $upn = $userName + "@" + $domainName 
        $user | Set-ADUser -UserPrincipalName $upn
    }
    ```

### 작업 6: Azure AD Connect 설치

이 작업에서는 Azure AD Connect를 설치합니다.

1. **DC1**에 대한 원격 데스크톱 세션 내에서 서버 관리자에서 **로컬 서버**를 선택하고 **IE 보안 강화 구성**이 사용하지 않도록 설정되어 있는지 확인합니다. 그렇지 않은 경우 **IE 보안 강화 구성** 옆의 **켜기** 링크를 선택하고 **관리자** 설정을 **끄기**로 설정하고 **확인**을 선택합니다.

2. **DC1**에 대한 원격 데스크톱 세션 내에서 **Windows PowerShell ISE** 창을 열고 이 명령을 실행하여 Chrome 브라우저를 설치합니다.

    ```pwsh
    $LocalTempDir = $env:TEMP; $ChromeInstaller = "ChromeInstaller.exe"; (new-object System.Net.WebClient).DownloadFile('http://dl.google.com/chrome/install/375.126/chrome_installer.exe', "$LocalTempDir\$ChromeInstaller"); & "$LocalTempDir\$ChromeInstaller" /silent /install; $Process2Monitor = "ChromeInstaller"; Do { $ProcessesFound = Get-Process | ?{$Process2Monitor -contains $_.Name} | Select-Object -ExpandProperty Name; If ($ProcessesFound) { "Still running: $($ProcessesFound -join ', ')" | Write-Host; Start-Sleep -Seconds 2 } else { rm "$LocalTempDir\$ChromeInstaller" -ErrorAction SilentlyContinue -Verbose } } Until (!$ProcessesFound)
    ```

2. **DC1**에 대한 원격 데스크톱 세션 내에서 Chrome 브라우저를 시작하고 <https://portal.azure.com>에서 Azure Portal로 이동합니다.

3. 로그인하라는 메시지가 표시되면 이 연습의 앞부분에서 메모장에 복사한 **john.doe** Azure AD 사용자 계정의 자격 증명을 입력합니다.

4. 메시지가 표시되면 **john.doe** 사용자 계정의 암호를 변경합니다. 
  
    > **참고**: **이 암호는 전에도 너무 많이 봤습니다. 추측하기 어려운 것을 선택하세요.** 메시지를 받으면 암호가 허용될 만큼 고유할 때까지 암호를 수정해야 합니다.

5. **로그인 상태를 유지하시겠습니까?** 여부를 묻는 메시지가 표시되면 **아니요**를 선택합니다. Azure Portal 인터페이스로 리디렉션됩니다. 

6. **Microsoft Azure 시작** 대화 상자가 표시되면 **나중에**를 선택합니다. 

7. Azure Portal의 포털 왼쪽 탐색 메뉴에서 **Azure Active Directory**를 선택하여 **Contoso - 개요** 페이지로 이동합니다.

8. **Contoso - 개요** 페이지에서 왼쪽의 **관리** 아래에서 **Azure AD Connect**를 선택합니다.

9.  **Azure AD Connect** 페이지에서 **Azure AD Connect 다운로드** 링크를 선택합니다.  그런 다음, 메뉴에서 **동기화 연결**을 선택합니다.

10. Microsoft 다운로드 사이트의 **Microsoft Azure Active Directory Connect** 웹 페이지에서 **다운로드**를 선택합니다.

11. **AzureADConnect.msi**를 실행할지 저장할지 묻는 메시지가 표시되면 **실행**을 선택합니다. 그러면 파일이 다운로드되고 **Microsoft Azure Active Directory Connect** 마법사가 자동으로 시작됩니다. 

12. **Azure AD Connect 시작** 페이지에서 **라이선스 약관 및 개인정보 보호정책에 동의합니다** 확인란을 선택하고 **계속**을 선택합니다.

13. **기본 설정** 페이지에서 **사용자 지정** 단추를 선택합니다.

14. **필수 구성 요소 설치** 페이지에서 모든 선택적 구성 옵션의 선택을 취소하고 **설치**를 선택합니다.

15. **사용자 로그인** 페이지에서 **통과 인증** 옵션과 **Single Sign-On 사용** 확인란을 선택하고 **다음**을 선택합니다.

16. **Azure AD에 연결** 페이지에서 **john.doe** 계정의 자격 증명을 사용하여 로그인하고 **다음**을 선택합니다.

17. **디렉터리 연결** 페이지에서 **포리스트** 드롭다운 목록에 **corp.contoso.com** 항목이 표시되는지 확인하고 **디렉터리 추가**를 선택합니다. **AD 포리스트 계정**에서 **새 AD 계정 만들기** 옵션이 선택되어 있는지 확인하고 **ENTERPRISE ADMIN USERNAME** 텍스트 상자에 **CORP.CONTOSO.COM\\demouser**를 입력하고 **PASSWORD** 텍스트 상자에 **demo\@pass123**을 입력하고 **확인**을 선택합니다.


18. **디렉터리 연결** 페이지로 돌아가서 **다음**을 선택합니다.

19. **Azure AD 로그인 구성** 페이지에서 사용자 지정 도메인 이름이 확인된 **Active Directory UPN 접미사**로 나열되고 **userPrincipalName** 항목이 **USER PRINCIPAL NAME** 드롭다운 목록에 표시되는지 확인합니다. **UPN 접미사가 확인된 도메인 이름과 일치하지 않으면 사용자가 온-프레미스 자격 증명으로 Azure AD에 로그인할 수 없음**이라는 경고에 유의하세요. **확인된 도메인에 모든 UPN 접미사를 일치시키지 않고 계속** 확인란을 선택하고 **다음**을 선택합니다. 

    >**참고**: 일부 사용자는 라우팅할 수 없고 Azure AD 테넌트의 확인된 사용자 지정 도메인 이름으로 구성할 수 없는 **contoso.local** UPN 접미사로 구성되기 때문입니다.

20. **도메인 및 OU 필터링** 페이지에서 **선택한 도메인 및 OU 동기화**를 선택한 다음, **DemoAccounts** OU 및 자식 OU가 모두 선택되었는지 확인하고 **다음**을 선택합니다. 


21. **사용자 고유 식별** 페이지에서 기본 설정을 수락하고 **다음**을 선택합니다. 


22. **사용자 및 디바이스 필터링** 페이지에서 기본 설정을 수락하고 **다음**을 선택합니다. 

23. **선택적 기능** 페이지에서 기본 설정을 수락하고 **다음**을 선택합니다.

24. **Single Sign-On 사용** 페이지에서 **자격 증명 입력**을 선택하고, **포리스트 자격 증명** 대화 상자에서 **CORP\\demouser** 사용자 이름 및 **demo\@pass123** 암호로 로그인하고, **다음**을 선택합니다.


25. **구성 준비 완료** 페이지에서 **구성이 완료되면 동기화 프로세스 시작** 확인란이 선택되지 **않았는지** 확인하고 **설치**를 선택합니다.


   > **참고**: 동기화 프로세스를 사용하도록 설정하기 전에 특성 수준 필터링을 구성합니다.

   > **참고**: 설치에는 약 2분이 소요됩니다.

26. **구성 완료** 페이지에서 **끝내기**를 선택합니다.


### 작업 7: Active Directory 휴지통 사용

이 작업에서는 Contoso Active Directory 도메인에서 휴지통을 사용하도록 설정합니다. 

1. **DC1**에 대한 원격 데스크톱 세션 내에서 서버 관리자 콘솔의 도구 메뉴에서 **Active Directory 관리 센터**를 시작합니다.


2. **Active Directory 관리 센터** 콘솔의 왼쪽에서 **corp(로컬)** 를 마우스 오른쪽 단추로 선택하고 **휴지통 사용**을 선택합니다. 작업을 확인하라는 메시지가 표시되면 **확인**을 선택합니다.


3. AD 관리 센터를 새로 고치라는 메시지가 표시되면 **확인**을 선택합니다.

   > **참고**: 하이브리드 시나리오에서 휴지통의 이점에 대한 자세한 내용은 <https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-sync-recycle-bin>을 참조하세요.

### 작업 8: Azure AD Connect 특성 수준 필터링 구성

이 작업에서는 대상 Azure AD 테넌트의 사용자 지정 도메인 이름과 일치하는 UPN 접미사가 있는 사용자 계정의 동기화를 제한하는 Azure AD Connect 특성 수준 필터링을 구성합니다.

   > **참고**: 긍정 필터링 옵션에는 두 개 이상의 동기화 규칙이 필요합니다. 그 중 하나는 동기화할 개체의 올바른 범위를 결정합니다. 두 번째 포괄적인 동기화 규칙은 동기화해야 하는 개체로 아직 식별되지 않은 모든 개체를 필터링합니다.

1. **DC1**에 대한 원격 데스크톱 세션 내에서 시작 메뉴의 **Azure AD Connect**에서 **동기화 규칙 편집기**를 시작합니다.


2. 동기화 규칙 편집기 창의 **동기화 규칙 보기 및 관리** 페이지에서 **인바운드**가 **방향** 드롭다운 목록에 표시되는지 확인하고 **새 규칙 추가**를 선택합니다. 그러면 **인바운드 동기화 규칙 만들기** 마법사가 시작됩니다.


3. **인바운드 동기화 규칙 만들기 - 설명** 페이지에서 다음 설정을 지정하고 **다음**을 선택합니다.

    - 이름: **AD에서 사용자 지정 인바운드 - UPN 필터**

    - 설명: **사용자 지정 인바운드 규칙 - UPN이 Azure AD 사용자 지정 도메인과 일치하도록 설정된 사용자를 포함합니다.**

    - 연결된 시스템: **corp.contoso.com**

    - 연결된 시스템 개체 형식: **사용자**

    - 메타버스 개체 형식: **사람**

    - 링크 형식: **조인**

    - 우선 순위: **50**

    - 태그: **비워 둡니다**.

    - 암호 동기화 사용: **비워 둡니다**.

    - 사용 안 함: **비워 둡니다**.


4. **인바운드 범위 지정 필터 만들기** 페이지에서 **그룹 추가**를 선택하고, 다음을 지정하는 **추가 절**을 선택하고, **다음**을 선택합니다.

    - 특성: **userPrincipalName**

    - 연산자: **ENDSWITH**

    - 값: **\@\<your custom domain name>**

5. **조인 규칙** 페이지에서 **다음**을 선택합니다.

6. **변환** 페이지에서 **변환 추가**를 선택하고 다음을 지정하고 **추가**를 선택합니다.

    - FlowType: **Constant**

    - 대상 특성: **cloudFiltered**

    - 원본: **False**

7. **다음 동기화 주기 동안 ‘corp.contoso.com’에서 전체 가져오기 및 전체 동기화가 실행됨** 메시지를 표시하는 **경고** 대화 상자가 표시되면 **확인**을 선택합니다.

   > **참고**: 이렇게 하면 규칙 목록 맨 위에 새 규칙이 나열되어 있는 동기화 규칙 인터페이스를 다시 보고 관리해야 합니다. 

8. **동기화 규칙 편집기** 창으로 돌아가서 **동기화 규칙 보기 및 관리** 페이지에서 **인바운드**가 **방향** 드롭다운 목록에 나타나는지 확인하고 **새 규칙 추가**를 다시 선택합니다. 그러면 **인바운드 동기화 규칙 만들기** 마법사가 시작됩니다.

9. **설명** 페이지에서 다음 설정을 지정하고 **다음**을 선택합니다.

    - 이름: **AD에서 사용자 지정 인바운드 - 포괄적인 필터**

    - 설명: **사용자 지정 인바운드 규칙 - Azure AD 사용자 지정 도메인과 일치하도록 UPN이 설정되지 않은 모든 사용자를 제외합니다.**

    - 연결된 시스템: **corp.contoso.com**

    - 연결된 시스템 개체 형식: **사용자**

    - 메타버스 개체 형식: **사람**

    - 링크 형식: **조인**

    - 우선 순위: **51**

    - 태그: **비워 둡니다**.

    - 암호 동기화 사용: **비워 둡니다**.

    - 사용 안 함: **비워 둡니다**.


10. **범위 지정 파일러** 페이지에서 **다음**을 선택합니다.

11. **조인 규칙** 페이지에서 **다음**을 선택합니다.

12. **변환** 페이지에서 **변환 추가**를 선택하고 다음을 지정하고 **추가**를 선택합니다.

    - FlowType: **Constant**

    - 대상 특성: **cloudFiltered**

    - 원본: **True**

13. **다음 동기화 주기 동안 ‘corp.contoso.com’에서 전체 가져오기 및 전체 동기화가 실행됨** 메시지를 표시하는 **경고** 대화 상자가 표시되면 **확인**을 선택합니다.

    >**참고**: 이렇게 하면 **동기화 규칙 보기 및 관리** 인터페이스로 돌아가고 규칙 목록 상단에 새 규칙이 나열됩니다. 

### 작업 9: 디렉터리 동기화 시작 및 확인

1. **DC1**에 대한 원격 데스크톱 세션 내에서 **Azure AD Connect** 데스크톱 바로 가기를 두 번 선택합니다.

2. **Azure AD Connect 시작** 페이지에서 **구성**을 선택합니다. 

3. **추가 작업** 페이지에서 **동기화 옵션 사용자 지정**을 선택하고 **다음**을 선택합니다.

4. **Azure AD에 연결** 페이지에서 **john.doe** 계정의 자격 증명을 사용하여 로그인하고 **다음**을 선택합니다.

5. **디렉터리 연결** 페이지에서 **다음**을 선택합니다.

6. **도메인 및 OU 필터링** 페이지에서 **다음**을 선택합니다. 

7. **선택적 기능** 페이지에서 기본 설정을 수락하고 **다음**을 선택합니다.

8. **Single Sign-On 사용** 페이지에서 **다음**을 선택합니다.

9. **구성 준비 완료** 페이지에서 **구성이 완료되면 동기화 프로세스 시작** 확인란을 선택하고 **구성**을 선택합니다.

10. **구성 완료** 페이지에서 **끝내기**를 선택합니다.

11. **DC1**에 대한 원격 데스크톱 세션 내에서 Azure Portal을 표시하는 Edge 브라우저 창에서 Contoso Azure AD 테넌트의 **사용자 - 모든 사용자** 페이지로 이동합니다.

12. **사용자 - 모든 사용자** 페이지에서 사용자 개체 목록에는 Azure AD 테넌트의 사용자 지정 도메인 이름과 일치하는 UPN 접미사가 있는 모든 사용자 계정이 포함됩니다. 페이지를 새로 고치거나 변경 내용을 보려면 몇 분 정도 기다려야 할 수 있습니다.

13. Azure Portal에서 Contoso Azure AD 테넌트의 **그룹 - 모든 그룹** 페이지로 이동하고 모든 corp.contoso.com 도메인 그룹도 동기화되었음을 확인합니다. 

14. Azure Portal에서 **Contoso - Azure AD Connect** 페이지로 이동하고 왼쪽에서 **Azure AD Connect**를 선택합니다. 다음 설정이 지정되었는지 확인합니다. 

    - Azure AD Connect동기화 상태: **사용** 
  
    - 마지막 동기화: **이는 일종의 타임스탬프여야 합니다**. 
  
    - 암호 해시 동기화: **Disabled** 
  
    - 페더레이션: **Disabled**
   
    - 원활한 Single Sign-On: **1개의 도메인에 대해 사용** 
  
    - 통과 인증: **에이전트 1개로 사용**

   > **참고**: 프로덕션 환경에서 중복성을 위해 추가 에이전트를 설치합니다. 자세한 내용은 <https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-pta-quick-start>을 참조하십시오.

### 작업 10: 하이브리드 Azure AD 조인 구성

이 작업에서는 Azure AD 디바이스 동기화 옵션을 구성합니다.

1. **DC1**에 대한 원격 데스크톱 세션 내에서 **Azure AD Connect** 데스크톱 바로 가기를 두 번 선택합니다.

2. **Azure AD Connect 시작** 페이지에서 **구성**을 선택합니다. 

3. **추가 작업** 페이지에서 **디바이스 옵션 구성**을 선택하고 **다음**을 선택합니다.

4. **개요** 페이지에서 **하이브리드 Azure AD 조인** 및 **디바이스 쓰기 저장**에 대한 정보를 검토하고 **다음**을 선택합니다.

5. **Azure AD에 연결** 페이지에서 **john.doe** 계정의 자격 증명을 사용하여 로그인하고 **다음**을 선택합니다.

6. **디바이스 옵션** 페이지에서 **하이브리드 Azure AD 조인 구성** 옵션이 선택되어 있는지 확인하고 **다음**을 선택합니다. 

7. **디바이스 운영 체제** 페이지에서 **Windows 10 이상의 도메인 조인 디바이스** 및 **지원되는 Windows 하위 수준 도메인 조인 디바이스** 확인란을 선택하고 **다음**을 선택합니다. 

   > **참고**: Windows 하위 수준 디바이스는 페더레이션 도메인에 대한 AD FS처럼 관리되는 도메인 또는 페더레이션 서비스에 대한 원활한 SSO를 사용하는 경우에만 지원됩니다.

8. **SCP 구성** 페이지에서 **corp.contoso.com** Active Directory 포리스트 상자를 선택하고 **인증 서비스** 드롭다운 목록에서 **Azure Active Directory** 항목을 선택한 다음, **추가**를 선택합니다.

9. corp.contoso.com에 대한 Enterprise 관리자 자격 증명을 입력하라는 메시지가 표시되면 **Windows 보안** 대화 상자에서 **CORP\\demouser** 사용자 이름과 **demo\@pass123** 암호를 사용하여 로그인합니다.

10. **SCP 구성** 페이지로 돌아가 **다음**을 선택합니다.

11. **구성 준비** 페이지에서 **구성**을 선택합니다.

12. **구성 완료** 페이지에서 작업이 성공적으로 완료되었는지 확인하고 **종료**를 선택합니다.


### 작업 11: 하이브리드 Azure AD 조인 수행

1. 랩 컴퓨터에서 Azure Portal의 이전 실습 랩 연습(**기본 디렉터리**)에서 리소스를 배포한 Azure 구독과 연결된 Azure AD 테넌트에 로그인했는지 확인합니다. 그렇지 않은 경우 Azure Portal의 도구 모음에서 **디렉터리 + 구독** 아이콘(**Cloud Shell** 아이콘 오른쪽)을 선택하여 해당 Azure AD 테넌트로 전환합니다. 

2. Azure Portal에서 **APP1** 가상 머신의 페이지로 이동합니다.

3. **APP1** 가상 머신 페이지에서 원격 데스크톱을 통해 **APP1**에 연결합니다. 로그인하라는 메시지가 표시되면 **demo@pass123** 암호와 함께 **AGAyers\@<custom_domain_name>** 사용자 이름을 사용합니다(여기서 **<custom_domain_name>** 자리 표시자는 이 연습의 앞부분에서 Contoso Azure AD 테넌트에 할당한 사용자 지정 DNS 도메인 이름을 나타냅니다.

4. **APP1**에 대한 원격 데스크톱 세션 내에서 **서버 관리자** 창에서 **도구** 아래에서 **작업 스케줄러**를 시작합니다. 


5. **작업 스케줄러** 콘솔에서 **작업 스케줄러 라이브러리** > **Microsoft** > **Windows** > **작업 영역 조인**으로 이동합니다. 여기에서 **Automatic-Device-Join** 작업을 활성화한 다음, 실행합니다. 


6. **DC1**에 대한 원격 데스크톱 세션으로 전환하고 Windows PowerShell ISE 창의 콘솔 창에서 다음을 실행하여 Azure AD Connect 델타 동기화를 시작합니다.

   ```pwsh
   Import-Module -Name 'C:\Program Files\Microsoft Azure AD Sync\Bin\ADSync\ADSync.psd1'
   
   Start-ADSyncSyncCycle -PolicyType Delta
   ```

7. **APP1**에 대한 원격 데스크톱 세션으로 다시 전환하고 **명령 프롬프트**를 시작합니다.

8. 명령 프롬프트 창에서 다음을 실행하여 APP1의 Azure AD 등록 상태를 확인합니다. 

   ```
   dsregcmd /status
   ```

9. 명령의 출력이 다음과 유사한지 확인합니다.

   ```
   +----------------------------------------------------------------------+
   | Device State                                                         |
   +----------------------------------------------------------------------+

        AzureAdJoined : YES
     EnterpriseJoined : NO
             DeviceId : 61eea2b8-efbe-43d9-b267-126433c8ee34
           Thumbprint : BBAAA0FB4A55E880388851BED955A2669A961A96
       KeyContainerId : 2eb75eb8-0a1d-437b-99d9-9dd161ca0d90
          KeyProvider : Microsoft Software Key Storage Provider
         TpmProtected : NO
         KeySignTest: : PASSED
                  Idp : login.windows.net
             TenantId : xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx
           TenantName : xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx
          AuthCodeUrl : https://login.microsoftonline.com/xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx/oauth2/authorize
       AccessTokenUrl : https://login.microsoftonline.com/xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx/oauth2/token
               MdmUrl :
            MdmTouUrl :
     MdmComplianceUrl :
          SettingsUrl :
       JoinSrvVersion : 1.0
           JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/
            JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net
        KeySrvVersion : 1.0
            KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/
             KeySrvId : urn:ms-drs:enterpriseregistration.windows.net
         DomainJoined : YES
           DomainName : CORP

   +----------------------------------------------------------------------+
   | User State                                                           |
   +----------------------------------------------------------------------+

               NgcSet : NO
      WorkplaceJoined : NO
        WamDefaultSet : NO
           AzureAdPrt : NO

   +----------------------------------------------------------------------+
   | Ngc Prerequisite Check                                               |
   +----------------------------------------------------------------------+

        IsUserAzureAD : NO
        PolicyEnabled : NO
       DeviceEligible : YES
   SessionIsNotRemote : NO
     X509CertRequired : NO
         PreReqResult : WillNotProvision

   ```
11. **DC1**에 대한 원격 데스크톱 세션으로 다시 전환하고, Azure Portal을 표시하는 Edge 브라우저 창에서 Contoso Azure AD 테넌트의 **디바이스 - 모든 디바이스** 페이지로 이동하여 **조인 형식**이 **하이브리드 Azure AD 조인됨** 상태에서 APP1 서버를 나타내는 항목이 있는지 확인합니다.

   > **참고**: Azure AD 등록 상태가 올바르게 보고되고 Azure AD 개체가 Azure Portal에 나타날 때까지 기다려야 할 수 있습니다.


