---
lab:
  title: 12 - Microsoft Entra 스마트 잠금 값 관리
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# 랩 12 - Microsoft Entra 스마트 잠금 값 관리

### 로그인 유형 = Microsoft 365 관리

## 랩 시나리오

조직에 대한 추가 암호 보호 설정을 구성해야 합니다.

#### 예상 소요 시간: 5분

### 연습 1 - Microsoft Entra 스마트 잠금 값 관리

#### 작업 - 스마트 잠금 추가

조직의 요구 사항에 따라 Microsoft Entra 스마트 잠금 값을 사용자 지정할 수 있습니다. 조직에 특수한 값이 있는 스마트 잠금 설정의 사용자 지정에는 Microsoft Entra ID Premium P1 또는 사용자에 대한 높은 라이선스가 필요합니다.

1. [https://entra.microsoft.com](https://entra.microsoft.com)으로 이동한 후 해당 디렉터리에 대한 전역 관리자 계정을 사용하여 로그인합니다.

2. 포털 메뉴를 열고  **ID**를 선택합니다.

3. ID 메뉴에서 **보호** 메뉴를 엽니다.

4. 왼쪽 탐색 메뉴에서 **인증 방법**을 선택합니다.

5. 그런 다음 **암호 보호**를 선택합니다.

    ![인증 방법 페이지 및 암호 인증으로 이동하는 선택이 강조 표시된 화면 이미지](./media/lp2-mod3-browse-to-password-protection.png)

6. **암호 보호 설정의 잠금 기간(초)** 상자에서 값을 **120**으로 설정합니다.

7. **모드** 옆의 **적용**을 선택합니다.

8. 변경 내용을 저장합니다.

    **참고** - 스마트 잠금 임계값이 트리거되면 계정이 잠겨 있는 동안 다음 메시지가 나타납니다.
    - 권한 없는 사용을 방지하기 위해 계정이 일시적으로 잠겨 있습니다. 나중에 다시 시도하세요. 문제가 계속 발생하면 관리자에게 문의하세요.

9. 이는 Microsoft Entra 테넌트에서 사용자를 선택하고 프라이빗 브라우저에서 <login.microsoftonline.com>으로 이동한 다음, 계정이 잠겨 있다는 알림을 받을 때까지 잘못된 암호를 입력하여 테스트할 수 있습니다.
