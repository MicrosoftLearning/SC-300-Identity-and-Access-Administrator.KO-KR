---
lab:
  title: 26 - Microsoft Entra 역할에 대한 Privileged Identity Management 구성
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# 랩 26: Microsoft Entra 역할에 대한 Privileged Identity Management 구성

## 랩 시나리오

권한 있는 역할 관리자는 적합 역할 할당을 활성화하는 사용자에 대한 환경 변경을 포함하여 Microsoft Entra 조직에서 PIM(Privileged Identity Management)을 사용자 지정할 수 있습니다. PIM을 구성하는 데 익숙해져야 합니다.

#### 예상 소요 시간: 30분

참고 - 랩 환경에서 MFA 요구 사항이 계속 변경되었습니다.  사용자 간에 전환하여 이 랩을 완료하면 MFA를 설정하라는 메시지가 표시될 수 있습니다.

### 연습 1 - Microsoft Entra 역할 설정 구성

#### 작업 1 - 역할 설정 열기

Microsoft Entra 역할에 대한 설정을 열려면 다음 단계를 따릅니다.

1. 전역 관리자로 [https://entra.microsoft.com](https://entra.microsoft.com)  에 로그인합니다.

2. **Privileged Identity Management**를 검색한 후 선택합니다.

3. Privileged Identity Management 페이지의 왼쪽 탐색 메뉴에서 **Microsoft Entra 역할**을 선택합니다.

4. 빠른 시작 페이지의 왼쪽 탐색 영역에서 **설정**을 선택합니다.

    ![설정 메뉴가 강조 표시된 Microsoft Entra 역할 페이지를 표시하는 화면 이미지](./media/lp3-mod3-pim-ad-roles-settings.png)

5. 역할 목록을 검토한 다음 **역할 이름으로 검색**에서 **준수**를 입력합니다.

6. 결과에서 **준수 관리자**를 선택합니다.

7. 역할 설정 세부 정보를 검토합니다.

#### 작업 2 - 활성화하려면 승인 필요

여러 승인자를 설정하는 경우 승인자 중 한 명이 승인되거나 거부되는 즉시 승인이 완료됩니다. 두 명 이상의 사용자에게 승인을 요구할 수 없습니다. 역할을 활성화하기 위해 승인을 요구하려는 경우 다음 단계를 따릅니다.

1. 역할 설정 정보 페이지의 상단 메뉴에서 **편집**을 선택합니다.

    ![역할 설정 세부사항 - 편집이 강조 표시된 준수 관리자 페이지 - 의 위쪽 부분을 표시하는 화면 이미지](./media/lp4-mod3-pim-edit-compliance-role.png)

2. 역할 편집 설정 – 준수 관리자 페이지에서 **활성화 승인 필요** 확인란을 선택합니다.

3. **승인자 선택**을 선택합니다.

4. 구성원 선택 창에서 관리자 계정을 선택한 다음 **선택**을 선택합니다.

    ![역할 설정 편집 페이지를 표시하고 선택한 구성원이 강조 표시된 구성원 창을 선택하는 화면 이미지](./media/lp4-mod3-pim-add-approver.png)

5. 역할 설정을 구성하면, **업데이트**를 선택해 변경 사항을 저장합니다.

### 연습 2 - Microsoft Entra 역할을 사용한 PIM

#### 작업 1 - 역할 할당

Microsoft Entra ID를 사용하면 전역 관리자가 영구적인 Microsoft Entra 관리자 역할을 할당할 수 있습니다. 이러한 역할 할당은 Microsoft Entra 관리 센터, Azure Portal 또는 PowerShell 명령을 사용하여 만들 수 있습니다.

PIM(Privileged Identity Management) 서비스를 사용하여 권한 있는 역할 관리자는 영구 디렉터리 역할을 할당할 수도 있습니다. 또한 권한이 있는 역할 관리자는 사용자의 Microsoft Entra 관리자 역할을 적격으로 만들 수 있습니다. 적격인 관리자는 필요할 때 역할을 활성화할 수 있으며 작업을 완료하고 나면 권한이 만료됩니다.

사용자가 Microsoft Entra 관리자 역할을 받을 수 있도록 하려면 다음 단계를 따릅니다.

1. 전역 관리자 계정을 사용하여 [https://entra.microsoft.com](https://entra.microsoft.com)에 로그인합니다.

2. **Privileged Identity Management**를 검색한 후 선택합니다.

    **참고** - ID - ID 거버넌스 - Privileged Identity Management 메뉴에서 찾을 수 있습니다.

3. Privileged Identity Management 페이지의 왼쪽 탐색 메뉴에서 **Microsoft Entra 역할**을 선택합니다.

4. 빠른 시작 페이지의 왼쪽 탐색 영역에서 **역할**을 선택합니다.

5. 상단 메뉴에서 + **할당 추가**를 선택합니다.

    ![할당 추가 메뉴가 강조 표시된 Microsoft Entra 역할을 표시하는 화면 이미지](./media/lp4-mod3-pim-assign-role.png)

6. 할당 추가 페이지의 **멤버 자격** 탭에서 설정을 검토합니다.

7. **역할 선택** 메뉴를 선택한 다음 **준수 관리자**를 선택합니다.

8. **이름으로 역할 검색** 필터를 사용하여 역할을 쉽게 찾을 수 있습니다.

9. **구성원 선택** 아래에서 **선택한 구성원이 없음**을 선택합니다.

10. 구성원 선택 창에서 **Miriam Graham**을 선택한 다음 **선택**을 선택합니다.

    ![선택 구성원이 강조 표시된 구성원 선택 창을 표시하는 화면 이미지](./media/lp4-mod3-pim-add-role-assignment.png)

11. 할당 추가 페이지에서 **다음**을 선택합니다.

12. **설정** 탭의 **할당 유형**에서 사용 가능한 옵션을 검토합니다. 해당 작업의 경우 기본 설정을 사용합니다.

    - 적격 할당에는 역할을 사용하는 작업을 수행하기 위해 역할의 멤버가 필요합니다. 작업은 MFA(Multi-Factor Authentication) 검사를 수행하고, 비즈니스 근거를 제공하거나 지정된 승인자의 승인을 요청하는 과정을 포함할 수 있습니다.
    - 활성 할당에는 역할을 사용하는 작업을 수행하기 위해 멤버가 필요하지 않습니다. 활성으로 할당된 구성원에게는 역할에 할당된 권한이 있습니다.

13. 나머지 설정을 검토하고 **할당하기**를 선택합니다.

#### 작업 2 - Miriam으로 로그인

1. 새 InPrivate 브라우저 창을 엽니다.
2. Microsoft Entra 관리 센터(https://entra.microsoft.com))에 연결합니다.
    **참고** - 사용자가 로그인된 상태로 Azure Portal이 열리면 오른쪽 위에서 해당 사용자 이름을 선택하고 **다른 계정으로 로그인**을 선택합니다.
3. Miriam으로 로그인합니다.

   | 필드 | 값 |
   | :--- | :--- |
   | 사용자 이름 | **MiriamG@** `<<your domain.onmicrosoft.com>>` |
   | 암호 |  테넌트의 관리자 암호를 입력합니다(테넌트 관리자 암호를 검색하려면 랩 리소스 탭 참조). |

4. **ID** 메뉴에서 **사용자**를 연 다음 **모든 사용자**를 선택합니다.
5. 사용자 목록에서 **Miriam**을 찾습니다.
6. **개요** 페이지에서 **할당된 역할**을 찾습니다.
7. **적합한 할당**를 선택합니다.
1. 현재 Miriam에게는 **준수 관리자** 역할을 할당할 수 있습니다.

#### 작업 3 - Microsoft Entra 역할 활성화

Microsoft Entra 역할을 맡아야 하는 경우 Privileged Identity Management에서 **내 역할**을 열어 활성화를 요청할 수 있습니다.

1. **리소스, 서비스 및 문서 검색** 창에서 Privileged를 검색합니다.
2. **Privileged Identity Management** 페이지를 엽니다.
3. 왼쪽 탐색 메뉴에서 Privileged Identity Management 페이지의 **내 역할**을 선택합니다.

4. 내 역할 페이지에서 **적격 할당** 목록을 검토합니다.

    ![적격 역할 할당이 강조 표시된 내 역할을 표시하는 화면 이미지](./media/lp4-mod3-my-roles.png)

5. 준수 관리자 역할 행에서 **활성화**를 선택합니다.

6. 활성화 – 준수 관리자 창에서 **추가 인증 필요**를 선택하고 지침에 따라 추가 보안 인증을 제공합니다. 세션당 한 번만 인증해야 합니다.

    ![준수 관리자를 활성화하는 팝업을 표시하는 화면 이미지](./media/lp4-mod3-pim-activate-role.png)

    **확인** - 현재 랩 환경 구성에 따라 MFA를 구성하여 정상적으로 로그인해야 합니다.

7. 추가 보안 인증을 완료한 후에 활성화 – 준수 관리자 창의 **이유** 상자에 **해당 역할을 활성화하기 위한 근거입니다.** 를 입력합니다.

    **중요 참고 사항** - 최소 권한 원칙에 따라 필요한 시간 동안만 계정을 활성화해야 합니다.  완료해야 하는 작업의 소요 시간이 1.5시간이라면 계정 활성화 기간을 2시간으로 설정합니다.  마찬가지로 오후 3시까지는 작업을 수행할 수 없다면 사용자 지정 활성화 시간을 선택합니다.

8. **활성화**를 선택합니다.

#### 작업 4 - 제한된 범위의 역할 할당

특정 역할의 경우 부여된 사용 권한의 범위는 단일 관리 단위, 서비스 주체 또는 애플리케이션으로 제한될 수 있습니다. 이 절차는 관리 단위의 범위를 포함하는 역할을 할당하는 경우의 예입니다.

1. MiriamG의 브라우저 창을 닫은 다음 관리자 계정으로 Microsoft Entra 관리 센터를 열어야 합니다.
2. Privileged Identity Management 페이지로 이동하여 왼쪽 탐색 메뉴에서 Azure **Microsoft Entra 역할**을 선택합니다.
3. **역할**을 선택합니다.
4. 역할 페이지의 상단 메뉴에서 **+ 할당 추가**를 선택합니다.

5. 할당 추가 페이지에서 **역할 선택** 메뉴를 선택한 다음, **사용자 관리자**를 선택합니다.

6. **범위 유형** 메뉴를 선택하고 사용 가능한 옵션을 검토합니다. 이제 **디렉터리** 범위 유형을 사용합니다.

   **팁** - 관리 단위 범위 유형에 대한 자세한 내용을 보려면 [https://docs.microsoft.com/en-us/azure/active-directory/roles/admin-units-manage](https://docs.microsoft.com/en-us/azure/active-directory/roles/admin-units-manage)로 이동하세요.

7. 제한된 범위 없이 역할을 할당할 때와 마찬가지로 구성원을 추가하고 설정 옵션을 완료합니다. 이제 **취소**를 선택합니다.

#### 작업 5 - 기존 역할 할당 업데이트 또는 제거

기존 역할 할당을 업데이트하거나 제거하려면 다음 단계를 수행합니다.

1. Privileged Identity Management 열기 > Microsoft Entra 역할 페이지의 왼쪽 탐색 메뉴에서 **할당**을 선택합니다.

2. 준수 관리자는 **할당** 목록에서 **작업** 열의 옵션을 검토합니다.

    ![준수 관리자의 작업 열에 나열된 옵션을 표시하는 화면 이미지](./media/lp4-mod3-pim-edit-role-assignments.png)

3. **업데이트**를 선택하고 멤버 자격 설정 창에서 사용할 수 있는 옵션을 검토합니다. 완료하면 창을 닫습니다.

4. **제거**를 선택합니다.

5. **제거** 대화 상자에서 정보를 검토한 다음 **예**를 선택합니다.
