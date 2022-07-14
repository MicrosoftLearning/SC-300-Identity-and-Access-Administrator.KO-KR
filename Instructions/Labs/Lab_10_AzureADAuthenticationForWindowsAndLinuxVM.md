---
lab:
  title: 10 - Windows 및 Linux 가상 머신에 대한 Azure AD 인증
  learning path: "02"
  module: Module 02 - Implement an Authentication and Access Management Solution
ms.openlocfilehash: 82dcb43bdae3df54a80625dc29134d4497207d8c
ms.sourcegitcommit: 80c5c0ef60c1d74fcc58c034fe6be67623013cc0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2022
ms.locfileid: "146823189"
---
# <a name="lab-10---azure-ad-authentication-for-windows-and-linux-virtual-machines"></a>랩 10 - Windows 및 Linux 가상 머신에 대한 Azure AD 인증

**참고** - 이 랩에는 Azure Pass가 필요합니다. 지침은 랩 00을 참조하세요.

## <a name="lab-scenario"></a>랩 시나리오

회사는 원격 액세스를 위해 가상 머신에 로그인하는 데 Azure Active Directory를 사용하도록 결정했습니다.  이 랩에서는 Windows 및 Linux 가상 머신에 대해 설정하는 방법을 보여 줍니다.

#### <a name="estimated-time-30-minutes"></a>예상 소요 시간: 30분

### <a name="exercise-1---login-to-windows-virtual-machines-in-azure-with-azure-ad"></a>연습 1 - Azure AD를 사용하여 Azure에서 Windows Virtual Machines에 로그인

#### <a name="task-1---create-a-windows-virtual-machine-with-azure-ad-login-enabled"></a>작업 1 - Azure AD 로그인을 사용하도록 설정된 Windows Virtual Machine 만들기

1. [https://portal.azure.com](https://portal.azure.com)으로 이동

1. **+ 리소스 생성** 를 선택합니다.

1. Marketplace 검색 창에서 **Windows Server** 를 입력합니다.

1. **Windows Server** 를 선택하고 소프트웨어 플랜 드롭다운 목록에서 **Windows Server 2019 Datacenter** 를 선택합니다.

1. 기본 탭에서 VM의 관리자 사용자 이름과 암호를 만들어야 합니다.

1. **관리** 탭의 Azure AD 섹션에서 Azure AD로 로그인 확인란을 선택합니다.

1. ID 섹션에서 **시스템이 할당한 관리 ID** 확인란을 선택합니다. Azure AD로 로그인하도록 설정했으면 자동으로 선택됩니다.

1. 가상 머신을 만드는 과정의 나머지 단계를 진행합니다. 

1. 만들기를 선택합니다.

#### <a name="task-2---azure-ad-login-for-existing-azure-virtual-machines"></a>작업 2 - 기존 Azure Virtual Machines에 대한 Azure AD 로그인

1. [https://portal.azure.com](https://portal.azure.com)에서 **가상 머신** 으로 이동합니다.

1. **액세스 제어(IAM)** 를 선택합니다.

1. **추가** 를 선택한 다음, **역할 할당 추가** 를 선택하여 역할 할당 추가 페이지를 엽니다.

1. 다음 역할을 할당합니다. 
    - **역할**: Virtual Machine 관리자 로그인 또는 Virtual Machine 사용자 로그인
    - **다음에 대한 액세스 할당**: 사용자, 그룹, 서비스 주체 또는 관리 ID

1. 세부 단계에 대해서는 Azure Portal을 사용하여 Azure 역할 할당을 참조하세요.

### <a name="exercise-2---login-to-linux-virtual-machines-in-azure-with-azure-ad"></a>연습 2 - Azure AD를 사용하여 Azure에서 Linux Virtual Machines에 로그인

#### <a name="task-1---create-a-linux-vm-with-system-assigned-managed-identity"></a>작업 1 - 시스템 할당 관리 ID를 사용하여 Linux VM 만들기

1. [https://portal.azure.com](https://portal.azure.com)으로 이동

1. **+ 리소스 생성** 를 선택합니다.

1. 인기 보기의 **Ubuntu Server 18.04 LTS** 에서 **만들기** 를 선택합니다.

1. **관리** 탭에서 확인란을 선택하여 **Azure Active Directory로 로그인(미리 보기)** 을 사용하도록 설정합니다.

1. **시스템이 할당한 관리 ID** 가 선택되어 있는지 확인합니다.

1. 가상 머신을 만드는 과정의 나머지 단계를 진행합니다. 이 미리 보기 중에는 사용자 이름 및 암호 또는 SSH 공개 키를 사용하여 관리자 계정을 만들어야 합니다.

#### <a name="task-2---azure-ad-login-for-existing-azure-virtual-machines"></a>작업 2 - 기존 Azure Virtual Machines에 대한 Azure AD 로그인

1. [https://portal.azure.com](https://portal.azure.com)에서 **가상 머신** 으로 이동합니다.

1. **액세스 제어(IAM)** 를 선택합니다.

1. 추가 > 역할 할당 추가를 선택하여 역할 할당 추가 페이지를 엽니다.

1. 다음 역할을 할당합니다. 
    - **역할**: Virtual Machine 관리자 로그인 또는 Virtual Machine 사용자 로그인
    - **다음에 대한 액세스 할당**: 사용자, 그룹, 서비스 주체 또는 관리 ID

1. 세부 단계에 대해서는 Azure Portal을 사용하여 Azure 역할 할당을 참조하세요.
