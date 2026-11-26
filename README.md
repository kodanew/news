# KODA 일일동향 뉴스 포털

## 이번 수정본의 주요 변경
- 구글 시트를 원본 데이터로 사용하도록 GitHub Actions 자동 동기화 추가
- 브라우저에서 Google CSV를 직접 읽지 못하는 CORS 문제를 피하도록 GitHub가 15분마다 CSV를 내려받아 `data/sheet.csv`로 저장
- 첫 화면은 가장 최근 날짜 하루의 기사만 표시
- 날짜 선택 메뉴를 상단과 기사 목록 하단에 모두 배치
- 날짜는 최신순 5개씩 표시하고 좌우 화살표로 이전/다음 날짜 묶음 이동
- 날짜 선택 시 해당 날짜의 기사만 표시
- 대표 기사는 시트 C열에 이미지 주소가 있고 E열에 제목이 있을 때만 표시
- 대표 이미지 클릭 및 제목 클릭은 D열 링크로 이동
- 회원사 소식(초록), 정책 및 부동산개발업계 동향(파랑), 기타 소식(금색) 구분
- 뉴스 제목 자체를 원문 링크로 연결

## Google Sheets 열 순서
| 열 | 내용 |
|---|---|
| A | 날짜 |
| B | 일일동향보고 제목 |
| C | 대표 기사 썸네일 이미지 주소 |
| D | 대표 기사 클릭 링크 |
| E | 대표 기사 한글 제목 |
| F | 회원사 소식 |
| G | 정책 및 부동산개발업계 동향 |
| H | 기타 소식 |
| I~K | 대표 기사 한글 제목(추가 지정용) |

C열 이미지는 외부에서 접근 가능한 이미지 URL 또는 공유 권한이 '링크가 있는 모든 사용자-뷰어'인 Google Drive 파일 주소를 사용하세요. 셀 위에 겹쳐 놓은 이미지(셀 안에 URL이 없는 이미지)는 CSV로 전달되지 않을 수 있습니다.

## GitHub에 올리는 방법
1. 압축을 풀고 `koda-daily-news` 폴더 안의 파일과 `.github` 폴더를 모두 저장소 최상위(root)에 업로드합니다.
2. 기존 파일은 수정본으로 덮어씁니다. `index.html`, `app.js`, `style.css`, `news.json`, `admin.html`, 로고 파일을 포함해 폴더 구조를 그대로 유지합니다.
3. GitHub 저장소의 Settings → Actions → General에서 Workflow permissions가 제한되어 있다면 `Read and write permissions`를 선택하고 저장합니다. workflow 파일에 `contents: write` 권한도 지정되어 있습니다.
4. 저장소 Actions 탭 → `Sync Google Sheet CSV` → `Run workflow`를 한 번 실행합니다.
5. 실행이 성공하면 `data/sheet.csv`가 생성/갱신됩니다. 이후 15분마다 자동 실행됩니다.
6. GitHub Pages는 기존과 동일하게 main 브랜치의 /(root)에서 배포합니다.

## 확인 방법
- Actions의 `Sync Google Sheet CSV` 실행이 초록색 완료 상태인지 확인
- 저장소의 `data/sheet.csv` 파일에 최신 행이 있는지 확인
- 웹사이트에서 강력 새로고침(Ctrl+F5) 실행
- 상단 상태가 `Google Sheets 자동 동기화 자료`로 표시되는지 확인

## 관리자 페이지 안내
GitHub Pages는 정적 사이트이므로 `admin.html`에서 입력한 내용이 Google Sheets에 직접 기록되지는 않습니다. 직원들은 Google Sheets에 직접 입력하면 됩니다. 이 수정본은 Google Sheets → GitHub 자동 동기화 → 공개 웹사이트 순서로 자료를 표시합니다.
