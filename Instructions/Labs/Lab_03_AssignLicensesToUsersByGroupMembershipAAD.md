---
lab:
  title: 03 - 그룹 구성원 자격을 사용하여 라이선스 할당
  learning path: "01"
  module: Module 01 - Implement an identity management solution
ms.openlocfilehash: 9ecd9c244867c5c995a5e6dc39bbdc47f48ad5c7
ms.sourcegitcommit: fbe0a16b7c6a9a2ac2c2ea3b3f707faa0afe23a2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2022
ms.locfileid: "139258492"
---
# <a name="lab-03-assigning-licenses-using-group-membership"></a>랩 03: 그룹 구성원 자격을 사용하여 라이선스 할당

## <a name="lab-scenario"></a>랩 시나리오

조직에서 Azure AD의 보안 그룹을 사용하여 라이선스를 관리하기로 결정했습니다. 새로운 보안 그룹을 구성하고, 해당 그룹에 라이선스를 할당하고, 그룹 구성원 라이선스가 업데이트되었는지 확인해야 합니다.

#### <a name="estimated-time-10-minutes"></a>예상 소요 시간: 10분

### <a name="exercise-1---create-a-security-group-and-add-a-user"></a>연습 1 - 보안 그룹 만들기 및 사용자 추가

#### <a name="task-1---check-to-see-if-delia-dennis-has-access-to-office-365"></a>작업 1 - Delia Dennis에게 Office 365 액세스 권한이 있는지 확인

1. 새 InPrivate 브라우저 창을 시작합니다.
2. [https://www.office.com](https://www.office.com)에 연결합니다.
3. 로그인을 클릭하고 Delia Dennis로 연결합니다.

    | **설정**| **값**|
    | :--- | :--- |
    | 사용자 이름 | DeliaD@`your domain name.com`|
    | 암호| 리소스의 전역 관리자 암호 입력|

4. Office.com 웹 사이트에 연결은 되지만 라이선스가 없다는 메시지가 표시됩니다.

    ![Delia Dennis로 로그인한 Office.com 웹 사이트의 화면 이미지. 라이선스가 할당되어 있지 않아 Office 애플리케이션을 사용할 수 없음.](./media/delia-no-office-license.png)
    
5. 브라우저 창을 닫습니다.

#### <a name="task-2----create-a-security-group-in-azure-active-directory"></a>작업 2 - Azure Active Directory에서 보안 그룹 만들기

1. [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview]( https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) 으로 이동합니다.

2. 왼쪽 탐색 영역의 **관리** 에서 **그룹** 을 선택합니다.
3. 그룹 블레이드의 메뉴에서 **새 그룹** 을 선택합니다.
4. 다음 정보를 사용하여 그룹을 생성합니다.

    | **설정**| **값**|
    | :--- | :--- |
    | 그룹 형식| 보안|
    | 그룹 이름| sg-SC300-O365|
    | 멤버 자격 유형| 할당됨|
    | 소유자| *자신의 관리자 계정을 그룹 소유자로 할당*|

5. 구성원 아래에서 **선택한 멤버가 없음** 텍스트를 클릭합니다.
6. 사용자 목록에서 **Delia Dennis** 를 선택합니다.
7. **선택** 단추를 클릭합니다.

    ![그룹 유형, 그룹 이름, 소유자 및 구성원이 강조 표시된 새 그룹 블레이드를 보여주는 화면 이미지](./media/lp1-mod2-create-group.png)

8. **만들기** 단추를 클릭합니다.
9. 만들기가 완료되면 **sg-SC300-O365** 그룹이 **모든 그룹** 목록에 표시되는지 확인합니다.

#### <a name="task-3---assign-a-license-to-a-group"></a>작업 3 - 그룹에 라이선스 할당

1. **모든 그룹** 목록에서 **sg-SC300-O365** 를 선택합니다.
2. Marketing 블레이드의 **관리** 에서 **라이선스** 를 선택합니다.
3. 메뉴에서 **+ 할당** 을 선택합니다.
4. 라이선스 할당 업데이트 블레이드의 **라이선스 선택** 에서 사용 가능한 라이선스 목록을 검토한 후 **Office 365 E3** 의 체크박스를 선택합니다.

    **팁** - 여러 라이선스를 선택한 경우 라이선스 옵션 검토 메뉴를 사용하여 특정 라이선스를 선택하고 해당 라이선스의 라이선스 옵션을 볼 수 있습니다.

    ![선택되어 그룹에 할당된 라이선스를 보여 주는 화면 이미지. 라이선스 검토 메뉴 역시 선택되어 여러 선택 옵션을 보여줍니다.](./media/lp1-mod2-assign-license-group.png)

6. **저장** 을 선택합니다.

#### <a name="taks-4---confirm-the-office-365-license"></a>작업 4 - Office 365 라이선스 확인

1. 새 InPrivate 브라우저 창을 시작합니다.
2. [https://www.office.com](https://www.office.com)에 연결합니다.
3. 로그인을 클릭하고 Delia Dennis로 연결합니다.

    | **설정**| **값**|
    | :--- | :--- |
    | 사용자 이름 | DeliaD@`your domain name.com`|
    | 암호| 리소스의 전역 관리자 암호 입력|

4. Office.com 웹 사이트에 연결하여 라이선스 관련 메시지가 없는지 확인해야 합니다. 모든 Office 애플리케이션은 왼쪽에서 사용할 수 있습니다.

    ![Delia Dennis로 로그인한 Office.com 웹 사이트의 화면 이미지. 라이선스가 할당되었으므로 Office 애플리케이션을 사용할 수 있음.](./media/delia-office-license.png)
    
5. 브라우저 창을 닫습니다.
    
