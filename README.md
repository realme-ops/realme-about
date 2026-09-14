# 리얼미 소개 페이지 (about.real-me.co.kr)

AI 검색엔진과 검색 크롤러가 리얼미를 정확히 읽어가도록 만든 **사실 정리 페이지**다.
사람을 설득하는 랜딩이 아니다. 주 독자는 챗GPT·퍼플렉시티·구글·네이버의 봇이다.

- 정식 주소: https://about.real-me.co.kr/ (DNS CNAME `about` → `realme-ops.github.io`)
- 임시 주소: https://realme-ops.github.io/realme-about/
- 최초 배포: 2026-09-14

## 왜 만들었나

2026-09-14 진단에서 확인한 사실:

- 홈(real-me.co.kr, 아임웹)은 아임웹 플랫폼 정책으로 **GPTBot·ChatGPT-User가 403 차단**된다. 사이트별 예외는 불가(아임웹 공식 답변). robots.txt 문제가 아니라 웹방화벽 단계다.
- 그래서 챗GPT는 홈의 FAQ·가격·예약제 안내를 읽지 못한다. 실제로 챗GPT에서 리얼미를 알고 **예약 없이 매장에 바로 온 고객**이 있었다.
- 깃허브 페이지로 배포한 서브도메인(impact-me, find-me, premium, change-me)은 GPTBot·ChatGPT-User·ClaudeBot 모두 200이다.

→ AI가 읽어야 하는 브랜드 정보를 깃허브 서브도메인에 따로 두기로 했다.

## 무엇이 들어 있나

| 파일 | 역할 |
|---|---|
| `index.html` | 본문. 서비스 정의 → 기본 정보 → 플랜·가격 → 다른 서비스와의 차이 → FAQ 12 → 쇼룸 위치 → 칼럼 12 → 예약. 구조화 데이터(Organization·AboutPage·LocalBusiness×2·FAQPage) 포함 |
| `llms.txt` | AI용 사이트 안내서. 홈의 llms.txt와 같은 내용 + 이 페이지 링크 |
| `robots.txt` | AI 크롤러(OpenAI·Anthropic·Perplexity·Google-Extended·Bing·Yeti) 전부 허용 |
| `sitemap.xml` | 단일 URL |
| `assets/realme_logo_ink.png` | 오피셜 워드마크(밝은 배경용). 재조판 금지 |

## 작성 원칙

1. **홈 FAQ와 글자까지 동일하게.** 가격·시간·주소·예약제 문장은 real-me.co.kr 자주 묻는 질문에서 그대로 가져온다. 화면과 다른 말을 하는 페이지는 AI가 신뢰 판정에서 감점한다.
2. **사이트에 없는 사실은 넣지 않는다.** 영업시간·전화번호·구로 우편번호가 비어 있는 이유다. 홈에 먼저 적고, 그 다음 여기에 옮긴다.
3. **문장은 혼자 서 있게.** 주어 + 수치 + 조건이 한 문장 안에 있어야 문단째로 인용된다.
4. **비교표의 "쇼핑 동행"은 리얼미 서비스가 아니다.** 홈 FAQ 7번 "사진촬영, 쇼핑동행 서비스와 어떻게 다른가요?"와 같은 구조로, "그 서비스는 이렇고 리얼미는 이렇다"를 답하기 위한 비교 대상이다. 지우지 말 것.
5. 브랜드 컬러(ink `#494540` · paper `#F7F5F4` · champagne `#DCC9A6`)와 워드마크만 쓴다. 광고 랜딩 톤은 쓰지 않는다.

## 가격·플랜이 바뀌면

세 곳을 같은 날 함께 고친다. 하나만 고치면 AI가 낡은 쪽을 "사실"로 학습한다.

1. 홈 FAQ (아임웹)
2. 홈 llms.txt (아임웹 SEO 설정) — `>`와 `"`는 HTML 코드로 바뀌므로 쓰지 않는다
3. 이 저장소 `index.html`(FAQ 본문 + FAQPage 스키마 + 플랜 표) 과 `llms.txt`

고친 뒤 `index.html`의 `dateModified`와 하단 "최종 갱신" 날짜를 올린다.

## 예약 버튼의 귀속

예약 링크는 홈과 같은 타입폼(REAL-ME)으로 가고 `utm_source=about&landing=about&cta=about_*`가 붙는다.
리드 시트에는 about으로 찍히지만, 타입폼 끝의 예약 페이지 링크가 홈 전용(`source=realme_home`)으로 고정돼 있어 **예약 알림 라벨은 홈으로 잡힌다.** about 유입을 따로 세야 하면 타입폼을 복제한다.

## 배포

`main` 브랜치 루트를 GitHub Pages로 서빙한다. 커밋하면 1분 안에 반영된다.
푸시는 realme-ops 계정 자격으로 한다(로컬 git 자격 증명이 다른 계정일 수 있음):

```bash
git -c credential.helper= -c 'credential.helper=!gh auth git-credential' push origin main
```

## 측정

- 기준선(2026-06-14~09-12, GA4): chatgpt.com 리퍼럴 12세션(7월 3 · 8월 6 · 9월 3)
- 재측정 2026-09-28: GPTBot·ChatGPT-User·ClaudeBot curl 200 확인, GA4 chatgpt 세션, 챗GPT 임시채팅 질문 10개에서 리얼미 언급·링크 여부
