---
lab:
  title: 25 - 내부 및 외부 사용자에 대한 액세스 검토 만들기
  learning path: "04"
  module: Module 04 - Plan and Implement and Identity Governance Strategy
ms.openlocfilehash: c5207f3a8886c28390b38d3e1387168ca1d65021
ms.sourcegitcommit: b5fc07c53b5663eaa1883cf38b70c57cd88470ca
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2022
ms.locfileid: "146741714"
---
# <a name="lab-25---creating-access-reviews-for-internal-and-external-users"></a>랩 25 - 내부 및 외부 사용자에 대한 액세스 검토 만들기  

## <a name="lab-scenario"></a>랩 시나리오

권한 있는 사용자 액세스는 비슷한 방식으로 정기적으로 검토되어야 합니다.  이러한 할당은 상승된 액세스 할당이므로 회사에서 식별한 대로 일관되게 검토해야 합니다.  사용하지 않고 불필요한 권한 할당을 제거해야 합니다.  더 이상 회사에 속하지 않거나 회사 내 부서를 변경한 사용자에 대해서도 자동 제거를 구성해야 합니다.

#### <a name="estimated-time-5-minutes"></a>예상 소요 시간: 5분

### <a name="exercise-1---create-an-internal-access-review"></a>연습 1 - 내부 액세스 검토 만들기

#### <a name="task---create-a-new-access-review"></a>작업 - 새 액세스 검토 만들기

1. 전역 관리자로 [https://portal.azure.com](https://portal.azure.com)에 로그인합니다.

2. 액세스 검토는 액세스 수명 주기를 관리할 수 있습니다.  **Azure Active Directory** 내에서 **관리** 메뉴에서 **ID 거버넌스** 를 찾습니다.  **ID 거버넌스** 에서 **액세스 검토** 를 선택합니다.

3. 액세스 검토 이름을 지정하고 시작 날짜 및 빈도를 설정합니다. 기간은 액세스 검토가 만료되기 전에 실행되는 기간입니다.  끝을 특정 날짜로 설정하거나 여러 번 발생한 후에 설정할 수 있습니다.  그런 다음, 액세스 검토의 사용자 범위를 선택합니다.

4. 이 범위의 일부가 될 역할의 범위를 선택합니다.  모든 역할을 추가하거나 특정 검토에 대해 특정 역할만 선택할 수 있습니다. 

5. 다음 단계는 검토자를 결정하는 것입니다.  이러한 검토자는 자체 검토를 수행하는 구성원이거나 전체 부서에 대한 액세스를 검토하는 경우 감독자에게 할당될 수 있습니다. 검토자가 구성원에서 해당 권한 있는 액세스를 자동으로 제거하도록 응답하지 않는 경우 작업을 설정할 수도 있습니다.

6. 고급 설정을 사용하면 검토의 일부로 메시지를 넣을 수 있습니다.  시작을 선택하여 액세스 검토를 시작합니다.

7. 액세스 검토를 만들면 액세스 검토 목록이 검토의 역할 및 소유자로 채워집니다.

8. 검토 중인 구성원은 검토가 시작될 때 메일을 받게 됩니다.

9. 역할 중 하나에 대한 액세스 검토를 선택하면 이러한 액세스 검토에 대한 상태가 표시됩니다.

