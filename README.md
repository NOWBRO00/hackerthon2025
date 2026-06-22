# SEOSANCHECK (서산책)

서산책(SEOSANCHECK)은 충청남도 서산의 관광지, 음식, 특산품, 축제, 아라메길 정보를 한곳에서 둘러보고 AI 추천 여행 코스를 생성할 수 있는 React 기반 관광 웹 애플리케이션입니다.

> 패키지명은 `hackerthon2025`이며, 서비스명은 UI와 문서에서 `SEOSANCHECK` 또는 `서산책`으로 사용합니다.

## 주요 기능

- 서산 날씨와 추천 관광 콘텐츠를 보여주는 홈 화면
- 서산9경, 서산9미, 서산9품, 페스티벌, 아라메길 콘텐츠 탐색
- 관광지와 업소 통합 검색
- 테마와 자유 입력을 기반으로 한 AI 여행 코스 추천
- 추천 코스 목록/상세 화면과 코스 다시보기
- Kakao Map 기반 코스 지도와 이동 수단별 예상 거리/시간 표시
- Naver Map 기반 관광지/업소 위치 확인

## 기술 스택

| 구분 | 내용 |
| --- | --- |
| Framework | React 18, Create React App |
| Language | JavaScript, JSX, CSS |
| Routing | react-router-dom v6 |
| HTTP Client | axios |
| UI | framer-motion, react-icons, react-toastify |
| Maps | Kakao Maps, Naver Maps, SK T Map |
| Deploy | Firebase Hosting |
| Runtime | Node.js 18 |
| Container | Docker, Docker Compose |

## 시작하기

### 사전 준비

- Node.js 18 이상
- npm
- 프론트엔드에서 호출할 백엔드 API 서버
- Kakao Maps API 키
- Naver Maps, SK T Map 사용을 위한 클라이언트 키

### 설치 및 실행

```bash
npm install
```

`.env.local` 파일을 생성하고 필요한 환경 변수를 설정합니다.

```bash
REACT_APP_API_URL=http://localhost:8080
REACT_APP_KAKAO_MAP_API_KEY=your_kakao_map_api_key
```

개발 서버를 실행합니다.

```bash
npm start
```

기본적으로 Create React App 개발 서버가 `http://localhost:3000`에서 실행됩니다.

## 환경 변수

| 변수명 | 설명 | 사용 위치 |
| --- | --- | --- |
| `REACT_APP_API_URL` | 백엔드 API의 base URL | `src/API/axios.js` |
| `REACT_APP_KAKAO_MAP_API_KEY` | Kakao Maps JavaScript SDK 키 | `src/COMPONENTS/AI/MapContainer.jsx` |

Naver Maps와 SK T Map 스크립트는 현재 `public/index.html`에서 로드됩니다. 운영 환경에서는 공개 저장소에 키가 노출되지 않도록 환경 변수 또는 별도 키 관리 방식으로 분리하는 것을 권장합니다.

## 사용 가능한 스크립트

```bash
npm start
```

개발 서버를 실행합니다.

```bash
npm run build
```

프로덕션 배포용 정적 파일을 `build/` 디렉터리에 생성합니다.

```bash
npm test
```

Jest와 React Testing Library 기반 테스트를 실행합니다. Create React App 기본 설정에 따라 watch 모드로 동작할 수 있습니다.

```bash
npm run eject
```

Create React App 설정을 프로젝트로 꺼냅니다. 되돌릴 수 없는 작업이므로 필요한 경우에만 사용하세요.

## Docker로 실행하기

개발 환경은 `Dockerfile.dev`와 `docker-compose.yml`을 사용할 수 있습니다.

```bash
docker compose up --build
```

컨테이너 내부에서 CRA 개발 서버가 `0.0.0.0:3000`으로 실행되며, 로컬 소스가 `/app`에 마운트되어 핫 리로드가 동작합니다.

## Firebase Hosting 배포

Firebase Hosting 설정은 `firebase.json`과 `.firebaserc`에 포함되어 있습니다.

- Firebase 프로젝트: `seosancheck`
- 배포 대상 디렉터리: `build/`
- SPA 라우팅을 위해 모든 요청을 `/index.html`로 rewrite

배포 예시는 다음과 같습니다.

```bash
npm run build
firebase deploy --only hosting
```

## 프로젝트 구조

```text
src/
├── API/
│   └── axios.js              # API 클라이언트 설정
├── COMPONENTS/
│   ├── AI/                   # AI 코스 목록, 상세, 지도 화면
│   ├── COMMON/               # Header, Footer, Drawer, Alert 등 공통 컴포넌트
│   ├── HOME/                 # 홈, 날씨, 서산9경/9미/9품, 축제, 아라메길
│   ├── MAPS/                 # Naver Map, T Map 래퍼
│   ├── PLACE/                # 관광지/업소 상세 화면
│   └── STEPS/                # AI 추천 코스 생성 단계 화면
├── CSS/                      # 화면별 스타일
├── IMAGE/                    # SVG 및 이미지 에셋
├── App.js
├── Router.jsx                # 라우팅 정의
└── index.js                  # React 앱 진입점
```

## 주요 라우트

| 경로 | 설명 |
| --- | --- |
| `/` | 홈 화면 |
| `/recommend` | AI 추천 코스 생성 단계 |
| `/ai-course` | AI 추천 코스 목록 |
| `/ai-course/:id` | AI 추천 코스 상세 |
| `/map` | 추천 코스 지도 |
| `/place/:id` | 관광지 상세 |
| `/store/:id` | 업소 상세 |
| `/9kyung` | 서산9경 |
| `/9mi` | 서산9미 |
| `/9pum` | 서산9품 |
| `/festival` | 서산 페스티벌 |
| `/aramegil` | 서산 아라메길 |

## 백엔드 API 의존성

이 저장소는 프론트엔드 애플리케이션만 포함합니다. 다음 API는 `REACT_APP_API_URL`로 설정된 백엔드 서버에서 제공되어야 합니다.

| Method | Endpoint | 사용 목적 |
| --- | --- | --- |
| GET | `/tourist-places` | 관광지 목록 검색 |
| GET | `/tourist-places/:id` | 관광지 상세 |
| GET | `/store` | 업소 목록 검색 |
| GET | `/store/:id` | 업소 상세 |
| GET | `/weather/seosan` | 서산 날씨 정보 |
| GET | `/ai/travel-plans?area=&text=` | AI 여행 코스 추천 |

AI 추천 코스 응답은 브라우저 `localStorage`의 `aiCourses`에 저장된 뒤 `/ai-course`와 `/ai-course/:id` 화면에서 사용됩니다.

## 참고 사항

- `.env*` 파일은 `.gitignore`에 포함되어 있으므로 로컬 환경 변수는 커밋되지 않습니다.
- 지도, 날씨, AI 추천 기능은 외부 API와 백엔드 응답 형식에 의존합니다.
- `firebase`와 `zustand` 패키지는 `package.json`에 포함되어 있지만 현재 주요 화면 코드에서는 직접 사용되지 않습니다.
- 기본 CRA 테스트나 메타데이터가 현재 UI와 다를 수 있으므로, 화면 변경 시 테스트와 manifest 정보를 함께 점검하는 것을 권장합니다.
