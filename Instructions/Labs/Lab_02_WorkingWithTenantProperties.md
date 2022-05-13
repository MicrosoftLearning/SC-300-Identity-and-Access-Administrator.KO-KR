---
lab:
  title: 02 - 테넌트 속성으로 작업
  learning path: "01"
  module: Module 01 - Implement an Identity Management Solution
ms.openlocfilehash: 36c7cdf2641017f0d9a15cfc2118f2d0bbeb1548
ms.sourcegitcommit: a60b8d48791d600c44fa5fa617b6a9b2c0edaa71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2022
ms.locfileid: "141368855"
---
# <a name="lab-02-working-with-tenant-properties"></a>랩 02: 테넌트 속성 사용

## <a name="lab-scenario"></a>랩 시나리오

테넌트와 연관된 다양한 속성을 식별하고 업데이트해야 합니다.

#### <a name="estimated-time-10-minutes"></a>예상 소요 시간: 10분

### <a name="exercise-1---changing-the-tenant-display-name"></a>연습 1 - 테넌트 표시 이름 변경

#### <a name="task-1---set-the-tenant-name-and-technical-contact"></a>작업 1 - 테넌트 이름 및 기술 담당자 설정

1. [https://portal.azure.com](https://portal.azure.com)으로 이동한 후 해당 디렉터리에 대한 전역 관리자 계정을 사용하여 로그인합니다.

2. **포털 표시 메뉴** 햄버거 아이콘을 선택하고 **Azure Active Directory** 를 선택합니다.

    ![Azure Active Directory가 선택된 Azure Portal 메뉴](./media/azure-portal-menu-aad.png)

3. 왼쪽 창의 관리 섹션에서 **속성** 을 선택합니다.

4. 대화 상자에서 테넌트 속성의 **이름** 및 **기술 담당자** 를 변경합니다.

| **설정** | **값** |
| :--- | :--- |
| Name | Contoso Marketing |
| 기술 담당자 | `your Global admin account` |

5. **저장** 을 선택하여 테넌트 속성을 업데이트합니다.

   **저장이 완료되면 이름이 즉시 변경됩니다.**

#### <a name="task-2---review-the-country-or-region-and-other-values-associated-with-your-tenant"></a>작업 2 - 테넌트와 연관된 국가나 지역 및 기타 값 검토

1. **Azure Active Directory** 블레이드의 관리 섹션에서 **속성** 을 선택합니다.

2. **테넌트 속성** 에서 **국가 또는 지역** 을 찾아 정보를 검토합니다.

    **중요** - 국가나 지역은 테넌트를 만들 때 지정됩니다. 이 설정은 나중에 변경할 수 없습니다.

3. **속성** 블레이드의 **테넌트 속성** 에서 **위치** 를 찾아서 정보를 검토합니다.

    ![국가 또는 지역 설정과 위치 설정이 강조 표시된 Azure Active Directory 속성 블레이드를 보여주는 화면 이미지](./media/azure-active-directory-properties-country-location.png)

#### <a name="task-3---finding-the-tenant-id"></a>작업 3 - 테넌트 ID 찾기

Azure 구독은 Azure AD(Azure Active Directory)와 트러스트 관계가 있습니다. Azure AD는 구독에 대한 사용자, 서비스, 디바이스를 인증하는 데 신뢰할 수 있습니다. 각 구독에는 연결된 테넌트 ID가 있으며, 구독에 대한 테넌트 ID를 찾을 수 있는 몇 가지 방법이 있습니다.

1. **Azure Active Directory** 블레이드의 관리 섹션에서 **속성** 을 선택합니다.

2. **테넌트 속성** 에서 **테넌트 ID** 를 찾습니다. 고유한 테넌트 식별자입니다.

    ![테넌트 ID 상자가 강조 표시된 테넌트 속성 페이지를 표시하는 화면 이미지](./media/portal-tenant-id.png)

### <a name="exercise-2---setting-your-privacy-information"></a>연습 2 - 개인 정보 설정

#### <a name="task-1---adding-your-privacy-info-on-azure-ad-including-global-privacy-contact-and-privacy-statement-url"></a>작업 1 - Azure AD에서 전역 개인 정보 보호 연락처, 개인정보처리방침 등의 개인 정보 추가

전역 개인 정보 보호 연락처와 조직의 개인정보처리방침을 모두 추가하는 것이 좋습니다. 그러면 내부 직원과 외부 게스트가 정책을 검토할 수 있습니다. 개인정보처리방침이 고유하게 생성되고 각 비즈니스에 맞게 조정되기 때문에 도움말은 변호사에게 문의하는 것이 좋습니다.

   **참고** - 개인 데이터를 보거나 삭제하는 방법에 대한 자세한 내용은 [https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure)를 참조하세요. GDPR에 대한 자세한 내용은 [https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted)를 참조하세요.

Azure AD의 **속성** 영역에 조직의 개인 정보를 추가합니다. 속성 영역에 액세스하고 개인 정보를 추가하려면:

1. **Azure Active Directory** 블레이드의 관리 섹션에서 **속성** 을 선택합니다.

    ![기술 담당자, 전역 연락처, 개인정보처리방침 상자가 강조 표시된 테넌트 속성을 보여주는 화면 이미지](./media/properties-area.png)

2. 직원의 개인 정보를 추가합니다.

- **전역 개인 정보 보호 연락처** - `AllanD@` **Azure 랩 도메인**
     - Azure 랩 테넌트의 기본 제공 사용자인 Allan Deyoung은 IT 관리자입니다. 이 랩에서는 Allan을 개인 정보 보호 연락처로 사용합니다.
     - 이 사용자는 데이터 위반이 발생하는 경우 Microsoft에서 연락할 사람이기도 합니다. 여기에 나열된 사용자가 없는 경우 Microsoft에서는 전역 관리자에게 연락합니다.

- **개인정보처리방침 URL** -  `https://github.com/R-C-Stewart/SC-300-Identity-and-Access-Administrator/blob/master/Allfiles/Labs/Lab2/SC-300-Lab_ContosoPrivacySample.pdf`
     - 샘플 개인 정보 PDF는 랩 디렉터리에서 제공됩니다.
     - 조직이 내부 및 외부 게스트의 데이터 개인 정보를 모두 처리하는 방법을 설명하는 조직의 문서에 대한 링크를 입력합니다.

    **중요** - 고유한 개인정보처리방침 또는 개인 정보 보호 연락처를 포함하지 않는 경우 외부 게스트는 검토 권한 상자에 “ **<조직 이름\>** 에서는 검토할 해당 약관에 대한 링크를 제공하지 않습니다”라는 텍스트를 보게 됩니다. 예를 들어 게스트 사용자는 B2B 협업을 통해 조직에 액세스하는 초대를 받을 때 이 메시지를 확인하게 됩니다.

    ![메시지를 포함한 B2B 협업 검토 권한 상자](./media/active-directory-no-privacy-statement-or-contact.png)

3. **저장** 을 선택합니다.

#### <a name="task-2---check-your-privacy-statement"></a>작업 2 - 개인정보처리방침 확인

1. Azure 홈 화면 - 대시보드로 돌아옵니다.
2. UI 오른쪽 위에서 사용자 이름을 클릭합니다.
3. 드롭다운 메뉴에서 **계정 보기** 를 선택합니다.

     **새 브라우저 탭이 자동으로 열립니다.**

4. 왼쪽 메뉴에서 **설정 및 프라이버시** 를 선택합니다.
5. **개인 정보** 를 선택합니다.
6. **조직의 알림** 에서 Contoso Marketing 조직 개인정보처리방침 옆의 **보기** 항목을 선택합니다.

     **새 브라우저 탭이 열리고 연결한 개인 정보 PDF 파일이 표시됩니다.**

7. 샘플 개인정보처리방침을 검토합니다.
8. PDF가 표시된 브라우저 탭을 닫습니다.
9. **내 계정** 항목이 표시된 브라우저 탭을 닫습니다.
