---
lab:
  title: 24 - 앱에 앱 역할 추가 및 토큰으로 수신
  learning path: "03"
  module: Module 03 - Implement Access Management for Apps
ms.openlocfilehash: e796d84e5ece63e16de898aca18f36b37b88a515
ms.sourcegitcommit: 448f935ad266989a6f0086019e0c0e0785ad162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/10/2022
ms.locfileid: "138421314"
---
# <a name="lab-24-add-app-roles-to-your-app-and-receive-them-in-the-token"></a>랩 24: 앱에 앱 역할 추가 및 토큰으로 수신

## <a name="lab-scenario"></a>랩 시나리오

RBAC(역할 기반 액세스 제어)는 애플리케이션에서 권한 부여를 적용하는 데 널리 사용되는 메커니즘입니다. RBAC를 사용하는 경우, 관리자는 개별 사용자나 그룹이 아닌 역할에 사용 권한을 부여합니다. 그런 다음 관리자는 다른 사용자 및 그룹에 역할을 할당하여 누가 어떤 컨텐츠와 기능에 액세스 권한을 갖는지를 제어할 수 있습니다. RBAC 역할을 구현할 계획이며 이 절차를 수행하는 방법을 이해하고 있는지 확인해야 합니다.

#### <a name="estimated-time-10-minutes"></a>예상 소요 시간: 10분

### <a name="exercise-1---adding-roles-to-your-apps"></a>연습 1 - 앱에 역할 추가

#### <a name="task-1---declare-app-roles-using-the-app-roles-ui"></a>작업 1 - 앱 역할 UI를 사용하여 앱 역할 선언

   **중요** - 앱 역할 포털 UI 기능은 퍼블릭 미리 보기로 제공됩니다. 퍼블릭 미리 보기는 서비스 수준 계약 없이 제공되며 프로덕션 워크로드에는 사용하지 않는 것이 좋습니다. 특정 기능이 지원되지 않거나 기능이 제한될 수 있습니다.

Azure Portal의 사용자 인터페이스를 사용하여 앱 역할을 만들려면 다음을 수행합니다.

1. 전역 관리자 계정을 사용하여 [https://portal.azure.com](https://portal.azure.com)에 로그인합니다.

2. 포털 메뉴를 열고 **Azure Active Directory** 를 선택합니다.

3. **Azure Active Directory** 블레이드의 **관리** 에서 **앱 등록** 을 선택합니다.

4. 앞에서 만든 **데모 앱** 앱 등록 항목을 선택합니다.

5. **앱 역할** 을 선택한 다음, **+앱 역할 만들기** 를 선택합니다.

    ![앱 역할 생성가 강조 표시된 앱 역할을 보여 주는 화면 이미지](./media/lp3-mod3-app-roles-create-app-role.png)

6. **앱 역할 생성** 창의 **표시 이름** 상자에 **설문 조사 작성자** 를 입력합니다.

7. **Allow member types**(구성원 유형 허용)에서 **사용자/그룹** 을 선택합니다.

8. **값** 상자에 **Survey.Create** 를 입력합니다.

9. **설명** 상자에 **작성자가 설문 조사를 만들 수 있음** 이라고 입력합니다.

10. 설명은 필수 필드입니다.

11. **이 앱 역할을 사용하도록 설정하시겠습니까?** 가 선택되어 있는지 확인한 다음 **적용** 을 선택합니다.

#### <a name="task-2---assign-users-and-groups-to-roles"></a>작업 2 - 역할에 사용자 및 그룹 할당

애플리케이션에서 앱 역할을 추가하고 나면 이 역할에 사용자 및 그룹을 할당할 수 있습니다. 역할에 사용자 및 그룹을 할당하는 작업은 포털의 UI를 통해 수행하거나 [https://docs.microsoft.com/graph/api/user-post-approleassignments](https://docs.microsoft.com/graph/api/user-post-approleassignments)를 사용하여 프로그래밍 방식으로 수행할 수 있습니다. 다양한 앱 역할에 할당된 사용자가 애플리케이션에 로그인하면 해당 토큰은 역할 클레임에 할당된 역할을 갖게 됩니다.

Azure Portal을 사용하여 사용자 및 그룹을 역할에 할당하려면 다음을 수행합니다.

1. [https://portal.azure.com](https://portal.azure.com)에 로그인합니다.

2. IAzure Active Directory 왼쪽에 있는 탐색 메뉴에서 **엔터프라이즈 애플리케이션** 을 선택합니다.

3. **모든 애플리케이션** 목록에서 **Demo app** 을 선택합니다.

4. 이 앱은 이전 연습에서 만들었습니다.

5. **관리** 에서 **사용자 및 그룹** 을 선택합니다.

6. 메뉴에서 **+ 사용자/그룹 추가** 를 선택합니다.

7. **할당 추가** 블레이드의 사용자 및 그룹 아래에서 **선택된 항목 없음** 을 선택합니다.

8. 사용자와 보안 그룹 목록이 표시됩니다. **Grady** 를 검색하여 Grady Archie를 추가할 수 있습니다.

9. 사용자와 그룹을 선택한 후 **선택** 을 선택합니다.

10. **역할 할당 선택** 에서 **설문 조사 작성자** 를 선택해야 합니다.

    **참고** - 현재 역할이 설문 조사 작성자뿐이므로 이 옵션은 회색으로 표시됩니다.

11. **할당** 을 선택하여 앱에 사용자와 그룹 할당을 마칩니다.

12. 추가한 사용자와 그룹이 **사용자 및 그룹** 목록에 보이는지 확인합니다.
