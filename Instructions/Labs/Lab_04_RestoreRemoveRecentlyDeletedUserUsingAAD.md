---
lab:
  title: 04 - 삭제된 사용자 복원
  learning path: "01"
  module: Module 01 - Implement an identity management solution
ms.openlocfilehash: 9ec368f11cce9ad63fbc297149a68582e1773358
ms.sourcegitcommit: 448f935ad266989a6f0086019e0c0e0785ad162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/10/2022
ms.locfileid: "138421313"
---
# <a name="lab-04-restore-a-deleted-user"></a>랩 04: 삭제한 사용자 복원

## <a name="lab-scenario"></a>랩 시나리오

계정이 삭제되어 복구가 필요한 경우가 발생할 수도 있습니다. 최근에 삭제된 계정을 복구할 수 있는지 확인해야 합니다.

#### <a name="estimated-time-5-minutes"></a>예상 소요 시간: 5분

### <a name="exercise-1---remove-a-user-from-azure-active-directory"></a>연습 1 - Azure Active Directory에서 사용자 제거

#### <a name="task-1---remove-a-user"></a>작업 1 - 사용자 제거

1. [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview]( https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) 으로 이동합니다.

2. 왼쪽 탐색 영역의 **관리** 에서 **사용자** 를 선택합니다.

3. **사용자** 목록에서 삭제할 사용자의 확인란을 선택합니다. 예를 들어 **Chris Green** 을 선택합니다.

    **팁** - 목록에서 사용자를 선택하면 여러 사용자를 동시에 관리할 수 있습니다. 사용자를 선택하는 경우 해당 사용자의 블레이드를 열려면 개별 사용자만 관리하면 됩니다.

    ![사용자 한 명의 확인란이 선택되어 있고 다른 확인란은 강조 표시되어 목록에서 여러 사용자를 선택할 수 있음을 보여 주는 모든 사용자 목록 화면 이미지.](./media/lp1-mod2-remove-user.png)

4. 사용자 계정이 선택된 상태의 메뉴에서 **사용자 삭제** 를 선택합니다.

5. 대화 상자를 검토한 다음 **확인** 을 선택합니다.

#### <a name="task-2---restore-a-deleted-user"></a>작업 2 - 삭제된 사용자 복원

1. 사용자 블레이드의 왼쪽 탐색 영역에서 **삭제된 사용자** 를 선택합니다.

2. 삭제된 사용자 목록을 검토하고 방금 삭제한 사용자를 선택합니다.

    **중요** - 기본적으로 삭제된 사용자 계정은 30일 후 자동으로 Azure Active Directory에서 영구히 제거됩니다.

3. 메뉴에서 **사용자 복원** 을 선택합니다.

4. 대화 상자를 검토한 다음 **확인** 을 선택합니다.

5. 왼쪽 탐색 영역에서 **모든 사용자** 를 선택합니다.

6. 사용자가 복원되었는지 확인합니다.
