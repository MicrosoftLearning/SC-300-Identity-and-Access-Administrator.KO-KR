---
lab:
  title: 16 - 인증 세션 컨트롤 구성
  learning path: "02"
  module: Module 02 - Implement an Authentication and Access Management Solution
ms.openlocfilehash: 8fadbe8fc6c26f79f2f75efae07e90cae714088b
ms.sourcegitcommit: 448f935ad266989a6f0086019e0c0e0785ad162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/10/2022
ms.locfileid: "138421362"
---
# <a name="lab-16---configure-authentication-session-controls"></a>랩 16 - 인증 세션 컨트롤 구성

## <a name="lab-scenario"></a>랩 시나리오

회사 보안 구성의 일환으로, 로그인 빈도를 제어하는 데 사용할 수 있는 조건부 액세스 정책을 테스트해야 합니다.

#### <a name="estimated-time-10-minutes"></a>예상 소요 시간: 10분

### <a name="exercise-1---configure-sign-in-frequency-controls-using-a-conditional-access-policy"></a>연습 1 - 조건부 액세스 정책을 사용하여 로그인 빈도 제어 구성

#### <a name="task---user-the-azure-portal-to-configure-conditional-access"></a>작업 - 조건부 액세스를 구성하는 Azure Portal 사용자

1. [https://portal.azure.com](https://portal.azure.com)으로 이동한 후 해당 디렉터리에 대한 전역 관리자 계정을 사용하여 로그인합니다.

2. 포털 메뉴를 열고 **Azure Active Directory** 를 선택합니다.

3. Azure Active Directory 블레이드의 **관리** 에서 **보안** 을 선택합니다.

4. 보안 블레이드의 왼쪽 탐색 영역에서 **조건부 액세스** 를 선택합니다.

5. 상단 메뉴의 드롭다운에서 **+ 새 정책** 을 선택하고 **새 정책 만들기** 를 선택합니다.

    ![새 정책이 강조 표시된 조건부 액세스 블레이드를 표시하는 화면 이미지](./media/lp2-mod1-conditional-access-new-policy.png)

6. **이름** 상자에 **로그인 빈도** 를 입력합니다.

7. **할당** 아래에서 **사용자 또는 워크로드 ID** 를 선택합니다.

8. 포함 탭에서 **사용자 및 그룹** 확인란을 선택합니다.

9. 선택 창에서 **Grady Archie** 계정을 선택한 다음 **선택** 을 선택합니다.

10. **클라우드 앱 또는 작업** 을 선택합니다.

11. **클라우드 앱** 이 선택되어 있는지 확인하고 **앱 선택** 을 선택합니다.

12. 선택 창에서 **Office 365** 를 선택하고 **선택** 을 선택합니다.

13. **액세스 제어** 에서 **세션** 을 선택합니다.

14. 세션 창에서 **로그인 빈도** 를 선택합니다.

15. 값 상자에 **30** 을 입력합니다.

16. 단위 메뉴를 선택하고 **일** 을 선택한 다음 **선택** 을 선택합니다.

17. **정책 사용** 에서 **보고 전용** 을 선택한 다음, **생성** 를 선택합니다.

    ![정책 설정이 강조 표시된 새 조건부 액세스 정책을 표시하는 화면 이미지](./media/lp2-mod3-create-session-conditional-access-policy.png)

   **참고** - 보고 전용 모드는 관리자가 정책을 환경에 사용하도록 설정하기 전에 조건부 액세스 정책의 영향을 평가할 수 있도록 하는 새 조건부 액세스 정책 상태입니다. 보고 전용 모드의 릴리스 사용
    
    - 조건부 액세스 정책은 보고 전용 모드에서 사용하도록 설정할 수 있습니다.
    - 로그인하는 동안 보고 전용 모드의 정책은 평가되지만 적용되지 않습니다.
    - 결과는 로그인 로그 세부 정보에 대한 조건부 액세스 및 보고 전용 탭에 기록됩니다.
    - Azure Monitor 구독이 있는 고객은 조건부 액세스 인사이트 통합 문서를 사용하여 조건부 액세스 정책의 영향을 모니터링할 수 있습니다.
