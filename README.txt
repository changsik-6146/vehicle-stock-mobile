# 차량 재고 조회 - OneDrive 연동용

## 현재 상태
- 정적 웹앱 소스는 준비됨.
- Microsoft Entra 앱 등록(Client ID)과 HTTPS 배포 주소 등록이 필요함.
- 앱은 Microsoft Graph delegated `Files.Read` 권한으로 사용자가 선택한 OneDrive Excel 파일을 읽음.
- 차량 데이터는 웹페이지 소스에 포함하지 않음.

## Microsoft 앱 등록
1. https://entra.microsoft.com/ 접속 후 App registrations > New registration.
2. 지원 계정 유형에서 개인 Microsoft 계정(consumer accounts)을 포함하는 유형 선택.
3. Redirect URI 플랫폼을 Single-page application(SPA)으로 선택.
4. 배포한 웹페이지의 HTTPS 주소를 Redirect URI로 등록.
5. Overview의 Application (client) ID 복사.
6. API permissions에서 Microsoft Graph delegated `Files.Read`와 `User.Read` 추가.
7. index.html에서 CLIENT_ID 값에 복사한 ID 입력.
8. 정적 호스팅에 다시 배포.

## OneDrive 연결
웹페이지에서 Microsoft 로그인 > 엑셀 파일 찾기 > 실제 차량관리 엑셀 선택.
새로고침 버튼은 OneDrive 파일을 다시 검색/다운로드함.
PC Excel 저장 후 OneDrive 동기화가 완료된 뒤 새로고침해야 최신본이 보임.

## 주의
- Client ID는 공개 클라이언트 식별자이며 비밀번호가 아님. Client Secret을 브라우저 코드에 넣지 말 것.
- 공개 저장소에 실제 차량 데이터, 엑셀 원본, 토큰을 올리지 말 것.
- 개인용 OneDrive의 Excel Workbook API 대신 Graph driveItem 파일 다운로드 API를 사용.
- 현재 파일 파싱 셀: C6 차종, I6 차량번호, G14 가격(원), C9 특이사항, D21 차량위치.
- 실제 엑셀의 셀 주소가 바뀌면 코드의 셀 주소도 맞춰야 함.
