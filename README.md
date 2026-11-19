코덕 체험단 모음 사이트

- `index.html` — 화면. 목록은 `data.json`을 `fetch('./data.json?v=' + Date.now())`로 불러와 그립니다. (D-day는 한국 시간 자정 기준 자동 계산)
- `data.json` — 체험단 데이터. 매일 오전 9시 30분 자동 업데이트가 이 파일만 고쳐서 커밋·푸시합니다.

## data.json 형식

```json
{
  "updated": "2026-11-19",
  "items": [
    {
      "id": "bbia-x",
      "brand": "삐아",
      "handle": "@bbia_official",
      "platform": "x",                 // instagram | x | powderroom | glowpick
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
  ]
}
```

`codek-tester/data.json`·`codek-tester/index.html`은 같은 내용의 사본입니다.
