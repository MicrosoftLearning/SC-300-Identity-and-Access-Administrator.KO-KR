---
lab:
  title: 27 - Microsoft Entra 데이터 원본에 대한 Microsoft Sentinel Kusto 쿼리
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# 랩 27 - Microsoft Entra 데이터 원본에 대한 Microsoft Sentinel Kusto 쿼리

**참고** - 이 랩에는 Azure Pass가 필요합니다. 지침은 랩 00을 참조하세요.

## 랩 시나리오

Microsoft Sentinel은 Microsoft의 클라우드 네이티브 SIEM 및 SOAR 솔루션입니다.  Microsoft 및 타사 보안 솔루션에서 데이터 원본을 연결하면 보안 조작 작업을 실행할 수 있습니다.  이 랩 연습에서는 KQL(Kusto 쿼리 언어)을 사용하여 헌팅 쿼리를 실행하기 위해 Azure AD에 대한 데이터 커넥터가 있는 Microsoft Sentinel 작업 영역을 만듭니다. 

#### 예상 소요 시간: 30분

### 연습 1 - Kusto 쿼리에 대한 Microsoft Sentinel 구성

#### 작업 1 - Microsoft Sentinel 작업 영역 만들기

1. 전역 관리자로 [https://portal.azure.com](https://portal.azure.com)  에 로그인합니다.

1. **Microsoft Sentinel**을 검색한 다음, 이를 선택합니다. 

1. 왼쪽 위 모서리에서 +만들기**를 선택합니다**.

1. **작업 영역에 Microsoft Sentinel 추가** 타일에서 **새 작업 영역 만들기**를 선택합니다.

1. **리소스 그룹**에서 **새로 만들기**를 선택하고 **Sentinel-RG**를 입력합니다.

1. 작업 영역의 이름을 지정합니다.  예제 - SentinelLogAnalytics.

1. 가까운 지역을 선택합니다.

1. **검토 + 만들기**, **만들기**를 차례로 선택합니다.

1. Log Analytics 작업 영역 배포가 완료되면, **새로 고침** 단추를 선택합니다. 그런 다음, 작업 영역을 선택하고 **추가**를 선택합니다.  그러면 Microsoft Sentinel에 작업 영역이 추가되고 Microsoft Sentinel이 열립니다.

1. 메시지가 표시되면 **확인**을 선택하여 Microsoft Sentinel 평가판을 활성화합니다.

#### 작업 2 - 데이터 원본으로 Azure AD 추가
    **Note** - As of 11/1/2023, the data source is still Azure AD (not Microsoft Entra ID)

1. Microsoft Sentinel에서 **메뉴에서 콘텐츠 관리**로 이동하고 **콘텐츠 허브**를 선택합니다****.

1. 검색 상자를 사용하여 커넥터 목록에서 Azure**를 찾고**, Azure Active Directory**를 찾고**, 검사 상자를 표시합니다.

1. 오른쪽에는 미리 보기 타일이 열립니다.  **설치**를 선택합니다.

1. 설치가 완료되면 구성 메뉴에서 데이터 커넥터** 메뉴 항목을 선택합니다**.

    **참고** - 1개의 커넥트or가 설치되어 있고 나열된 Microsoft Entra ID**를 표시**해야 합니다.

1. **Microsoft Entra ID**를 선택한 다음 커넥터 페이지** 열기를 선택합니다**.

1. 커넥터 페이지에서 데이터 커넥터에 대한 지침과 다음 단계가 제공됩니다. **구성**을 계속하려면 각 **필수 구성 요소** 옆에 확인 표시가 있는지 확인합니다.

1. **구성**에서 **로그인 로그** 및 **감사 로그**에 대한 확인란을 선택합니다. 추가 로그 원본은 사용할 수 있지만 현재 **미리 보기**로 제공되며 이 과정의 범위를 벗어납니다.

1. **변경 내용 적용**을 선택합니다. 

1. 변경 내용이 성공적으로 적용되었다는 알림이 제공됩니다. 커넥터 페이지의 오른쪽 위에 있는 **X**를 선택하여 **Microsoft Sentinel** 작업 영역으로 이동합니다.

1. **Microsoft Sentinel | 데이터 커넥터** 타일에서 **새로 고침**을 선택하고, 숫자 1은 **연결된** 수에 표시됩니다.

   **참고** - Azure AD 데이터 커넥터는 활성 수에 표시하는 데 몇 분 정도 걸릴 수 있습니다. 

#### 작업 3 - 사용자 활동에 대한 Kusto 쿼리 실행

1. **Microsoft Sentinel**에서 **일반** 메뉴 제목 아래의 **로그**로 이동합니다.

1. **Log Analytics 시작** 창을 닫습니다.

1. 샘플 쿼리가 포함된 창이 열리고, 감사를** 선택하고**, 검색하여 사용자 ID를 찾**습니다**.

1. **실행**을 선택합니다. 

1. 그러면 Microsoft Entra ID의 사용자 ID 목록이 표시됩니다.  작업 영역을 방금 만들었으므로 결과가 표시되지 않을 수 있습니다.  쿼리의 형식을 확인합니다.

1. 메뉴의 **위협 관리**에서 **헌팅**을 선택합니다. 

1. 아래로 스크롤하여 **사용자 계정 및 인증 애플리케이션별 비정상적인 로그인 위치** 쿼리를 찾습니다.  Microsoft Entra 로그인에 대한 이 쿼리는 각 Microsoft Entra 애플리케이션에 대한 모든 사용자 로그인을 고려하고 개별 애플리케이션 내의 사용자에 대한 위치 프로필에서 가장 비정상적인 변경 사항을 선택합니다. 의도는 특정 애플리케이션 벡터를 통해 사용자 계정 손상에 대한 헌팅입니다. 

1. **쿼리 결과 보기**를 선택하여 쿼리를 실행합니다.

1. 이렇게 하면 새 작업 영역에 대한 결과가 제공되지 않을 수 있지만, 이제 쿼리를 실행하여 정보를 수집하거나 잠재적 위협을 헌팅하는 방법을 알아보았습니다.
