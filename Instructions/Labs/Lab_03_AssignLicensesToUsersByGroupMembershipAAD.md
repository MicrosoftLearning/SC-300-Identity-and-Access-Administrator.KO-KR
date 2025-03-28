---
lab:
  title: 03 - 그룹 구성원 자격을 사용하여 라이선스 할당
  learning path: '01'
  module: Module 01 - Implement an identity management solution
---

# 랩 03: 그룹 구성원 자격을 사용하여 라이선스 할당

### 로그인 유형 = Microsoft 365 + E5 테넌트 로그인

## 랩 시나리오

조직에서 Microsoft Entra ID의 보안 그룹을 사용하여 라이선스를 관리하기로 결정했습니다. 새로운 보안 그룹을 구성하고, 해당 그룹에 라이선스를 할당하고, 그룹 구성원 라이선스가 업데이트되었는지 확인해야 합니다.

#### 예상 소요 시간: 25분

### 연습 1 - 보안 그룹 만들기 및 사용자 추가

#### 작업 1 - Delia Dennis에게 Office 365 액세스 권한이 있는지 확인

1. 새 InPrivate 브라우저 창을 시작합니다.
2. [https://www.office.com](https://www.office.com)에 연결합니다.
3. 로그인을 선택하고 Delia Dennis로 연결합니다.

   | **설정** | **값** |
   | :--- | :--- |
   | 사용자 이름 | DeliaD@`your domain name.com` |
   | 암호| DeliaD에 제공된 사용자 암호를 입력합니다. |

4. Office.com 웹 사이트에 연결은 되지만 라이선스가 없다는 메시지가 표시됩니다.

   ![Delia Dennis로 로그인한 Office.com 웹 사이트의 화면 이미지. 라이선스가 할당되어 있지 않아 Office 애플리케이션을 사용할 수 없음.](./media/delia-no-office-license.png)
    
5. 브라우저 창을 닫습니다.

#### 작업 2 - Microsoft Entra ID에서 보안 그룹 만들기

1. [https://entra.microsoft.com](https://entra.microsoft.com)으로 이동합니다.

2. 왼쪽 탐색 메뉴의 **ID**에서 **그룹**을 선택한 다음 **모든 그룹**을 선택합니다.
3. 그룹 페이지의 메뉴에서 **새 그룹**을 선택합니다.
4. 다음 정보를 사용하여 그룹을 생성합니다.

   | **설정**| **값**|
   | :--- | :--- |
   | 그룹 형식| 보안|
   | 그룹 이름| sg-SC300-O365|
   | 멤버 자격 유형| 할당됨|
   | 소유자| *자신의 관리자 계정을 그룹 소유자로 할당*|

5. 구성원 아래에서 **선택한 멤버가 없음** 텍스트를 선택합니다.
6. 사용자 목록에서 **Delia Dennis**를 선택합니다.
7. **선택** 단추를 누릅니다.

   ![그룹 유형, 그룹 이름, 소유자, 구성원이 강조 표시된 새 그룹 페이지를 보여 주는 화면 이미지](./media/lp1-mod2-create-group.png)

8. **생성** 단추를 선택합니다.
9. 만들기가 완료되면 **sg-SC300-O365** 그룹이 **모든 그룹** 목록에 표시되는지 확인합니다.

#### 작업 3 - sg-SC300-O365에 Office 라이선스 추가

**랩 팁** - Microsoft 365 관리 센터를 통해 라이선스를 추가 및 제거해야 합니다. 이것은 비교적 새로운 변화입니다.

1. 웹 브라우저에서 새 탭을 엽니다.

2. Microsoft 365 관리 센터(http://admin.microsoft.com)에 연결합니다.

3. 메시지가 표시되면 관리자 계정으로 로그인합니다.

4. 왼쪽 메뉴에서 **청구**를 선택한 다음 **라이선스**를 선택합니다.

5. 목록에서 **Office 365 E3** 라이선스를 선택합니다.

6. 라이선스 화면에서 **그룹** 탭을 선택합니다.

7. **+ 라이선스 할당** 항목을 선택합니다.

8. **sg-SC300-O365** 그룹을 검색하여 목록에서 선택합니다.

8. 그룹을 추가한 후 **할당**을 선택합니다.
 
9. 확인 메시지를 닫습니다.

10. 브라우저 탭으로 돌아가서 **Microsoft Entra 관리 센터**를 엽니다.

11. 왼쪽 탐색에서 **모든 사용자**로 돌아가서 **ID** 아래에서 **사용자**를 선택합니다.

12. 그룹 페이지에서 **sg-SC300-O365**를 선택합니다.

13. 왼쪽 탐색 영역에서 **라이선스**를 선택합니다.

14. Office 365 E3 라이선스가 할당되었음을 확인합니다.

15. 라이선스 화면에서 종료할 수 있습니다.

#### 작업 4 - Office 365 라이선스 확인

1. 새 InPrivate 브라우저 창을 시작합니다.
2. [https://www.office.com](https://www.office.com)에 연결합니다.
3. 로그인을 선택하고 Delia Dennis로 연결합니다.

   | **설정**| **값**|
   | :--- | :--- |
   | 사용자 이름 | DeliaD@`your domain name.com`|
   | 암호| 제공된 비밀번호를 입력합니다.  |

4. Office.com 웹 사이트에 연결하여 라이선스 관련 메시지가 없는지 확인해야 합니다. 모든 Office 애플리케이션은 왼쪽에서 사용할 수 있습니다.

   ![Delia Dennis로 로그인한 Office.com 웹 사이트의 화면 이미지. 라이선스가 할당되었으므로 Office 애플리케이션을 사용할 수 있음.](./media/delia-office-license.png)
    
5. 브라우저 창을 닫습니다.

### 연습 2 - Microsoft Entra ID에서 Microsoft 365 그룹 만들기

#### 작업 1 - 그룹 만들기

Microsoft Entra 관리자의 업무 중 하나는 다양한 유형의 그룹을 만드는 것입니다. 조직의 영업부를 위해 새로운 Microsoft 365 그룹을 만들어야 합니다.

1. [https://entra.microsoft.com]( https://entra.microsoft.com) 으로 이동합니다.

2. 왼쪽 탐색 메뉴의 **ID**에서 **그룹**을 선택한 다음 **모든 그룹**을 선택합니다.

3. 그룹 페이지의 메뉴에서 **새 그룹**을 선택합니다.

4. 다음 정보를 사용하여 그룹을 생성합니다.

   | **설정**| **값**|
   | :--- | :--- |
   | 그룹 형식| Microsoft 365|
   | 그룹 이름| 북서부 판매액|
   | 멤버 자격 유형| 할당됨|
   | 소유자| *자신의 관리자 계정을 그룹 소유자로 할당*|
   | 멤버| **Alex Wilber** 및 **Bianca Pisani**|

   ![그룹 유형, 그룹 이름, 소유자, 구성원이 강조 표시된 새 그룹 페이지를 보여 주는 화면 이미지](./media/lp1-mod2-create-o365-group.png)

5. 완료되면 이름이 **Northwest sales**라는 그룹이 **모든 그룹** 목록에 표시되는지 확인합니다.

### 연습 3 - 모든 사용자를 구성원으로 사용하여 동적 그룹 만들기

#### 작업 1 - 동적 그룹 만들기

회사가 성장함에 따라 수동으로 그룹을 관리하는 것은 시간이 너무 오래 걸릴 수 있습니다. 디렉터리를 표준화한 이후에는 동적 그룹을 활용할 수 있습니다. 실제로 동적 그룹을 생성할 준비가 되었는지 확인하기 위해 새로운 동적 그룹을 만들어봐야 합니다.

1. 제공된 관리자 계정으로 [https://entra.microsoft.com](https://entra.microsoft.com)에 로그인합니다. 테넌트에서 최소한 사용자 관리자 역할이 필요합니다.

2. **ID**를 선택합니다.

3. **그룹**에서 **모든 그룹**을 선택한 다음 **새 그룹**을 선택합니다.

4. 새 그룹 페이지의 **그룹 종류**에서 **보안**을 선택합니다.

5. **그룹 이름** 상자에 **SC300-myDynamicGroup**을 입력합니다.

6. **구성원 자격 유형** 메뉴를 선택하고 **동적 사용자**를 선택합니다.

7. 그룹의 **소유자**를 선택합니다.

7. **동적 사용자 구성원**에서 **동적 쿼리 추가**를 선택합니다.

8. **규칙 구문** 상자 오른쪽 위에 있는 **편집**을 선택합니다.

9. 규칙 구문 편집 창에서 **규칙 구문** 상자에 다음 식을 입력합니다.

   ```powershell
   user.objectId -ne null
   ```

   **경고** - `user.objectId`는 대/소문자를 구분합니다.

10. **확인**을 선택합니다. 규칙은 규칙 구문 상자에 나타납니다.

   ![규칙 구문이 강조 표시된 동적 그룹 구성원 자격 규칙 페이지를 보여 주는 화면 이미지](./media/lp1-mod3-dynamic-group-membership-rule.png)

11. **저장**을 선택합니다. 새 동적 그룹에는 이제 구성원 사용자뿐만 아니라 B2B 게스트 사용자도 포함됩니다.

12. 새 그룹 페이지에서 **생성**를 선택하여 그룹을 생성합니다.

#### 작업 2 - 구성원이 추가되었는지 확인

**참고** - 동적 그룹 멤버 자격의 모집단은 최대 15분이 걸릴 수 있습니다.

1. **홈** `Microsoft Entra admin center`에서 선택합니다.
2. **ID**시작합니다.
3. **그룹** 메뉴에서 **모든 그룹 **선택합니다.
4. 필터 상자에 **SC300**을 입력하면 새로 만든 그룹이 목록에 표시됩니다.
5. **SC300-myDynamicGroup**을 선택하여 그룹을 엽니다.
6. 그룹의 *직접 구성원 수가 30명이 넘는다는 메시지가 표시됩니다.
7. **관리** 메뉴에서 **구성원**을 선택합니다.
8. 구성원을 검토합니다.

#### 작업 3 - 다른 규칙 사용해 보기

1. **게스트** 사용자만 포함된 그룹을 만들어 봅니다.

   - (user.objectId -ne null) 및 (user.userType -eq "Guest") 식을 사용하면 됩니다.

2. Microsoft Entra 사용자 **멤버**만 포함된 그룹을 만들어 봅니다.

   - (user.objectId -ne null) 및 (user.userType -eq "Member") 식을 사용하면 됩니다.

**랩 팁** - 그룹 생성 실패 메시지에서 잘못된 연산자가 언급될 경우, 연산자의 맞춤법을 확인합니다.  objectId의 I와 userType의 T는 대문자임에 유의합니다.
