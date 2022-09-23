---
lab:
  title: 28 - ID 보안 점수를 사용하여 보안 상태 모니터링 및 관리
  learning path: "04"
  module: Module 04 - Plan and Implement and Identity Governance Strategy
ms.openlocfilehash: 14a8a2a123429f44b84ea45284f34a04bac6aa81
ms.sourcegitcommit: b5fc07c53b5663eaa1883cf38b70c57cd88470ca
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2022
ms.locfileid: "146741712"
---
# <a name="lab-28---monitor-and-managed-security-posture-with-identity-secure-score"></a>랩 28 - ID 보안 점수를 사용하여 보안 상태 모니터링 및 관리

## <a name="lab-scenario"></a>랩 시나리오

Azure AD ID 보호는 ID 기반 위험에 대한 자동화된 검색 및 수정을 제공하고, 포털에서 잠재적인 위험을 조사하는 데이터를 제공합니다. Azure AD ID 보호는 ID 보안 상태를 모니터링하고 개선하기 위한 ID 보안 점수도 제공합니다.  Microsoft 365 Defender 및 클라우드용 Microsoft Defender와 동일한 방식으로 ID 보안 점수는 Azure Active Directory에서 ID에 대한 전반적인 보안 태세를 개선할 수 있는 개선 작업 및 권장 사항을 제공합니다.  이 랩에서는 이 기능을 탐색합니다. 

#### <a name="estimated-time-15-minutes"></a>예상 소요 시간: 15분

### <a name="exercise-1---using-identity-secure-score-to-monitor-and-manage-identity-security-posture"></a>연습 1 - ID 보안 점수를 사용하여 ID 보안 상태 모니터링 및 관리

#### <a name="task-1---review-identity-secure-score-and-improvement-actions"></a>작업 1 - ID 보안 점수 및 개선 작업 검토

1. 전역 관리자로 [https://portal.azure.com](https://portal.azure.com)에 로그인합니다.

1. **Azure AD Identity Protection** 을 검색한 다음, 선택합니다.

1. **개요** 타일에서 **ID 보안 점수** 를 찾을 수 있습니다.

1. **ID 보안 점수** 를 선택합니다.  이렇게 하면 ID 보안 점수 대시보드로 연결됩니다.

1. 아래로 스크롤하여 **개선 작업** 을 봅니다.

1. 클라우드용 Microsoft Defender 및 Microsoft 365 Defender의 개선 작업과 달리 이러한 개선 작업은 ID에 따라 다릅니다.  이렇게 하면 보안 상태 관리에 더 집중된 잠재적인 작업 목록이 제공됩니다.  이 목록에서 시작된 개선 작업은 전체 테넌트 보안 태세에도 영향을 줍니다. 

#### <a name="task-2---execute-an-improvement-action"></a>작업 2 - 개선 작업 실행

1. ID 보안 상태의 한 영역을 개선하려면 **로그인 위험 정책 켜기** 를 선택합니다.

1. 열리는 타일에서 아래로 스크롤하고 **시작** 을 선택합니다.

1. **ID 보호 | 로그인 위험 정책** 에 대한 새 탭이 열립니다.

1. **할당** 에서 **모든 사용자** 를 선택합니다.

1. **로그인 위험** 에서 **중간 이상** 을 선택합니다.

1. **제어** 에서 **허용** - **다단계 인증 필요** 를 선택합니다.

1. **정책 시행** 을 **켜기** 로 설정하고 **저장** 을 선택합니다.

1. 이제 ID 보안 점수를 늘려야 하는 로그인 위험 정책을 만들었습니다.  ID 보안 점수에 영향을 미치는 데 최대 24시간이 걸립니다.

1. 다른 개선 작업 및 이를 만들고 사용하도록 설정하는 단계를 검토합니다.


