# KODA 일일동향 뉴스 포털

## 구성
- `index.html`: 일반 공개용 뉴스 포털
- `admin.html`: 협회 담당자용 뉴스 등록/수정/삭제 도구
- `app.js`: 구글 시트 CSV 연결, 날짜/분야/검색 필터
- `news.json`: 관리자 수기 등록 뉴스
- `style.css`: PC 및 모바일 반응형 디자인
- `koda-logo.png`, `koda-symbol.png`: 제공받은 협회 로고

## 구글 시트 연결
공개 페이지는 다음 공개 CSV를 브라우저에서 직접 불러옵니다.

`https://docs.google.com/spreadsheets/d/e/2PACX-1vTZSE8w18mQ75Blx6U6nkJHaNWGe-O9NaSROYsdTrglBn_fa1VqtGwva4GULoymaopAn_J9lpwAoJnu/pub?gid=0&single=true&output=csv`

시트가 웹에 게시되어 있어야 하며, CSV 공개 접근이 허용되어야 합니다. 이 작업 환경에서는 Google의 CSV 응답을 직접 가져오지 못해 실제 열 제목과 행 구조를 확인하지 못했습니다. 따라서 `app.js`는 날짜/일자, 제목/기사명, 분야/카테고리, 언론사/출처, 요약/내용, URL/링크와 같은 일반적인 열 이름을 자동으로 찾아 연결하도록 만들었습니다. 날짜 열이 없으면 첫 번째 열, 제목 열이 없으면 두 번째 열을 기본값으로 사용합니다. 실제 시트의 열 이름이 다르면 업로드 후 CSV 파일을 전달해 주시면 정확하게 맞출 수 있습니다.

## GitHub Pages 배포
1. GitHub 저장소(예: `koda-daily-news`)를 생성합니다.
2. 이 폴더 안의 파일 전체를 저장소 최상위(root)에 업로드합니다.
3. 저장소의 **Settings → Pages**에서 **Deploy from a branch**를 선택합니다.
4. Branch `main`, Folder `/ (root)`를 선택하고 저장합니다.
5. 배포 주소는 `https://깃허브계정.github.io/koda-daily-news/` 형태입니다.

## 매일 뉴스 등록
1. 공개 사이트 주소 뒤에 `admin.html`을 붙여 관리자 화면으로 이동합니다.
2. 게시일, 분야, 제목, 출처, 원문 URL, 핵심 요약을 입력하고 저장합니다.
3. `news.json 다운로드`를 누릅니다.
4. GitHub 저장소의 기존 `news.json`을 교체하고 Commit changes를 누릅니다.
5. 공개 페이지는 구글 시트 뉴스와 `news.json`의 수기 등록 뉴스를 함께 표시합니다.

## 중요: 관리자 권한과 보안
GitHub Pages는 정적 웹 호스팅입니다. 이 관리자 화면은 브라우저에서 JSON을 편집/내보내는 도구이며, 저장 버튼만으로 원격 GitHub 파일을 직접 변경하지 않습니다. 내보낸 `news.json`을 저장소에 커밋해야 모든 방문자에게 공개됩니다. 관리자 URL에 접근 제어가 없으므로 주소를 비밀번호처럼 취급하지 마세요. GitHub 토큰을 HTML/JavaScript 안에 넣는 방식은 사용하지 마세요.

## 기사 저작권
언론사 기사 전문을 복사하기보다 협회 자체 요약, 제목, 출처, 원문 링크 중심으로 운영하는 것을 권장합니다.
