---
lab:
  title: 17 - 클라우드용 Defender Apps 애플리케이션 검색 및 제한 적용
  learning path: "03"
  module: Module 03 - Implement Access Management for Apps
ms.openlocfilehash: 2810d72197e31241d7a3c30d85b40cc5682be0bf
ms.sourcegitcommit: fa8ae52be1e809ca81d07036fefeebffb54c1861
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/08/2022
ms.locfileid: "147521462"
---
# <a name="lab-17---defender-for-cloud-apps-application-discovery-and-enforcing-restrictions"></a>랩 17 - 클라우드용 Defender Apps 애플리케이션 검색 및 제한 적용

## <a name="lab-scenario"></a>랩 시나리오

클라우드용 Microsoft Defender Apps는 네트워크 트래픽의 로그를 활용하여 사용자가 액세스하는 애플리케이션을 식별합니다.  온-프레미스 방화벽의 트래픽 로그는 가장 일반적인 애플리케이션 및 이러한 앱에 액세스하는 사용자에 대한 스냅샷 보고서를 제공합니다.  관리 디바이스의 트래픽이 클라우드용 Microsoft Defender Apps 검색 개요 대시보드로 공급됩니다.

#### <a name="estimated-time-10-minutes"></a>예상 소요 시간: 10분

### <a name="exercise-1---defender-for-cloud-apps-discovery"></a>연습 1 - 클라우드용 Defender Apps 검색

#### <a name="task-1---discovery-apps-in-defender-for-cloud-apps"></a>작업 1 - 클라우드용 Defender Apps에서 앱 검색

1. 전역 관리자 계정을 사용하여 [https://security.microsoft.com](https://security.microsoft.com)에 로그인합니다.

1. 왼쪽 메뉴에서 아래쪽으로 스크롤하여 **추가 리소스** 를 선택합니다.

1. **추가 리소스** 창에서 **클라우드용 Microsoft Defender Apps** 아래에서 **열기** 를 찾아 선택합니다.  그러면 Microsoft 365 계정 내의 **클라우드용 Microsoft Defender Apps** 포털로 이동합니다.

1. 왼쪽 메뉴에서 **검색** 드롭다운을 선택하고 **클라우드 앱 카탈로그** 을 선택합니다.

1. **범주별로 찾아보기** 에서 **클라우드 스토리지** 를 선택합니다.

1. 앱 목록에서 앱 이름 옆에 있는 **위험 점수** 를 확인합니다.  

1. 다른 브라우저 탭을 열고 **Dropbox.com** 으로 이동합니다.

1. 이 웹 사이트에 액세스할 수 있습니다.


#### <a name="task-2---restrict-apps-in-defender-for-cloud-apps"></a>작업 2 - 클라우드용 Defender Apps에서 앱 제한

1. **검색된 앱** 타일로 돌아가서 Dropbox에 대해 **비사용 권한으로 태그 지정** 을 선택합니다.  **참고**: 원을 그리는 확인 표시 옆에 있습니다.

1. 이 프로세스를 통해 회사 정책 내에서 승인되지 않은 애플리케이션을 차단하여 조직 내에서 섀도 IT를 제한할 수 있습니다.

**참고**: 애플리케이션의 승인을 취소하고 해당 애플리케이션이 차단되는 사이에는 지연이 있습니다.

1. 애플리케이션이 허가되지 않은 것으로 차단되면 브라우저, 프라이빗 브라우저 또는 스토어 다운로드를 통해 애플리케이션에 액세스할 수 없습니다.



