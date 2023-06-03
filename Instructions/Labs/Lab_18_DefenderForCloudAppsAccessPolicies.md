---
lab:
  title: 18 - 클라우드용 Defender Apps 액세스 정책
  learning path: '03'
  module: Module 03 - Implement Access Management for Apps
---

# 18 - 클라우드용 Defender Apps 액세스 및 세션 정책

## 랩 시나리오

클라우드용 Microsoft Defender Apps를 사용하여 모니터링하는 클라우드 앱과 관련된 추가 조건부 액세스 정책을 만들 수 있습니다.  이러한 정책 만들기는 클라우드용 Microsoft Defender Apps 포털 내의 제어 메뉴 내에서 수행할 수 있습니다.

#### 예상 소요 시간: 20분

### 연습 1 - 조건부 액세스 앱 제어 정책 만들기 및 테스트

#### 작업 1 - PradeepG에 FORMS에 대한 무조건적인 액세스 권한이 있는지 확인

1. 새 **InPrivate 탐색**창을 시작합니다.
2. [https://forms.microsoft.com](https://forms.microsoft.com)에 연결합니다.
3. 페이지의 오른쪽 위에서 로그인을 클릭합니다.
4. Pradeep Gupta로 로그인합니다.
   - 사용자 이름 = PradeepG@<<<your lab hoster provided domain>>>
   - 암호 = 리소스 탭의 암호
5. Microsoft Forms가 열리고 경고 메시지가 표시되지 않는지 확인합니다.
6. InPrivate 검색 창을 닫습니다.

#### 작업 2 - Defender for Cloud Apps에서 작동하도록 Azure AD 구성

1. [portal.azure.com](portal.azure.com)으로 이동하고 Azure Active Directory로 이동합니다.

2. **관리**에서 **보안**을 선택 합니다.

3. **보호**에서 **조건부 액세스**를 선택합니다.

4. **+ 새 정책** 드롭다운을 선택하고 **새 정책 만들기**를 선택합니다.

5. **Forms를 사용하여 Pradeep 모니터링**과 같은 정책 이름을 입력합니다.

6. **사용자 또는 워크로드 ID**에서 **특정 사용자 포함**을 선택하고 **사용자 및 그룹 선택**을 선택하고 **사용자 및 그룹**을 표시합니다.

7. 랩 테넌트에 대한 **Pradeep Gupta** 계정을 선택하고 **선택**을 선택합니다.

8. **클라우드 앱 또는 작업**에서 **선택한 클라우드 앱, 작업 또는 인증 컨텍스트가 없습니다**를 선택합니다.

9. **앱 선택**을 선택한 다음, **Microsoft Forms**를 선택하고 **선택**을 선택합니다. 

10. **액세스 제어**에서 **세션** 및 **컨트롤 0개 선택**을 선택합니다.

11. **조건부 액세스 앱 제어 사용** 상자를 선택하고 기본값인 **모니터만**을 그대로 두고 **선택**을 ​​선택합니다.

12. **정책 사용**에서 **사용**을 선택하고 **만들기**를 선택합니다.

#### 작업 3 - Forms에 로그인하고 조건부 액세스가 모니터링되고 있는지 확인

1. 새 **InPrivate 탐색**창을 시작합니다.
2. [https://forms.microsoft.com](https://forms.microsoft.com)에 연결합니다.
3. 페이지의 오른쪽 위에서 로그인을 클릭합니다.
4. Pradeep Gupta로 로그인합니다.
   - 사용자 이름 = PradeepG@<<<your lab hoster provided domain>>>
   - 암호 = 리소스 탭의 암호
5. Pradeep에 액세스 권한이 있고 새 메시지가 표시되는지 확인합니다.
   - 회사에서 이 애플리케이션의 사용을 모니터링하고 있습니다.
6. InPrivate 검색 창을 닫습니다.

### 연습 2 - Microsoft Defender for Cloud Apps에서 경고 설정

#### 작업 1 - Microsoft Defender for Cloud Apps에 액세스하고 조건부 액세스 앱 제어 만들기

애플리케이션을 등록하면 앱과 Microsoft ID 플랫폼 간에 신뢰 관계가 설정됩니다. 트러스트는 단방향입니다. 앱이 Microsoft ID 플랫폼을 신뢰하지만 Microsoft ID 플랫폼이 앱을 신뢰하는 것은 아닙니다.

1. 전역 관리자 계정을 사용하여 [https://security.microsoft.com](https://security.microsoft.com)에 로그인합니다.

1. 왼쪽 메뉴에서 아래쪽으로 스크롤하여 **추가 리소스**를 선택합니다.

1. **추가 리소스** 창에서 **클라우드용 Microsoft Defender Apps** 아래에서 **열기**를 찾아 선택합니다.  그러면 Microsoft 365 계정 내의 **클라우드용 Microsoft Defender Apps** 포털로 이동합니다.

1. **클라우드용 Microsoft Defender Apps** 포털 메뉴에서 **제어**의 드롭다운 화살표를 선택하고 **정책**을 선택합니다.

1. **+ 정책 만들기**를 선택합니다. **액세스 정책**을 선택합니다.

1. 정책 이름(예: **Monitor Microsoft Forms 액세스**)을 입력합니다.

1. **카테고리**를 **액세스 제어**로 둡니다.

1. **다음 모두와 일치하는 활동**에서 **Intune 준수, 하이브리드 Azure AD 조인됨** 드롭다운을 선택하고 **하이브리드 Azure AD 조인됨**을 선택 취소합니다.

1. **앱 선택** 드롭다운을 선택합니다.  **Microsoft Forms**를 선택합니다.

1. **작업**을 **테스트**로 둡니다.

1. **경고**에서 **경고 만들기...** 를 선택한 상태로 두고 **메일로 경고 전송**을 선택합니다.

1. 랩 관리자 메일 주소를 입력하고 키보드에서 **Enter** 키를 선택합니다.

1. **만들기**를 선택하여 액세스 정책을 만듭니다.

#### 작업 2 - 작업을 트리거하기 위해 Forms에 Pradeep으로 로그인

1. 새 **InPrivate 탐색**창을 시작합니다.
2. [https://forms.microsoft.com](https://forms.microsoft.com)에 연결합니다.
3. 페이지의 오른쪽 위에서 로그인을 클릭합니다.
4. Pradeep Gupta로 로그인합니다.
   - 사용자 이름 = PradeepG@<<<your lab hoster provided domain>>>
   - 암호 = 리소스 탭의 암호
5. Pradeep에 액세스 권한이 있고 새 메시지가 표시되는지 확인합니다.
   - 회사에서 이 애플리케이션의 사용을 모니터링하고 있습니다.
6. InPrivate 검색 창을 닫습니다.

#### 작업 3 - Defender for Cloud Apps의 활동 검토

1. Defender for Cloud Apps를 실행하는 브라우저로 돌아갑니다.
2. 브라우저를 새로 고침하여 최신 데이터가 다운로드되도록 합니다.
3. **조사** 메뉴에서 **활동 로그**를 선택합니다.
4. **앱: 필터**를 사용하여 목록에서 **Microsoft Forms**를 선택합니다.
5. Pradeep에 대한 로그온 레코드를 확인합니다.
