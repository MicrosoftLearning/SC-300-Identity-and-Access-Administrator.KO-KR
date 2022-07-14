---
lab:
  title: 24 - Azure AD Identity Governance 설정에서 외부 사용자의 수명 주기 관리
  learning path: "04"
  module: Module 04 - Plan and Implement and Identity Governance Strategy
ms.openlocfilehash: a159b0548b2755c34ad9e4412e8f70ea14be1d5f
ms.sourcegitcommit: b5fc07c53b5663eaa1883cf38b70c57cd88470ca
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2022
ms.locfileid: "146741716"
---
# <a name="lab-24-manage-the-lifecycle-of-external-users-in-azure-ad-identity-governance-settings"></a>랩 24: Azure AD Identity Governance 설정에서 외부 사용자의 수명 주기 관리  

## <a name="lab-scenario"></a>랩 시나리오

승인된 액세스 패키지 요청을 통해 디렉터리에 초대된 외부 사용자가 더 이상 액세스 패키지 할당을 보유하지 않는 경우 수행할 작업을 선택할 수 있습니다. 사용자가 모든 액세스 패키지 할당을 포기하거나 마지막 액세스 패키지 할당이 만료되는 경우 이 상황이 발생할 수 있습니다. 외부 사용자에게 더 이상 액세스 패키지 할당이 없는 경우 기본값으로 디렉터리에 로그인하지 못하도록 차단됩니다. 30일 후에는 해당 게스트 사용자 계정이 디렉터리에서 제거됩니다.

#### <a name="estimated-time-5-minutes"></a>예상 소요 시간: 5분

### <a name="exercise-1---azure-ad-identity-governance-settings"></a>연습 1 - Azure AD Identity Governance 설정

#### <a name="task-1---manage-the-lifecycle-of-external-users-in-azure-ad-identity-governance-settings"></a>작업 1 - Azure AD Identity Governance 설정에서 외부 사용자의 수명 주기 관리

1. 전역 관리자로 [https://portal.azure.com](https://portal.azure.com)에 로그인합니다.

2. 해당 작업을 완료하려면 전역 관리자 또는 사용자 관리자 권한이 있는 계정이 필요합니다.

3. Azure Active Directory를 열고 **ID 거버넌스** 를 선택합니다.

4. 왼쪽 탐색 메뉴의 **권한 관리** 에서 **설정** 을 선택합니다.

5. 상단 메뉴에서 **편집** 을 선택합니다.

    ![외부 사용자의 수명 주기 관리가 강조 표시된 ID 거버넌스 설정 페이지를 표시하는 화면 이미지](./media/lp4-mod1-manage-lifcycle-of-ext-users.png)

6. **외부 사용자의 수명 주기 관리** 섹션에서 외부 사용자에 대한 다양한 설정을 검토합니다.

7. 외부 사용자가 액세스 패키지에 대한 마지막 할당을 상실한 경우 이 디렉터리에 로그인하지 못하도록 차단하려면 **외부 사용자가 이 디렉터리에 로그인하지 못하도록 차단** 을 **예** 로 설정합니다.

8. 사용자가 디렉터리에 로그인하지 못하도록 차단되면 사용자는 액세스 패키지를 다시 요청하거나 해당 디렉터리에서 추가 액세스를 요청할 수 없습니다. 나중에 사용자가 다른 액세스 패키지에 대한 액세스 권한을 요청해야 하는 경우에는 사용자의 로그인을 차단하도록 구성하지 마세요.

9. 외부 사용자가 액세스 패키지에 대한 마지막 할당을 상실한 후 이 디렉터리에서 게스트 사용자 계정을 제거하려면 **외부 사용자 제거** 를 **예** 로 설정합니다.

    **참고** - 권한 관리는 권한 관리를 통해 초대된 계정만 제거합니다. 또한 액세스 패키지 할당이 아닌 디렉터리의 리소스에 사용자가 추가된 경우에도 사용자는 로그인하지 못하도록 차단되며 디렉터리에서 제거됩니다. 게스트는 액세스 패키지 할당을 받기 전에 이 디렉터리에 있는 경우 유지됩니다. 그러나 게스트가 액세스 패키지 할당을 통해 초대되고 초대된 후에 비즈니스용 OneDrive 또는 SharePoint Online 사이트에 할당된 경우에도 제거됩니다.

10. 해당 디렉터리에서 게스트 사용자 계정을 제거하려면 제거 전 일 수를 설정할 수 있습니다. 액세스 패키지에 대한 마지막 할당을 잃는 즉시 게스트 사용자 계정을 제거하려면 **해당 디렉터리에서 외부 사용자를 제거하기 전까지 남은 일 수** 를 **0** 으로 설정합니다.

11. 변경한 경우 **저장** 을 선택합니다.