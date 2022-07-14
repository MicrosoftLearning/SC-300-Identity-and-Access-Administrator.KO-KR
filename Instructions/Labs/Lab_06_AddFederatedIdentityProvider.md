---
lab:
  title: 06 - 페더레이션 ID 공급자 추가
  learning path: "01"
  module: Module 01 - Implement an identity management solution
ms.openlocfilehash: da25fe1a291e37a641448b8e4587352989993c96
ms.sourcegitcommit: 80c5c0ef60c1d74fcc58c034fe6be67623013cc0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2022
ms.locfileid: "146823198"
---
# <a name="lab-06-add-a-federated-identity-provider"></a>랩 06: 페더레이션 ID 공급자 추가

## <a name="lab-scenario"></a>랩 시나리오

귀사는 여러 공급업체와 협력하고 있으며, 때로는 일부 공급업체 계정을 디렉터리에 게스트로 추가하고 해당 Google 계정을 사용하여 로그인하도록 허용해야 합니다.

#### <a name="estimated-time-25-minutes"></a>예상 소요 시간: 25분

### <a name="exercise-1---configure-identity-providers"></a>연습 1 - ID 공급자 구성

#### <a name="task-1---configure-google-to-be-used-as-an-identity-provider"></a>작업 1 - ID 공급자로 사용할 Google 구성

**참고** - 이 연습에서는 Google에서 Gmail 계정이 필요합니다. 새 Google 계정을 만든 다음, 연습 단계를 수행합니다.

1. https://console.developers.google.com 에서 Google API로 이동하고, Google 계정으로 로그인합니다. 공유 팀 Google 계정을 사용하는 것이 좋습니다.

1. 해당 계정을 사용하라는 메시지가 표시되면 서비스 약관에 동의합니다.

1. 새 프로젝트 만들기: 페이지 위쪽에서 프로젝트 메뉴를 선택하여 프로젝트 선택 페이지를 엽니다. 새 프로젝트를 선택합니다.  나머지 필드는 기본 설정으로 둡니다.

1. 새 프로젝트 페이지에서 프로젝트에 이름(예: **MyB2BApp**)을 지정한 다음, **만들기** 를 선택합니다.

1. 알림 메시지 상자에서 링크를 선택하거나 페이지 맨 위에 있는 프로젝트 메뉴를 사용하여 새 프로젝트를 엽니다.

1. 왼쪽 메뉴에서 **API 및 서비스** 를 선택한 다음, **OAuth 동의 화면** 을 선택합니다.

1. 사용자 유형에서 **외부** 를 선택한 다음, **만들기** 를 선택합니다.

1. **OAuth 동의 화면** 의 앱 정보에서 앱 이름(예: **Azure AD**)을 입력합니다.

1. 사용자 지원 이메일에서 이메일 주소를 선택합니다. 여기에는 Google에 로그인하는 데 사용한 메일 주소가 포함되어야 합니다.

1. 권한 있는 도메인에서 **도메인 추가** 를 선택한 다음, microsoftonline.com 도메인을 추가합니다.

   ```
   microsoftonline.com
   ```

1. 개발자 연락처 정보에서 포털에 로그인하는 데 사용한 랩 계정의 메일 주소를 입력합니다.

1. **저장하고 계속** 을 선택합니다.

1. 왼쪽 메뉴에서 **자격 증명** 을 선택합니다.

1. **+ 자격 증명 만들기** 를 선택한 다음, **OAuth 클라이언트 ID** 를 선택합니다.

1. 애플리케이션 유형 메뉴에서 웹 애플리케이션을 선택합니다. AZURE AD B2B와 같이 애플리케이션에 적합한 이름을 지정합니다. **권한 있는 리디렉션 URI** 에서 다음 URI를 추가합니다.

   ```
       - https://login.microsoftonline.com
       - https://login.microsoftonline.com/te/**tenant ID**/oauth2/authresp
       (where <tenant ID> is your tenant ID)
       - https://login.microsoftonline.com/te/**tenant name**.onmicrosoft.com/oauth2/authresp
       (where <tenant name> is your tenant name)
   ```

1. 만들기를 선택합니다. **클라이언트 ID** 와 **클라이언트 비밀** 을 복사합니다. Azure Portal에서 ID 공급자를 추가할 때 복사한 정보를 사용합니다.

1. 프로젝트 게시 상태를 테스트 중으로 두고 OAuth 동의 화면에 테스트 사용자를 추가할 수 있습니다. 또는 OAuth 동의 화면에서 앱 게시 단추를 선택하여 Google 계정이 있는 모든 사용자가 앱을 사용할 수 있도록 할 수 있습니다.

#### <a name="task-2---configure-azure-ad-for-google-federation"></a>작업 2 - Google 페더레이션에 대한 Azure AD 구성

1. 제한된 관리자 디렉터리 역할 또는 게스트 초대자 역할에 할당된 사용자로 [https://portal.azure.com](https://portal.azure.com)에 로그인합니다.

1. **Azure Active Directory** 를 선택합니다.

1. **관리** 에서 **외부 ID** 를 선택합니다.

1. Microsoft는 **Google** 에 대한 직접 페더레이션을 ID 공급자로 제공합니다.  **외부 ID | 모든 ID 공급자** 페이지에서 **+ Google** 을 선택하여 시작할 수 있습니다.
 
1. \+ Google을 선택하면 Google을 ID 공급자로 구성하는 데 필요한 추가 정보가 포함된 다른 페이지가 열립니다.  

1. 미리 복사해 둔 클라이언트 ID와 클라이언트 암호를 입력합니다. [저장]을 선택합니다.

1. 이렇게 하면 Google이 ID 공급자로 구성됩니다.

**참고** - Google을 소셜 ID 공급자 메시지로 추가하지 못할 수 있습니다.  해당 화면에서 외부 ID로 다시 이동하고 목록에서 Google을 사용할 수 있어야 합니다.

1. 기존 Gmail 계정을 사용한 경우 **외부 ID | 모든 ID 공급자** 를 사용하여 계정을 삭제해야 합니다. Google 개발자 콘솔로 돌아가서 만든 프로젝트를 삭제할 수도 있습니다.

   **참고** - 이 링크를 사용하여 Google 클라이언트 ID 및 클라이언트 비밀을 찾는 단계를 완료합니다.
   https://docs.microsoft.com/azure/active-directory/external-identities/google-federation

   **참고** - Facebook은 ID 공급자로 쉽게 구성할 수도 있습니다. https://docs.microsoft.com/azure/active-directory/external-identities/facebook-federation 에서 다음 단계에 액세스할 수 있습니다. 이 연습에서는 Google이 아닌 Facebook 계정을 사용하려는 경우 이 옵션을 완료할 수 있습니다.

1. 설정이 완료되면 프라이빗 브라우저를 열고 다음 웹 주소를 입력할 수 있습니다.

   ```
   login.microsoftonline.com
   ```

1. 만든 **Google** 메일 주소 및 암호를 입력합니다.  그런 다음, 앱 액세스를 위해 Microsoft 온라인 포털을 입력해야 합니다.
