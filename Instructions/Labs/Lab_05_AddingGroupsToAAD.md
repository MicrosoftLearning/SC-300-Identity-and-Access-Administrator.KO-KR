---
lab:
  title: 05 - Azure AD에 그룹 추가
  learning path: "01"
  module: Module 01 - Implement an identity management solution
ms.openlocfilehash: 192cb3bc35b573ed3b4799cfb3872038874cb521
ms.sourcegitcommit: 448f935ad266989a6f0086019e0c0e0785ad162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/10/2022
ms.locfileid: "138421446"
---
# <a name="lab-05-adding-groups-to-azure-ad"></a>랩 05: Azure AD에 그룹 추가

## <a name="lab-scenario"></a>랩 시나리오

Azure AD 관리자의 업무 중 하나는 다양한 유형의 그룹을 만드는 것입니다. 조직의 영업부를 위해 새로운 Microsoft 365 그룹을 만들어야 합니다.

#### <a name="estimated-time-5-minutes"></a>예상 소요 시간: 5분

### <a name="exercise-1---create-an-microsoft-365-group-in-azure-active-directory"></a>연습 1 - Azure Active Directory에서 Microsoft 365 그룹 만들기

#### <a name="task-1---create-the-group"></a>작업 1 - 그룹 만들기

1. [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview]( https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) 으로 이동합니다.

2. 왼쪽 탐색 영역의 **관리** 에서 **그룹** 을 선택합니다.

3. 그룹 블레이드의 메뉴에서 **새 그룹** 을 선택합니다.

4. 다음 정보를 사용하여 그룹을 생성합니다.

    | **설정**| **값**|
    | :--- | :--- |
    | 그룹 형식| Microsoft 365|
    | 그룹 이름| 북서부 판매액|
    | 멤버 자격 유형| 할당됨|
    | 소유자| *자신의 관리자 계정을 그룹 소유자로 할당*|
    | 멤버| **Alex Wilber** 및 **Bianca Pisani**|

    ![그룹 유형, 그룹 이름, 소유자 및 구성원이 강조 표시된 새 그룹 블레이드를 보여주는 화면 이미지](./media/lp1-mod2-create-o365-group.png)

5. 완료되면 이름이 **Northwest sales** 라는 그룹이 **모든 그룹** 목록에 표시되는지 확인합니다.
