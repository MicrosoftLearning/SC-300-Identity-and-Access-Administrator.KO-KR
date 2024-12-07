---
lab:
  title: 11 - Privileged Identity Management에서 Azure 리소스 역할 할당
  learning path: '02'
  module: Module 02 - Implement an authentication and access management solution
---

# 랩 11 - Privileged Identity Management에서 Azure 리소스 역할 할당

### 로그인 유형 = Azure 리소스 로그인

**참고** - 이 랩에는 Azure Pass가 필요합니다. 지침은 랩 00을 참조하세요.

## 랩 시나리오

Microsoft Entra PIM(Privileged Identity Management)은 사용자 지정 역할뿐만 아니라 기본 제공 Azure 리소스 역할을 관리할 수 있습니다. 여기에는 다음이 포함되지만 이에 국한되지 않습니다.

- 담당자
- 사용자 액세스 관리자
- 참가자
- 보안 관리자
- 보안 관리자

사용자를 Azure 리소스 역할에 대해 적격 사용자로 지정해야 합니다.

#### 예상 소요 시간: 10분

### 연습 1 - Azure 리소스를 사용한 PIM

#### 작업 1 - Azure 리소스 역할 할당

1. 전역 관리자 계정을 사용하여 [https://entra.microsoft.com](https://entra.microsoft.com)에 로그인합니다.

2. **Privileged Identity Management**를 검색한 후 선택합니다.

3. 왼쪽 탐색 영역의 Privileged Identity Management 페이지에서 **Azure 리소스**를 선택합니다.

4. 구독 드롭다운에서 MOC 구독##### 항목을 선택합니다. 그런 다음 화면 에서 **리소스 관리**를 선택합니다.

5. Azure 리소스의 검색 페이지에서 구독을 선택합니다.

6. **개요** 페이지에서 정보를 검토합니다.

   ![최근에 추가된 Azure 리소스를 표시하는 화면 이미지](./media/lp4-mod3-pim-az-resource-overview.png)

7. 왼쪽 탐색 메뉴의 **관리**에서 **역할**을 선택하여 Azure 리소스에 대한 역할 목록을 표시합니다.

8. 상단 메뉴에서 + **할당 추가**를 선택합니다.

9. 할당 추가 페이지에서, **역할 선택** 메뉴를 선택한 다음, **API Management 서비스 기여자**를 선택합니다.

10. **구성원 선택**에서 **선택된 구성원 없음**을 선택합니다.

11. 구성원 또는 그룹 선택에서 역할이 할당될 조직의 관리자 역할 **User1-######@LODSPRODMCA.onmicrosoft.com**을(를) 검색합니다.  그런 후에 **선택**을 선택합니다.

12. **다음**을 선택합니다.

13. **설정** 탭의 **할당 유형**에서 **적격**을 선택합니다.

   - **적격** 할당에는 역할을 사용하는 작업을 수행하기 위해 역할의 구성원이 필요합니다. 작업은 MFA(Multi-Factor Authentication) 검사를 수행하고, 비즈니스 근거를 제공하거나 지정된 승인자의 승인을 요청하는 과정을 포함할 수 있습니다.

   - **활성화** 할당은 역할을 사용하는 작업을 수행하기 위해 구성원을 필요로 하지 않습니다. 활성으로 할당된 구성원에게는 역할에 할당된 권한이 있습니다.

14. 시작 및 종료 날짜와 시간을 변경하여 할당 기간을 지정합니다.

15. 작업을 마쳤으면 **할당하기**를 선택합니다.

16. 새 역할 할당이 만들어지면 상태 알림이 표시됩니다.

#### 작업 2 - 기존 리소스 역할 할당 업데이트 또는 제거

기존 역할 할당을 업데이트하거나 제거하려면 다음 단계를 수행합니다.

1. **Microsoft Entra Privileged Identity Management**를 엽니다.

2. **Azure 리소스**를 선택합니다.

3. 관리하려는 구독을 선택하여 개요 페이지를 엽니다.

4. **관리**에서 **할당**을 선택합니다.

5. 작업 열의 **적격 할당** 탭에서 사용 가능한 옵션을 검토합니다.

6. **제거**를 선택합니다.

7. **제거** 대화 상자에서 정보를 검토한 다음 **예**를 선택합니다.
