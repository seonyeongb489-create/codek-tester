코덕 체험단 · 이벤트 모음 사이트

- `index.html` — 화면. 목록은 `data.json`을 `fetch('./data.json?v=' + Date.now())`로 불러와 그립니다. (D-day는 한국 시간 자정 기준 자동 계산)
- `data.json` — 체험단(`items`)과 이벤트(`events`) 데이터. 매일 11:00 / 16:00 / 21:00 자동 업데이트가 이 파일을 고쳐서 커밋·푸시합니다.
- 상단 `체험단 / 이벤트` 전환 탭을 누르면 `items`와 `events` 목록이 각각 그려집니다. 딥링크는 `#tester`, `#events`.

## 이벤트 탭(`events`) 수록 규칙

**이벤트 탭(`events`)은 구매 조건이나 사전 리뷰 실적 조건이 없는 무료 응모형(댓글·팔로우·RT·방문 인증)만 포함한다.**

- 제품 구매가 조건이거나, 정해진 리뷰 개수·리뷰 작성 실적이 있어야 응모되는 이벤트(예: 올리브영 '구매 후 리뷰', 글로우픽 '리뷰 N개 작성 후 응모')는 `events`에 넣지 않는다.
- 같은 이유로 조건이 붙은 이벤트는 2026-11-20 사용자 선택으로 `ev-hince-glit-oy`·`ev-banila-malcha-oy`·`ev-athe-ezni-oy`·`ev-glowpick-movie`·`ev-glowpick-weekend` 5건을 제외했고, 이후 자동 업데이트에서도 다시 넣지 않는다.
- 리뷰 의무가 있는 체험단은 원래대로 `items` 쪽에만 올린다.

## data.json 형식

```json
{
  "updated": "2026-11-20",
  "items": [
    {
      "id": "bbia-x",
      "brand": "삐아",
      "handle": "@bbia_official",
      "platform": "x",                 // instagram | x | powderroom | glowpick | musinsa | stylec | oliveyoung
      "category": "lip",               // lip | skin | hair | fragrance | multi
      "product": "라스트 오토 젤 아이라이너 + 미출시 젤 섀도우",
      "start": "2026-11-17",           // 없으면 null
      "end": "2026-11-19",             // 마감일 (필수)
      "announce": null,                // 발표일, 모르면 null → '발표 미정'
      "winners": 60,                   // 숫자 또는 "15명 이상", 모르면 null → '인원 미정'
      "keywords": ["팔로우", "구글폼"],  // 참여 방법 짧은 키워드
      "origin": "https://x.com/bbia_official",
      "apply": { "url": "https://forms.gle/..." },  // 원문에서 바로 신청하는 공고는 origin과 같은 URL
      "listed": "2026-11-17"           // 사이트에 올린 날
    }
  ],
  "events": [
    {
      "id": "ev-laka-seongsu",
      "brand": "라카",
      "handle": "@laka.official",
      "platform": "instagram",         // items와 동일한 값 사용 (oliveyoung 포함)
      "category": "lip",
      "kind": "visit",                 // comment(댓글) | visit(방문·오프라인 인증) | gift(무료 증정) — review(구매 후 리뷰)는 수록하지 않음
      "product": "성수 플래그십 오픈 — 방문 인증 추첨 (키스프루프 글로스 8색 세트 + 원통 파우치)",
      "start": "2026-11-19",
      "end": "2026-12-02",
      "announce": null,
      "winners": 5,                    // '전원'/'선착순' 문자열도 가능 → '전원 증정'으로 표시
      "keywords": ["성수 방문", "SNS 인증", "방문 증정"],
      "origin": "https://www.instagram.com/laka.official/",
      "apply": { "url": "https://www.instagram.com/laka.official/" },
      "listed": "2026-11-20"
    }
  ]
}
```

### 규칙
- `items`는 **리뷰·후기 의무가 있는 체험단**, `events`는 **구매·리뷰 실적 조건이 없는 무료 응모형 브랜드 이벤트(댓글·팔로우·RT·방문 인증·증정)**입니다. 두 배열은 서로 독립이라 체험단 자동 업데이트 스크립트가 `items`만 고쳐도 이벤트가 깨지지 않습니다.
- 이벤트 카드의 인원 표기는 `events`에서 `N명 추첨`, `전원 증정`, `인원 미정`으로 자동 변환됩니다.
- `end`는 필수, `start`·`announce`·`handle`·`winners`는 모르면 `null`.
- 마감일이 지난 항목은 사이트에서 자동으로 '마감' 처리되고 목록 맨 뒤로 정렬됩니다. 3일 이상 지난 항목은 자동 업데이트 때 정리합니다.
- `platform` 값이 처음 보는 것이면 상단 출처 탭에 자동으로 나타납니다(0건이면 숨김). 새 출처를 쓰려면 `index.html`의 `PLATFORM`·`.src` 색상만 추가하면 됩니다.

`codek-tester/data.json`·`codek-tester/index.html`은 같은 내용의 사본입니다.

## 출처(platform) 값

- `instagram`·`x`·`powderroom`·`glowpick`·`oliveyoung` — 기존 수집 루틴이 채우는 출처.
- `musinsa` — 무신사 프리유저 체험단(`https://www.musinsa.com/preuser/events/{eventId}`). 2026-11-22 수동 등록.
- `stylec` — 스타일씨 제공형 캠페인(`https://www.stylec.co.kr/trials/{wr_id}`). 2026-11-22 수동 등록.
- 출처 탭은 `index.html`의 `#tabs` 버튼과 `PLATFORM`·`counts`·`.src.<platform>` 색상을 함께 추가해야 보입니다.
