# 🛒 한국마트 전단지 관리 시스템

코드 수정 없이 **관리자 웹페이지**에서 상품을 추가/수정/삭제하면, **GitHub Pages 전단지에 즉시 반영**되는 무료 시스템입니다.

---

## 📁 파일 구성

| 파일 | 역할 |
|---|---|
| `index.html` | 손님이 보는 전단지 페이지 (디자인 그대로, 데이터만 동적으로 불러옴) |
| `products.json` | 상품 데이터 (이름·가격·이미지·뱃지). **이 파일만 수정하면 됨** |
| `admin.html` | 본인이 사용할 관리자 페이지 (폼으로 편집 → GitHub에 자동 커밋) |
| `README.md` | 이 안내서 |

---

## 🚀 첫 설정 (한 번만)

### 1단계. 기존 저장소에 파일 업로드
기존 `gang7369-lgtm/jmart` 저장소에 위 4개 파일을 모두 업로드합니다 (또는 기존 `index.html`을 새 버전으로 덮어쓰기).

### 2단계. GitHub Personal Access Token 발급
1. <https://github.com/settings/tokens/new?scopes=repo&description=jmart-flyer-admin> 접속
2. **Note**: `jmart-flyer-admin` (이미 채워져 있음)
3. **Expiration**: 원하는 기간 (`No expiration` 가능하나 보안상 90일 권장)
4. **scopes**: `repo` 체크 (이미 체크되어 있음)
5. 맨 아래 **Generate token** 클릭
6. 표시된 `ghp_...` 토큰을 복사 (이 화면을 벗어나면 다시 못 봅니다)

### 3단계. 관리자 페이지 접속 및 설정
1. `https://gang7369-lgtm.github.io/jmart/admin.html` 접속 (또는 로컬에서 `admin.html` 열기)
2. 상단 **🔧 GitHub 연결 설정** 펼치기
3. 다음 입력:
   - 사용자명: `gang7369-lgtm`
   - 저장소 이름: `jmart`
   - 브랜치: `main` (또는 사용 중인 브랜치)
   - products.json 경로: `products.json`
   - Personal Access Token: 위에서 복사한 `ghp_...`
4. **[설정 저장]** 클릭 → **[연결 테스트]** 클릭 → ✅ 표시 확인
5. **[GitHub에서 데이터 불러오기]** 클릭하면 현재 상품 목록이 화면에 나타남

> 토큰은 **본인 브라우저의 localStorage에만 저장**됩니다. 서버로 전송되지 않으며 GitHub API 호출 시에만 사용됩니다.

---

## 📝 일상 사용법

### 상품 수정/추가 (가장 흔한 작업)
1. `admin.html` 접속
2. 원하는 코너에서 **[수정]** 또는 **[+ 상품 추가]** 클릭
3. 폼 채우기 (이미지 URL 붙여넣으면 미리보기 표시)
4. **저장** → 화면에 반영됨 (이때까진 아직 GitHub 미반영)
5. 작업 끝나면 화면 맨 아래 **🚀 [GitHub에 저장 (즉시 배포)]** 클릭
6. 1~2분 후 `https://gang7369-lgtm.github.io/jmart/`에 자동 반영
7. 카카오톡으로 공유한 링크는 그대로 사용 (URL 변경 없음)

### 코너(카테고리) 추가
- **[+ 코너 추가]** 클릭 → 제목·탭이름·ID·레이아웃(그리드/리스트) 선택
- 새 코너 자동 생성 → 상품 추가하면 됨

### 매장/행사 정보 변경
- 화면 상단 **매장/행사 정보** 카드에서 직접 입력 → **GitHub에 저장**

### 순서 바꾸기
- 각 상품/코너의 **↑ ↓** 버튼으로 순서 조정

---

## 🎨 뱃지 사용법

| 뱃지 종류 | 색 | 추천 용도 |
|---|---|---|
| `한정` | 빨강 | 한정 수량, 데-박, 쪼야요 등 |
| `NEW` | 초록 | 신상품, 신메뉴 |

**애니메이션:**
- `깜빡임` → 1초 단위로 깜빡 (눈길 끌기)
- `펄스` → 부드럽게 커졌다 작아짐
- `없음` → 정적

---

## 🔄 데이터 흐름

```
[admin.html에서 편집]
        ↓ (저장 클릭)
[GitHub API → products.json 커밋]
        ↓ (1-2분, GitHub Pages 자동 배포)
[index.html이 products.json fetch]
        ↓
[손님 화면에 반영] ✨
```

---

## 💡 백업과 복구

- **JSON 다운로드** 버튼 → 현재 데이터를 `products.json`으로 다운로드
- **JSON 가져오기** 버튼 → 백업 파일을 다시 로드
- 추천: 큰 변경 전에 한 번씩 다운로드해두기

---

## ❓ 자주 발생하는 문제

**Q. "저장 실패: Bad credentials"**
→ 토큰이 만료됐거나 잘못 입력됨. 새 토큰 발급해서 재등록.

**Q. "저장 실패: Resource not accessible by personal access token"**
→ 토큰 발급 시 `repo` 권한을 체크하지 않음. 새로 발급할 것.

**Q. 저장 후에도 전단지가 안 바뀜**
→ GitHub Pages 배포에 1~2분 걸립니다. 새로고침은 강제 새로고침(`Ctrl+Shift+R`).

**Q. 다른 PC에서 admin.html 쓰려면?**
→ 토큰만 다시 한 번 입력하면 됨 (브라우저별로 저장).

**Q. 토큰 노출이 걱정되면?**
→ admin.html을 GitHub Pages에 올리지 말고 로컬(컴퓨터)에서만 열어 사용. `index.html`과 `products.json`만 GitHub에 올리면 됨.

---

## 🔧 향후 확장 아이디어

- 행사기간 자동 카운트다운 (D-2 표시)
- 이미지 자동 리사이즈 (Cloudflare Images / Imgur 업로드)
- 상품을 구글 시트에서 동기화 (현재는 admin.html 단독 사용)
- 카카오톡 공유 OG 이미지 자동 생성
- 다국어 (한/중) 자동 번역 토글

필요할 때 말씀하시면 추가 기능 만들어드릴 수 있어요.
