# 한 문장 규칙과 채점되는 실습이 디자인 감각을 만든다

이 웹앱이 가르칠 내용은 52개 개념으로 정리되고, 각 개념은 한 문장 규칙 하나와 코드로 판정할 수 있는 기준 하나로 줄어든다. 그중 진짜 표준은 **WCAG 성공 기준 일곱 개**(글자 대비 4.5:1·3:1, 강화 대비 7:1, 비텍스트 대비 3:1, 색만으로 의미 전달 금지, 터치 영역 24px, 강화 터치 영역 44px, 텍스트 간격 재정의 내성)뿐이다. 8px 간격 눈금, 한글 행간 1.5–1.6, 아이콘 선 2px, 60-30-10 같은 나머지는 전부 플랫폼 가이드이거나 실무 관례이므로 앱 문구는 "규칙"이 아니라 "권장"이라고 써야 한다. 실습 형식은 정답이 하나이고 변수 하나만 바꾼 문제에는 둘 중 고르기와 다른 것 찾기를, 정답이 연속값인 문제에는 슬라이더 조절을, 정답이 위치인 문제에는 끌어서 맞추기를 쓰고, 뒤의 둘은 목표값과의 거리로 채점한 뒤 정답을 겹쳐 보여 준다. 순서는 정렬 → 간격 → 색 기초(지각·대비) → 위계 → 타이포그래피 → 색 구성 → 아이콘·형태 → 무게·균형·광학 보정의 8단계가 조사한 커리큘럼들과 가장 잘 맞고, 뒤로 갈수록 정답의 객관성이 낮아지므로 허용 범위를 넓혀야 한다. 한 레슨 안에서는 "대조 쌍 제시 → 학습자 선택 → 한 문장 설명" 순서가 설명을 먼저 주는 것보다 근거가 강하고, 새 개념은 처음 몇 문제만 묶어서 낸 뒤 이전 개념과 섞어 복습시키는 것이 장기 기억에 유리하다. 한계도 분명하다. 형식과 개념의 짝짓기, 그리고 모든 채점 허용오차는 어떤 연구도 검증하지 않은 이 보고서의 제안이며, Apple HIG·Material 3·Refactoring UI 책 본문·Arnheim 원전·토스와 KRDS 공식 문서는 1차 출처를 열지 못해 2차 출처에 기댔다.

## 표준은 WCAG 일곱 항목뿐이고 나머지는 권장이다

이 앱의 신뢰도는 "이 답이 왜 정답인가"에 답할 수 있느냐에 달려 있다. 같은 형식의 선행 서비스인 Can't Unsee는 일부 정답이 규칙이 아니라 취향이라는 점, 자극이 iOS 스타일 하나뿐이라는 점, 왜 한쪽이 나은지 설명이 약하다는 점을 지적받았다 ([The Next Web](https://thenextweb.com/news/design-skills-cant-unsee-quiz), [Medium 게임 비평](https://medium.com/@jianingl/game-critique-blog-cant-unsee-7e748af41914)). 그래서 아래 표의 모든 수치에는 지위를 붙였다. **표준**은 W3C WCAG의 규범 기준이다. **플랫폼 가이드**는 Apple·Google·IBM·KRDS처럼 한 디자인 시스템 안에서만 구속력이 있는 값이다. **관례**는 저자나 실무 매체가 권하는 경험칙이다. **기하**는 계산으로 따라 나오는 값이고, **이론**은 Arnheim류의 지각 이론으로 측정 기준이 없다. 여기에 출처 접근 상태를 뜻하는 **2차**(1차 문서를 열지 못해 요약·미러·독자 노트에 의존)와 **미확인**(어떤 출처로도 확인하지 못함)을 덧붙였다.

지위는 채점 방식을 결정한다. 표준 위반은 오답으로 처리해도 방어할 수 있다. 대비 기준은 반올림이 허용되지 않아 흰 배경 위 `#777777`은 4.47:1로 4.5:1에 미달한다 ([WebAIM](https://webaim.org/articles/contrast/)). 관례는 "권장 범위 안/밖"으로 보여 주고 감점하는 편이 정직하다. 이론 영역은 넓은 허용 영역을 두고 정답 대신 비교 화면을 보여 줘야 한다. 순검정 `#000`을 피하라는 조언이 좋은 예다. 흰 배경 위 순검정은 21:1로 모든 WCAG 기준을 통과하므로 이것을 대비 오답으로 채점하면 틀린 것을 가르치게 된다 ([W3C SC 1.4.3](https://w3.org/WAI/WCAG20/Understanding/contrast-minimum)).

채점 허용오차에 대해서는 미리 밝혀 둔다. "몇 픽셀까지 정렬로 보는가"를 정한 권위 있는 출처는 없고, 조사한 게임 가운데 허용오차를 공개한 곳도 없다. 아래 표에서 **제안**이라고 표시한 허용 범위는 모두 이 조사에서 만든 설계값이며, 실제 사용자 응답 분포로 보정해야 한다.

## 기초 단계는 좌표와 휘도만으로 채점된다

정렬, 간격, 색 기초는 정답이 DOM 좌표와 색 값에서 바로 계산되므로 비디자이너가 가장 납득하기 쉬운 출발점이다. 정렬의 원리는 Robin Williams의 네 원칙(대비·반복·정렬·근접)에서 나오는데, 원서를 직접 읽지 못해 블로그 요약에 의존했다 ([Wiredcraft](https://wiredcraft.com/blog/robin-williams-four-basic-design-principles-for-non-designers/)). 간격에서 가장 강력한 도구는 근접성이다. NN/g는 근접성이 색이나 모양의 유사성보다 강하게 묶음을 만든다고 설명한다 ([NN/g](https://www.nngroup.com/articles/gestalt-proximity/)). 간격 눈금은 서로 독립적인 세 계통(Refactoring UI, KRDS, 토스 추정값)이 4·8·16·24·32·48·64로 수렴하므로 **4·8·12·16·24·32·48·64px**를 초보자용 눈금으로 가르쳐도 무리가 없다. 다만 세 계통 모두 2차 출처다.

한 가지 충돌이 있다. W3C 한국어 조판 요구사항은 한글 본문의 기본을 양끝 맞춤으로 기술하지만 이는 인쇄·워드프로세서 관행이고 ([W3C klreq](https://w3c.github.io/klreq/new)), 화면 UI를 다루는 국내 자료는 왼쪽 정렬을 기본으로 두고 양끝 맞춤을 금한다 ([KRAFTON 브랜드 가이드](https://brand.krafton.com/ko/Typograhpy)). 앱은 화면 UI 훈련이므로 왼쪽 정렬을 정답으로 삼되 "화면 기준 권장"이라고 표기하면 된다.

**표 1. 정렬·간격 (1–2단계)**

| 개념 | 한 문장 규칙 | 수치 기준과 지위 | 실습 형식 → 코드 채점 기준 | 출처 |
|---|---|---|---|---|
| 공유선 정렬 | 모든 요소는 이웃 요소와 가장자리 선 하나를 공유해야 한다. | 수치 없음. 관례(Williams, 2차). 허용오차 0–1px 통과, 2–4px "거의"는 제안 | 끌어서 맞추기: 어긋난 요소를 기준선에 놓기 → 왼쪽 x좌표 차이 ≤ 1px. 다른 것 찾기: 왼쪽 x가 다른 요소 탭 | [Wiredcraft](https://wiredcraft.com/blog/robin-williams-four-basic-design-principles-for-non-designers/) |
| 왼쪽 대 가운데 | 긴 글은 왼쪽 정렬하고 가운데 정렬은 짧은 글에만 쓴다. | 가운데 정렬은 3–4줄 이하, 5줄 이상은 왼쪽. 관례(국내 실무 매체) | 둘 중 고르기 → 가운데 정렬 블록의 줄 수가 5 이상이면 오답 | [요즘IT](https://yozm.wishket.com/magazine/detail/1017/), [Butterick](https://practicaltypography.com/summary-of-key-rules.html) |
| 베이스라인 정렬 | 크기가 다른 글자가 한 줄에 놓이면 세로 중앙이 아니라 베이스라인으로 맞춘다. | 수치 없음. 관례(Refactoring UI 독자 노트, 2차) | 끌어서 맞추기(세로) → 두 텍스트의 베이스라인 y 차이 ≤ 1px(제안) | [rjseymour66 노트](https://rjseymour66.github.io/webdev/refactoring-ui/) |
| 근접성 | 그룹 안 간격은 그룹 사이 간격보다 확실히 작아야 한다. | 출처에 비율 수치 없음. 관례(NN/g). "바깥 간격 ≥ 안쪽 간격의 1.5–2배"는 제안 | 끌어서 맞추기: 두 입력란 정중앙의 라벨을 주인 쪽으로 → max(안쪽 간격) < min(바깥 간격). 슬라이더: 제목 위 간격 > 아래 간격 | [NN/g 근접성](https://www.nngroup.com/articles/gestalt-proximity/) |
| 간격 눈금 | 간격은 미리 정한 눈금 값에서만 고른다. | 4·8·12·16·24·32·48·64px, 이웃 값은 약 25% 이상 차이. 관례(Refactoring UI, 2차). 8dp·4dp 그리드는 플랫폼 가이드(Material 1 보관본) | 슬라이더 → 값이 허용 집합에 속하는지. 다른 것 찾기: 패딩이 다른 카드 하나 → 같은 역할의 간격끼리 값 일치 | [rjseymour66 노트](https://rjseymour66.github.io/webdev/refactoring-ui/), [Material 1](https://m1.material.io/layout/metrics-keylines.html) |
| 테두리보다 여백 | 요소를 가를 때 선보다 여백과 배경 차이를 먼저 쓴다. | 수치 없음. 관례(저자가 직접 쓴 글) | 둘 중 고르기 → 테두리 요소 수가 적고 그룹 간격이 눈금 값인 쪽이 정답 | [Refactoring UI 저자 글](https://medium.com/refactoring-ui/40c736799886) |
| 그리드·최대 폭 | 블록 가장자리는 칼럼 선에 맞추고 본문 폭에는 상한을 둔다. | 데스크톱 12칼럼·모바일 4칼럼. 관례(NN/g). 모바일 화면 여백 16dp는 플랫폼 가이드(Material 1 보관본). 거터 폭 수치는 출처 없음 | 끌어서 맞추기 → 카드 좌우 가장자리가 칼럼 가장자리와 일치, 좌우 페이지 여백 동일 | [NN/g 그리드](https://nngroup.com/articles/using-grids-in-interface-designs), [Material 1](https://m1.material.io/layout/metrics-keylines.html) |
| 터치 영역 | 눌리는 영역은 보이는 아이콘보다 크게 잡는다. | 24×24 CSS px 이상은 표준(WCAG 2.2 SC 2.5.8, AA). 44×44는 표준(SC 2.5.5, AAA). 48×48dp와 타깃 간 8dp는 플랫폼 가이드(Google). Apple 44pt는 플랫폼 가이드(2차 미러) | 슬라이더 → 24 미만 실패, 24–43 최소 충족, 44 이상 권장. 인접 타깃 간격 ≥ 8 | [W3C SC 2.5.8](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html), [Google 접근성 도움말](https://support.google.com/accessibility/android/answer/7101858), [Apple HIG 미러](https://unpkg.com/apple-hig-mcp@1.1.3/content/accessibility.md) |

색은 두 덩어리로 나뉜다. 표 2의 앞 다섯 행(세 다이얼, 지각 밝기, 대비 두 종류, 색만으로 말하지 않기)은 수식으로 판정되는 기초이고, 나머지 여덟 행은 팔레트 구성이라 타이포그래피 뒤에 두는 편이 낫다. 대비 계산은 W3C 기법 문서에 그대로 구현할 수 있는 형태로 나와 있다. 각 채널을 `c = 값/255`로 정규화하고, `c ≤ 0.04045`이면 `c/12.92`, 아니면 `((c + 0.055)/1.055)^2.4`로 선형화한 뒤 `L = 0.2126R + 0.7152G + 0.0722B`를 구하고, 대비는 `(밝은 L + 0.05)/(어두운 L + 0.05)`다 ([W3C G18](https://www.w3.org/WAI/WCAG22/Techniques/general/G18.html)). 이 공식으로 조사 중 계산한 흰 배경 기준 앵커는 `#767676` 4.54:1(AA 통과 최저 회색), `#949494` 3.03:1(3:1 통과 최저), `#595959` 약 7.0:1(AAA 통과 최저)이며, 흰 글자는 `#3B82F6` 위에서 3.68:1로 작은 글자 기준에 미달하고 `#2563EB` 위에서 5.17:1로 통과한다. 이 값들은 출처 인용이 아니라 계산값이므로 정답 키로 쓰되 배포 전 자체 구현으로 한 번 더 검산해야 한다.

HSL 명도가 지각 밝기가 아니라는 점은 숫자 하나로 설득된다. 채도 100%·명도 50%에서 노랑의 상대 휘도는 0.928, 파랑은 0.072로 약 13배 차이가 난다(같은 공식의 계산값). 그래서 파랑 위에서 통하던 흰 글자가 노랑 위에서는 1.07:1로 사라진다. OKLCH는 L과 C를 고정하고 H만 돌리면 지각 밝기가 비슷한 색군이 나오도록 설계됐다 ([Evil Martians](https://evilmartians.com/chronicles/oklch-in-css-why-quit-rgb-hsl)). 초급 조작기는 HSL, 고급 조작기는 OKLCH로 두는 구성이 자연스럽다. APCA는 2023년 7월 WCAG 3 초안에서 빠졌고 2026년 4월 편집자 초안도 대비 알고리즘을 미정으로 두고 있으므로 ([Adrian Roselli](https://adrianroselli.com/2026/04/wcag3-contrast-as-of-april-2026.html)), 합격 판정은 WCAG 2로 하고 APCA는 참고 수치로만 보여 주는 것이 맞다.

**표 2. 색 (3단계: 앞 다섯 행, 6단계: 나머지)**

| 개념 | 한 문장 규칙 | 수치 기준과 지위 | 실습 형식 → 코드 채점 기준 | 출처 |
|---|---|---|---|---|
| 색의 세 다이얼 | 색은 헥스 코드가 아니라 색상·채도·명도 세 값으로 고친다. | HSL은 H 0–360, S·L 0–100%. OKLCH는 L 0–1, C 0–약 0.37, H 0–360. 색 공간 정의(업체 기술 글) | 슬라이더: 목표 색 맞추기 → 목표와의 H·S·L 차이(허용 범위는 제안) | [Evil Martians](https://evilmartians.com/chronicles/oklch-in-css-why-quit-rgb-hsl) |
| HSL 명도의 함정 | HSL 명도가 같아도 눈에 보이는 밝기는 같지 않다. | S100·L50에서 노랑 휘도 0.928, 파랑 0.072. W3C 공식 계산값 | 끌어서 맞추기(순서): 색 조각을 밝은 순으로 배열 → 상대 휘도 순서와 일치 | [W3C G18](https://www.w3.org/WAI/WCAG22/Techniques/general/G18.html), [Evil Martians](https://evilmartians.com/chronicles/oklch-in-css-why-quit-rgb-hsl) |
| 글자 대비 | 본문 글자는 배경과 4.5:1 이상 대비가 나야 한다. | 본문 4.5:1, 큰 글자(약 24px 이상 또는 굵은 약 18.5px 이상) 3:1은 표준(WCAG AA, SC 1.4.3). 7:1은 표준(AAA). 반올림 금지 | 슬라이더: 통과할 때까지 명도 조절 → G18 공식 비율을 반올림 없이 4.5·3·7과 비교 | [W3C SC 1.4.3](https://w3.org/WAI/WCAG20/Understanding/contrast-minimum), [WebAIM](https://webaim.org/articles/contrast/) |
| 비텍스트 대비 | 입력란 테두리·아이콘·포커스 링도 주변과 3:1 이상이어야 한다. | 3:1은 표준(WCAG 2.1 AA, SC 1.4.11). `#AAA` 테두리는 약 2.3:1로 미달 | 둘 중 고르기, 슬라이더 → 테두리색 대 인접색 ≥ 3 | [W3C SC 1.4.11](https://w3.org/WAI/WCAG22/Understanding/non-text-contrast) |
| 색만으로 말하지 않기 | 색 하나만으로 상태나 의미를 전달하지 않는다. | 표준(WCAG SC 1.4.1, Level A). 대안은 두 색 사이 3:1 이상 명도 대비. 적록 색각 이상은 남성 약 12명 중 1명, 여성 약 200명 중 1명(북유럽계 기준, 한국 수치 없음) | 다른 것 찾기 → 상태 요소에 아이콘·텍스트 형제 노드가 있는지, 또는 두 상태색 대비 ≥ 3 | [W3C SC 1.4.1](https://w3.org/WAI/WCAG22/Understanding/use-of-color.html), [MedlinePlus](https://medlineplus.gov/genetics/condition/color-vision-deficiency) |
| 60-30-10과 색 개수 | 화면 대부분은 중립색으로 두고 강조색은 조금만 쓴다. | 면적 60/30/10, 색은 세 가지 정도. 관례(조사한 권위 출처 중 NN/g만 수치 제시) | 둘 중 고르기, 슬라이더(면적) → 채도 기준으로 분류한 강조색 면적 5–15%(제안), 고채도 색상 군집 ≤ 3 | [NN/g 색](https://www.nngroup.com/articles/color-enhance-design/) |
| 강조색 한 자리 | 채운 강조색은 화면의 주 동작 하나에만 쓴다. | 화면당 채운 강조 컨트롤 1개. 플랫폼 가이드(Apple HIG의 툴바 예시) | 다른 것 찾기 → 강조색으로 채운 요소 수 = 1 | [Apple HIG 색](https://developer.apple.com/design/human-interface-guidelines/color.md) |
| 한 색 한 뜻 | 한 색은 모든 화면에서 한 가지 뜻만 갖는다. | 수치 없음. 플랫폼 가이드·관례 | 다른 것 찾기 → 역할 태그별 색 일치(빨강이 삭제와 할인에 함께 쓰이면 오답) | [Apple HIG 색](https://developer.apple.com/design/human-interface-guidelines/color.md), [NN/g 색](https://www.nngroup.com/articles/color-enhance-design/) |
| 조화 각도 | 색 조화는 기준 색상을 정해진 각도만큼 돌린 것이다. | 보색 180°, 유사색 ±30°, 삼색 120°, 분할보색 150°·210°, 사색 90° 간격. 관례(각도는 소프트웨어 라이브러리 문서 기준, NN/g는 120°만 확인) | 슬라이더(색상환) → 색상 차이(mod 360)가 목표 ±10–15°(제안). 어느 색상환인지 화면에 명시 | [Color.Harmony 문서](https://color.hexdocs.pm/Color.Harmony.html), [NN/g 색](https://www.nngroup.com/articles/color-enhance-design/) |
| 음영 눈금 | 색마다 음영 단계를 미리 정해 두고 그 안에서만 쓴다. | 회색 8–10단계, 색마다 5–10단계, 100–900의 9단계에서 500이 버튼 배경. 관례(저자 공개 챕터) | 끌어서 맞추기(순서) → 명도가 단조롭게 변하는지, 900 글자 대 100 배경 ≥ 4.5(제안) | [Refactoring UI 미리보기](https://www.refactoringui.com/previews/building-your-color-palette) |
| 음영의 채도·색상 보정 | 밝고 어두운 끝에서도 채도를 지키고 색상은 조금만 옮긴다. | 색상 이동은 최대 20–30°. 관례(Refactoring UI 독자 노트, 2차). 채도를 얼마나 올릴지는 수치 없음 | 슬라이더 → 양 끝 단계 채도 ≥ 중간 단계, 전체 색상 이동 ≤ 30° | [독자 노트](https://github-wiki-see.page/m/KeynesYouDigIt/Knowledge/wiki/Refactoring-UI) |
| 순검정·틴트 회색 | 순검정 대신 색기가 조금 도는 아주 어두운 회색을 쓴다. | 회색 채도는 밝은 쪽 2–3%에서 어두운 쪽 약 22%(한 회사 사례). 관례. 다크 표면 `#121212`는 2차(업체 블로그 경유). 접근성 기준이 아님 | 둘 중 고르기 → 스타일 점수로만 반영: `#000000` 사용, 채도 0 회색, 회색 간 색상 편차 ±10° 초과(제안) | [Ian Storm Taylor](https://ianstormtaylor.com/design-tip-never-use-black/), [Atmos](https://atmos.style/blog/dark-mode-ui-best-practices) |
| 색 위의 글자 | 색 배경 위에는 회색 글자 대신 배경과 같은 색상의 밝은 색을 쓴다. | 수치 없음. 관례(저자가 직접 쓴 글). 같은 색상 틴트도 4.5:1에 미달할 수 있음(`#BFDBFE`/`#2563EB` = 3.64:1, 계산값) | 둘 중 고르기 → 글자색 색상이 배경 색상과 일치하고 대비 기준도 통과 | [Refactoring UI 저자 글](https://medium.com/refactoring-ui/40c736799886), [W3C G18](https://www.w3.org/WAI/WCAG22/Techniques/general/G18.html) |

마지막 행은 문제 설계에서 조심할 지점이다. 같은 색상의 밝은 틴트는 회색보다 보기 좋지만 중간 톤 브랜드색 위에서는 작은 글자 기준을 넘지 못하는 경우가 많다. "보기 좋은 쪽"과 "표준을 통과하는 쪽"이 갈리는 문항은 두 판정을 따로 표시해야 한다.

## 위계와 타이포그래피는 개수 세기와 범위 판정으로 바뀐다

위계는 주관적으로 보이지만 대부분 개수로 환원된다. NN/g는 글자 크기를 세 단계 이하로, 큰 요소를 둘 이하로 제한하라고 권하고 ([NN/g](https://www.nngroup.com/articles/visual-hierarchy-ux-definition/)), Refactoring UI 저자들은 굵기 두 종과 글자색 두세 종으로 위계를 만들라고 권한다 ([Refactoring UI 저자 글](https://medium.com/refactoring-ui/40c736799886)). 따라서 화면 안의 서로 다른 `font-size`, `font-weight`, 글자색, 채운 버튼의 개수를 세면 채점이 된다. 다만 실제 디자인 시스템은 세 단계보다 많은 크기를 쓰므로 "3 이하"는 초보자용 연습 기준으로만 제시해야 한다. 스퀸트 테스트는 CSS `filter: blur()` 토글로 그대로 옮길 수 있고, NN/g 예시가 쓴 값이 5px·10px·20px이다.

타이포그래피에서는 라틴 문자 기준과 한글 기준을 구분해야 한다. Butterick의 행간 120–145%는 인쇄에 뿌리를 둔 라틴 기준이고 ([Butterick](https://practicaltypography.com/line-spacing.html)), 국내 자료는 한글 본문에 1.5–1.8, 그중에서도 1.5–1.6을 가장 자주 권한다 ([요즘IT](https://yozm.wishket.com/magazine/detail/1017/), [inthiswork](https://inthiswork.com/archives/250750)). 한글 행간이나 줄당 글자 수에 대한 표준 기구 권고나 동료 심사 연구는 찾지 못했고, 모든 수치가 실무 관례다. 자주 오해되는 것이 WCAG의 1.5다. SC 1.4.12는 사용자가 행간을 1.5배로 바꿔도 내용이 깨지지 않아야 한다는 요구이지, 제작자가 행간을 1.5로 설정하라는 요구가 아니다 ([W3C SC 1.4.12](https://www.w3.org/WAI/WCAG22/Understanding/text-spacing)). 자간도 마찬가지로 관례 영역이다. W3C 한국어 조판 문서와 정부 시스템 KRDS는 0을 기본으로 두고, 실무 매체는 살짝 좁히라고 권한다. 앱은 "0에서 아주 조금 좁히는 범위, 본문에 양수는 쓰지 않는다"로 가르치되 KRDS가 0을 쓴다는 사실을 함께 말해야 한다.

**표 3. 위계·타이포그래피 (4–5단계)**

| 개념 | 한 문장 규칙 | 수치 기준과 지위 | 실습 형식 → 코드 채점 기준 | 출처 |
|---|---|---|---|---|
| 단계 수 제한 | 글자 크기·굵기·색의 종류를 적게 유지한다. | 크기 3단계 이하(본문 14–16, 소제목 18–22, 제목 최대 32px). 관례(NN/g). 굵기 2종(400–500, 600–700), 글자색 2–3종. 관례(저자가 직접 쓴 글) | 다른 것 찾기, 둘 중 고르기 → 서로 다른 font-size ≤ 3, font-weight ≤ 2, 글자색 ≤ 3 | [NN/g 위계](https://www.nngroup.com/articles/visual-hierarchy-ux-definition/), [Refactoring UI 저자 글](https://medium.com/refactoring-ui/40c736799886) |
| 굵기와 색으로 위계 | 중요한 것을 키우기보다 덜 중요한 것을 흐리게 해서 위계를 만든다. | 수치 없음. 관례("덜 중요한 것을 낮춘다"는 책 요약, 2차). 차이는 어정쩡하지 않게(Williams, 2차) | 슬라이더: 보조 텍스트 색 농도 → 주 텍스트와 보조 텍스트의 배경 대비 차이가 생기되 보조도 4.5:1 유지. 둘 중 고르기 | [Refactoring UI 저자 글](https://medium.com/refactoring-ui/40c736799886), [sglavoie 요약](https://sglavoie-github-io.pages.dev/posts/2023/09/09/book-summary-refactoring-ui/) |
| 버튼 위계 | 주 동작만 채운 버튼으로 두고 나머지는 외곽선이나 링크로 낮춘다. | 화면당 채운 주 버튼 1개. 관례("화면당 하나"라는 문구는 출처에서 확인하지 못한 파생 관례) | 다른 것 찾기 → 채움 스타일 버튼 수 = 1 | [Refactoring UI 저자 글](https://medium.com/refactoring-ui/40c736799886) |
| 스퀸트 테스트 | 흐리게 봤을 때 먼저 보이는 것이 가장 중요한 것이어야 한다. | 블러 5·10·20px(NN/g 예시 값). 관례 | 블러 토글 후 가장 먼저 보이는 요소 탭 → 지정된 주 요소와 일치 | [NN/g 위계](https://www.nngroup.com/articles/visual-hierarchy-ux-definition/) |
| 본문 크기 | 본문 글자는 작게 잡지 않는다. | 웹 15–25px. 관례(Butterick). 최소 iOS 11pt·Android 12sp·웹 14px. 관례(국내 요약, Apple 값은 2차 미러). KRDS 본문 17px은 2차 | 슬라이더 → 14px 미만 실패, 16–18px 권장(제안) | [Butterick](https://practicaltypography.com/summary-of-key-rules.html), [요즘IT](https://yozm.wishket.com/magazine/detail/1017/), [KRDS 제3자 정리](https://www.oppadu.com/tools/design-systems-site/brand/krds.html) |
| 줄 길이 | 한 줄이 너무 길어지지 않게 본문 폭을 제한한다. | 라틴 45–75자, 이상적 66자. 관례(Bringhurst, 웹 번안판 경유 2차). 한글 모바일 30–40자·PC 40–70자. 관례(개인 블로그 수준). "한글 25–40자 환산"은 추정 | 끌어서 맞추기(칼럼 폭) → 줄당 글자 수(`ch` 단위 또는 폭 ÷ 평균 글자 폭)가 범위 안 | [Rutter](https://webtypography.net/2.1.2), [velog](https://velog.io/@hyounglee/typography-for-web-10), [inthiswork](https://inthiswork.com/archives/250750) |
| 줄 간격 | 한글 본문 행간은 글자 크기의 1.5–1.6배 안팎으로 잡는다. | 한글 1.6. 관례(요즘IT). 1.5–1.8. 관례(실무 글). KRDS·토스 본문 1.5는 2차. 라틴 120–145%. 관례(Butterick) | 슬라이더 → 한글 본문 1.5–1.7 우수, 1.4와 1.8 허용, 그 밖 감점(제안) | [요즘IT](https://yozm.wishket.com/magazine/detail/1017/), [Butterick](https://practicaltypography.com/line-spacing.html), [토스 제3자 정리](https://www.oppadu.com/tools/design-systems-site/brand/toss.html) |
| 크기와 행간의 반비례 | 글자가 커질수록 행간 배수는 줄인다. | 큰 제목 1.0–1.2, 본문 1.5. 관례(2차). Apple 텍스트 스타일 34/41, 17/22는 2차 미러 | 슬라이더 두 개 → 32px 이상은 1.0–1.3, 14–18px는 1.4–1.7(제안) | [rjseymour66 노트](https://rjseymour66.github.io/webdev/refactoring-ui/), [Apple HIG 미러](https://glama.ai/mcp/servers/@tmaasen/apple-dev-mcp/blob/b82f0efe2115dc4539c83a2374a714a84aeb350a/content/universal/typography.md) |
| 자간 | 한글 본문 자간은 0에서 아주 조금 좁히는 범위로 두고 영문 대문자는 넓힌다. | 한글 기본 0은 W3C 편집자 초안과 KRDS(2차). 16–17pt에서 −0.3(단위 미표기)은 관례(요즘IT). 대문자 +5–12%는 관례(Butterick) | 슬라이더 → 한글 본문 0 ~ −0.02em(제안), 양수면 감점. 대문자 라벨은 0.05–0.12em | [W3C klreq](https://w3c.github.io/klreq/new), [요즘IT](https://yozm.wishket.com/magazine/detail/1017/), [Butterick](https://practicaltypography.com/summary-of-key-rules.html) |
| 글자 크기 눈금 | 글자 크기도 정해진 눈금에서 고른다. | 12·14·16·18·20·24·30·36·48·60·72px. 관례(2차). 배율식은 1.2·1.25·1.333 등. 관례(에이전시 핸드북) | 다른 것 찾기 → 눈금 밖 크기 탐지 | [rjseymour66 노트](https://rjseymour66.github.io/webdev/refactoring-ui/), [Cieden](https://cieden.com/book/sub-atomic/typography/different-type-scale-types) |
| 서체 수 | 서체는 한 가지, 많아도 두 가지만 쓴다. | 1–2종. 관례·기업 브랜드 가이드 | 다른 것 찾기 → font-family 종류 ≤ 2, 한 문단 안 혼용 금지 | [KRAFTON](https://brand.krafton.com/ko/Typograhpy), [요즘IT](https://yozm.wishket.com/magazine/detail/1017/) |
| 한글 줄바꿈 | 한글은 어절 중간에서 줄이 끊기지 않게 한다. | `word-break: keep-all`과 `overflow-wrap: break-word`. 권장(개발자 블로그). W3C 문서는 글자 단위와 어절 단위를 모두 허용 | 둘 중 고르기 → 모든 줄바꿈 위치가 공백인지 검사 | [Dale Seo](https://daleseo.com/css-text-wrap/), [W3C klreq](https://w3c.github.io/klreq/new) |

이 단계에서 가장 객관적으로 가르칠 수 있는 한글 고유 규칙은 줄바꿈이다. 줄 끝이 어절 안에 걸렸는지는 코드로 완전히 판정된다. 반대로 서체 짝짓기는 권위 있는 규칙 집합을 찾지 못했으므로 "한 서체 안에서 굵기만 바꾼다"는 안전한 기본값만 가르치고 채점 문항에서는 빼는 편이 낫다.

## 아이콘과 광학 보정은 계산된 목표값과 넓은 허용 범위로 가르친다

아이콘 일관성은 속성 목록으로 풀린다. 조사한 모든 아이콘 시스템이 캔버스 크기, 여백, 선 굵기, 모서리 반경, 선 끝 모양, 채움 방식, 시점, 디테일 수준과 색 수라는 같은 변수들을 세트 전체에 고정한다. 수치도 **24px 캔버스에 2px 선**(Material 1 보관본, Lucide) 또는 32px 캔버스에 2px 선(IBM)으로 모인다 ([Material 1 아이콘](https://m1.material.io/style/icons.html), [Lucide](https://lucide.dev/contribute/icon-design-guide), [IBM](https://design-language-website-carbon-design-system.vercel.app/iconography/ui-icons/design)). 그래서 다른 것 찾기 문제는 한 번에 속성 하나만 바꿔 만들 수 있다. 주의할 점은 선 끝 모양이다. Material과 IBM은 각진 끝을, Lucide는 둥근 끝을 쓰므로 보편적 정답은 없고 "세트 안에서 일치하는가"만 정답이 된다. 평면 선 아이콘 사이에 입체·다색 아이콘이 끼면 어색한 이유는 시점, 디테일, 선 굵기, 색 수 규칙을 한꺼번에 어기고 채도·질감·밀도 면에서 훨씬 무겁기 때문인데, 이 설명은 여러 출처를 종합한 것이고 한 출처가 한 문장으로 말한 것은 아니다. 섞인 스타일이 사용성을 해친다는 실험 근거는 찾지 못했고, 금지는 가이드라인들의 합의다.

형태에서 가장 채점하기 좋은 규칙은 중첩 모서리 공식이다. 안쪽 반경은 바깥 반경에서 간격을 뺀 값이고, 바깥 50에 간격 20이면 안쪽은 30이다 ([Cloud Four](https://cloudfour.com/thinks/the-math-behind-nesting-rounded-corners/)). 광학 크기도 계산이 받쳐 준다. 원을 정사각형과 같은 면적으로 만들려면 지름이 변의 112.84%여야 하고 ([Bjango](https://bjango.com/articles/opticaladjustments/)), Material의 키라인은 사각 18dp에 원 20dp로 약 111%다. 재생 삼각형은 무게중심이 밑변에서 1/3 지점에 있으므로 경계 상자 중심(1/2)과의 차이인 **삼각형 길이의 1/6, 약 16.7%**만큼 꼭짓점 쪽으로 옮기면 된다. 이 16.7%는 출처에 적힌 수가 아니라 무게중심 원리에서 이 조사가 계산한 값이다.

**표 4. 아이콘 일관성·형태감 (7단계)**

| 개념 | 한 문장 규칙 | 수치 기준과 지위 | 실습 형식 → 코드 채점 기준 | 출처 |
|---|---|---|---|---|
| 한 세트 한 규격 | 한 화면의 아이콘은 한 라이브러리의 한 설정에서만 가져온다. | 24px 캔버스 + 2px 선(Material 1 보관본, Lucide), 32px + 2px(IBM). 플랫폼 가이드(해당 시스템 안에서만 구속) | 다른 것 찾기: 4–6개 중 한 속성만 다른 아이콘 → 속성 태그 비교, 정답률과 반응 시간 기록 | [Material 1](https://m1.material.io/style/icons.html), [Lucide](https://lucide.dev/contribute/icon-design-guide), [IBM](https://design-language-website-carbon-design-system.vercel.app/iconography/ui-icons/design) |
| 선 굵기 | 세트 안 모든 선은 같은 굵기다. | 2dp, 복잡하거나 작은 아이콘만 1.5dp 예외. 플랫폼 가이드 | 다른 것 찾기(1.5px 대 2px) → stroke-width 값 일치 | [Material 1](https://m1.material.io/style/icons.html) |
| 끝 모양·모서리 | 선 끝과 모서리 처리는 세트 안에서 하나로 통일한다. | Material·IBM은 각진 끝, Lucide는 둥근 끝과 반경 2px. 시스템마다 달라 정답은 "세트 내 일치" | 다른 것 찾기 → linecap·linejoin·반경 값 일치 | [IBM](https://design-language-website-carbon-design-system.vercel.app/iconography/ui-icons/design), [Lucide](https://lucide.dev/contribute/icon-design-guide) |
| 채움 방식 | 외곽선형과 채움형은 뜻이 있을 때만 섞는다. | 수치 없음. 관례(외곽선 = 기본, 채움 = 선택 상태) | 다른 것 찾기, 둘 중 고르기 → 채움 태그가 상태 태그와 일치 | [Shestopalov 아이콘 세트](https://medium.com/design-bridges/icon-set-3b4fc87dc6b5) |
| 시점·디테일·색 수 | 평면 선 아이콘 사이에 입체나 다색 그림을 섞지 않는다. | 제품 아이콘 1색, 마케팅 아이콘 최대 2색, 3색 이상은 일러스트. 관례(Figma 디자인 시스템 가이드) | 다른 것 찾기 → 색 수와 시점 태그 | [designsystems.com](https://www.designsystems.com/iconography-guide/), [Shestopalov 아이콘 세트](https://medium.com/design-bridges/icon-set-3b4fc87dc6b5) |
| 여백과 최소 틈 | 아이콘은 캔버스 가장자리와 선 사이에 틈을 남긴다. | 24dp 캔버스 안 20dp 라이브 영역. 플랫폼 가이드(Material 1 보관본). 선 사이 틈 2px 이상. 플랫폼 가이드(Lucide) | 둘 중 고르기 → 경계 상자가 라이브 영역 안, 최소 틈 ≥ 2px | [Material 1](https://m1.material.io/style/icons.html), [Lucide](https://lucide.dev/contribute/icon-design-guide) |
| 글자와 굵기 맞추기 | 아이콘 굵기는 옆 글자 굵기와 맞춘다. | SF Symbols는 9굵기·3스케일. 플랫폼 가이드 | 둘 중 고르기 → 아이콘 굵기 값 = 텍스트 굵기 값 | [Apple SF Symbols](https://developer-mdn.apple.com/design/human-interface-guidelines/foundations/sf-symbols) |
| 광학 크기 | 같은 상자에 넣으면 원이 사각형보다 작아 보이므로 원을 더 크게 그린다. | 사각 18dp·원 20dp(약 111%). 플랫폼 가이드(Material 1 보관본). 면적 일치 112.84%. 기하·관례 | 슬라이더: 원 크기 → 사각 변 대비 110–116%(제안) | [Material 1](https://m1.material.io/style/icons.html), [Bjango](https://bjango.com/articles/opticaladjustments/) |
| 중첩 모서리 | 안쪽 모서리 반경은 바깥 반경에서 간격을 뺀 값이다. | 안쪽 = 바깥 − 간격(50 − 20 = 30). 기하·관례. 결과가 0이면 1–4 정도를 눈으로 잡음 | 슬라이더 → max(바깥 − 간격, 0)의 ±1–2px(제안, 0 하한은 이 보고서의 정식화) | [Cloud Four](https://cloudfour.com/thinks/the-math-behind-nesting-rounded-corners/), [Hype4](https://hype4.academy/articles/design/your-radius-nesting-guide) |
| 부드러운 모서리 | 곡률이 서서히 변하는 모서리가 원호를 바로 붙인 모서리보다 매끈해 보인다. | "Figma 코너 스무딩 60%가 iOS 아이콘과 같다"는 값은 미확인(제3자 블로그, Apple·Figma 1차 문서 미확인) | 둘 중 고르기(감상용, 점수 비중 낮게) | [squircle.js.org](https://squircle.js.org/blog/squircle-vs-rounded-rectangle) |
| 각도 | 사선은 정해진 각도만 쓴다. | 45° 우선, 그 밖은 15° 배수. 플랫폼 가이드(IBM) | 다른 것 찾기 → 각도 mod 15 = 0 | [IBM](https://design-language-website-carbon-design-system.vercel.app/iconography/ui-icons/design) |
| 황금비 | 황금비는 법칙이 아니라 선택 도구다. | 1.618을 특별히 선호한다는 근거 없음, 선호 범위 1.414–1.732 보고. 2차(잡지 기사 경유, 일부 미발표 실험) | 채점 문항으로 쓰지 않고 한 줄 팁으로만 | [Fast Company](https://www.fastcompany.com/3044877/the-golden-ratio-designs-biggest-myth) |

무게와 균형은 이 커리큘럼에서 근거가 가장 약한 영역이다. 시각적 무게 요인을 정리한 Steven Bradley는 무게를 정밀하게 재는 방법을 모른다고 직접 밝혔고, 실용적 확인법으로 스퀸트 테스트만 제시한다 ([Smashing Magazine](https://www.smashingmagazine.com/2014/12/design-principles-visual-weight-direction)). Arnheim의 이론은 원전을 읽지 못해 블로그와 강의 노트 요약에 의존했고, 그 이론을 검증한 실험 논문들도 열지 못했다. 출처끼리 충돌도 있다. Bradley는 어두울수록 무겁다고 하고 Arnheim 요약은 밝은 것이 어두운 것보다 무겁다고 한다 ([Cartwright 노트](https://k-cartwright.blogspot.com/2009/11/balance-weight-and-direction.html?m=1)). 앱에서는 "배경과의 대비가 클수록 무겁다"로 가르치면 두 주장과 모두 어긋나지 않는데, 이 절충은 이 조사의 해석이다. 따라서 이 단계의 문제는 한 변수만 다른 쌍을 쓰고, 끌어서 맞추기에는 점이 아니라 넓은 허용 영역을 둬야 한다.

**표 5. 시각적 무게·균형·광학 보정 (8단계)**

| 개념 | 한 문장 규칙 | 수치 기준과 지위 | 실습 형식 → 코드 채점 기준 | 출처 |
|---|---|---|---|---|
| 시각적 무게 | 크고, 채도가 높고, 배경과 대비가 크고, 홀로 떨어진 요소일수록 무겁게 보인다. | 측정법 없음. 관례. Arnheim의 요인 목록은 이론(2차) | 둘 중 고르기 "어느 쪽이 더 무거운가", 블러 토글 → 한 변수만 다른 쌍에서 변수의 방향 | [Smashing 무게](https://www.smashingmagazine.com/2014/12/design-principles-visual-weight-direction) |
| 지렛대 균형 | 무거운 요소는 중심 가까이, 가벼운 요소는 멀리 두면 균형이 맞는다. | 수치 없음, 눈으로 판단. 관례·이론(2차) | 끌어서 맞추기: 작고 진한 블록을 옮겨 크고 연한 블록과 균형 → 무게 × 거리 합의 중심이 프레임 중심 주변 허용 영역 안(교육용 근사, 이 공식을 인정한 출처 없음) | [Smashing 균형](https://www.smashingmagazine.com/2015/06/design-principles-compositional-balance-symmetry-asymmetry/), [Duke 강의 자료](https://sites.math.duke.edu/education/ccp/resources/write/design/graphic7.html) |
| 균형 유형 | 균형에는 대칭, 비대칭, 방사, 모자이크 네 가지가 있다. | 분류 체계. 관례 | 둘 중 고르기(분류) → 유형 태그 일치 | [Smashing 균형](https://www.smashingmagazine.com/2015/06/design-principles-compositional-balance-symmetry-asymmetry/) |
| 시각적 중심 | 홀로 놓인 요소는 정중앙보다 살짝 위에 둬야 가운데로 보인다. | "살짝"뿐이고 어떤 출처에도 수치 없음("약 10% 위"는 미확인). 관례·이론 | 끌어서 맞추기(세로) → 기하 중심보다 위쪽의 넓은 허용 영역(제안), 정중앙 버전을 비교로 공개 | [Duke 강의 자료](https://sites.math.duke.edu/education/ccp/resources/write/design/graphic7.html), [Paper Mill Store](https://blog.thepapermillstore.com/designing-using-visual-center/) |
| 삼각형 중심 | 재생 삼각형은 경계 상자가 아니라 무게중심을 원의 중심에 맞춘다. | 무게중심은 밑변에서 1/3 지점(기하). 이동량 = 삼각형 길이의 1/6 ≈ 16.7%(이 조사의 계산). 작은 아이콘에서는 약 1px(뉴스레터) | 끌어서 맞추기(가로) → 꼭짓점 쪽 이동량이 길이의 16.7% ± 허용(제안) | [Bjango](https://bjango.com/articles/opticaladjustments/), [Iconic](https://iconic.iconbuddy.com/p/week-01-why-your-icons-look-off) |
| 오버슈트 | 둥글거나 뾰족한 형태는 기준선을 조금 넘겨야 같은 높이로 보인다. | O는 대문자 높이의 약 1–3%, Karow 권고는 O 3%·A 5%. 관례(Wikipedia 경유 2차) | 슬라이더: O의 높이 → H 대비 +1–3% | [Wikipedia](https://en.wikipedia.org/wiki/Overshoot_%28typography%29) |
| 버튼 라벨 세로 중앙 | 버튼 글자는 줄 상자가 아니라 대문자 높이를 기준으로 가운데에 맞춘다. | 수치 없음. 관례(라틴 문자 기준, 한글은 조사되지 않음) | 끌어서 맞추기(세로) → 대문자 높이 상자의 위아래 여백 차이 ≤ 1px(제안) | [Shestopalov 광학 효과](https://medium.com/design-bridges/optical-effects-9fca82b4cd9a) |

## 연속값은 거리로 채점하고 정답을 겹쳐 보여 준다

기존 도구들이 이미 형식별 채점 방식을 검증해 놓았다. Can't Unsee는 같은 UI의 두 버전 중 하나를 고르게 하고, 답한 뒤 두 카드를 겹쳐 빠르게 번갈아 보여 주며 무엇이 바뀌었는지 짧게 설명한다 ([The Next Web](https://thenextweb.com/news/design-skills-cant-unsee-quiz), [Medium 게임 비평](https://medium.com/@jianingl/game-critique-blog-cant-unsee-7e748af41914)). Kern Type은 글자를 끌어 간격을 맞추면 100점 만점 점수와 함께 기준 자간을 나란히 보여 주고 ([Where Creativity Works](https://wherecreativityworks.com/graphic-design-games/)), The Eyeballing Game은 오차를 픽셀로 재서 평균을 점수로 삼고 놓는 즉시 올바른 도형을 초록색으로 덧그린다 ([woodgears.ca](https://woodgears.ca/eyeball/about.html)). 두 도구에 대한 정보는 공식 사이트가 아니라 디자인 매체 기사와 제작자 설명 페이지에서 얻었다. 공통점은 뚜렷하다. 평가가 좋은 도구는 모두 답한 직후 기준 답안을 학습자의 답 위에 겹쳐 보여 준다.

**표 6. 실습 형식별 적합 개념과 채점**

| 형식 | 맞는 개념 | 채점 | 답한 뒤 보여 줄 것 |
|---|---|---|---|
| 둘 중 고르기 | 변수 하나만 다르고 정답을 방어할 수 있는 쌍: 대비 통과 여부, 왼쪽 대 가운데 정렬, 한글 줄바꿈, 버튼 위계, 틴트 회색 | 정오 + 반응 시간 | 두 버전 겹쳐 번갈아 보기 + 한 문장 이유 |
| 다른 것 찾기 | 일관성 개념: 아이콘 선 굵기·끝 모양·채움, 눈금 밖 간격, 어긋난 정렬, 여러 개의 채운 버튼 | 정오 + 반응 시간 | 다른 속성 강조 표시 + 수치 비교 |
| 슬라이더 조절 | 연속값 개념: 대비, 행간, 자간, 터치 영역, 원 대 사각 크기, 안쪽 반경, 오버슈트 | 목표 범위와의 거리를 통과·거의·재시도 세 구간으로 | 권장 범위 표시 + 학습자 값과 기준값 나란히 |
| 끌어서 맞추기 | 위치·순서 개념: 공유선 정렬, 라벨 근접성, 칼럼 맞춤, 삼각형 중심, 균형, 밝기 순서 배열 | 목표 위치와의 픽셀 거리 또는 허용 영역 포함 여부 | 가이드선·기준 도형 덧그리기 |

이 대응은 기존 도구가 어떤 기술에 어떤 조작을 붙였는지에서 끌어낸 추론이다. 시각 디자인 판단을 가르치는 데 형식들을 비교한 연구는 찾지 못했다. 다만 설계 근거는 있다. 연속 오차를 주고 기준을 보여 주는 형식은 한 문제에서 얻는 정보가 많고, 둘 중 고르기는 문제당 정오 한 비트에 설명이 더해질 뿐이다. 그래서 같은 개념을 "둘 중 고르기로 알아보기 → 슬라이더나 끌기로 직접 만들기" 순으로 두 번 다루는 구성이 합리적이다.

채점 가능성은 개념마다 다르다. 가장 객관적인 쪽부터 나열하면 터치 영역 크기와 간격, 눈금 위 간격 값, 안쪽 간격과 바깥 간격의 대소, 공유 정렬선, 줄당 글자 수, 크기별 행간 범위, 크기·굵기·색의 개수, 어절 줄바꿈, 화면당 주 버튼 수 순이고, 서체 짝짓기와 "충분한" 여백과 균형 판단이 가장 주관적이다. 점수에 넣는 비중도 이 순서를 따르는 것이 안전하다. 시간 제한은 처음부터 걸지 않는 편이 낫다. 아케이드형 게임은 시간 압박을 쓰지만 지각 학습 모듈은 반응 시간을 벌점이 아니라 숙련도 지표로 기록한다 ([Kellman 백서](https://kellmanlab.psych.ucla.edu/files/kellman_massey_2005.pdf)).

## 8단계 순서와 "쌍 먼저, 문장 나중" 레슨 구조

조사한 실무 커리큘럼들은 위계·정렬·간격·레이아웃을 먼저, 타이포그래피와 색을 가운데, 깊이·이미지·아이콘·마감을 뒤에 둔다. Refactoring UI는 위계 → 레이아웃과 간격 → 텍스트 → 색 → 깊이 → 이미지 → 마감 순이고 ([Refactoring UI](https://www.refactoringui.com/)), Learn UI Design은 기초(정렬·간격·일관성·크기) → 색 → 타이포그래피 → 컴포넌트(아이콘 디자인 포함) 순이다 ([Learn UI Design](https://learnui.design/)). 확인된 커리큘럼 어디에서도 색이 맨 앞에 오지 않는다. 요청에서 색감을 기초에 넣은 것과 이 관행을 함께 살리는 방법은 색을 둘로 쪼개는 것이다. 수식으로 판정되는 지각과 대비는 기초에 두고, 팔레트 구성은 타이포그래피 뒤로 보낸다. 이 8단계는 이 조사의 종합이며, 어떤 주제 순서가 더 잘 배워지는지 실험한 근거는 없다.

**표 7. 권장 8단계**

| 단계 | 다루는 개념 | 주 형식 | 이 자리에 두는 이유 |
|---|---|---|---|
| 1. 정렬 | 공유선, 왼쪽 대 가운데, 베이스라인 | 둘 중 고르기 → 끌어서 맞추기 | 정답이 좌표로 정해지고 가이드선 하나가 설명을 대신함 |
| 2. 간격 | 근접성, 간격 눈금, 그리드, 터치 영역 | 끌어서 맞추기, 슬라이더 | 대소 비교와 집합 포함 여부로 채점됨 |
| 3. 색 기초 | 세 다이얼, 지각 밝기, 대비, 색만으로 말하지 않기 | 슬라이더, 순서 배열 | WCAG 수식이 정답을 줌. 색 맞추기는 초반 흥미 유발에도 좋음 |
| 4. 위계 | 단계 수, 굵기와 색, 버튼 위계, 스퀸트 | 둘 중 고르기, 블러 토글 | 1–3단계의 간격·대비를 재료로 씀 |
| 5. 타이포그래피 | 본문 크기, 줄 길이, 행간, 자간, 크기 눈금, 한글 줄바꿈 | 슬라이더 | 범위 판정. 한글 전용 자극이 필요 |
| 6. 색 구성 | 60-30-10, 강조색, 조화 각도, 음영 눈금, 틴트 회색 | 둘 중 고르기, 슬라이더 | 관례 비중이 커지므로 "권장" 표기와 스타일 점수 분리 |
| 7. 아이콘·형태 | 세트 규격, 광학 크기, 중첩 모서리 | 다른 것 찾기, 슬라이더 | 일관성 감각은 앞 단계의 반복 경험 위에서 생김 |
| 8. 무게·균형·광학 보정 | 시각적 무게, 균형, 시각적 중심, 삼각형 중심, 오버슈트 | 끌어서 맞추기(넓은 허용 영역) | 근거가 가장 약하고 정답이 범위임 |

레슨 한 개의 구조에 대해서는 학습 과학의 근거가 비교적 단단하다. Schwartz와 Bransford의 실험에서 대조 사례를 먼저 분석한 뒤 설명을 들은 학생이 일주일 뒤 예측 과제를 가장 잘 풀었고, 단순 참·거짓 확인 문항은 모든 조건에서 약 93%로 차이를 드러내지 못했다 ([Schwartz & Bransford 1998](https://www.wright.edu/sites/www.wright.edu/files/uploads/2017/Feb/event/Schwartz_Bransford_1998_TimeForTelling.pdf)). 앱에 옮기면 두 가지가 나온다. 첫째, "한두 문장 설명"은 문제 앞이 아니라 **첫 선택 직후**에 줘야 한다. 둘째, 단원 끝 확인은 같은 문제의 반복이 아니라 스타일과 컴포넌트가 다른 새 자극으로 해야 이해 여부가 드러난다. 여기에 풀이가 끝난 예시 하나를 먼저 보여 주고 시작하면 효율이 오른다. Kellman 연구실의 실험에서 정답을 보여 주는 시행 뒤에 능동 시행을 붙인 조건은 능동 시행만 한 조건보다 약 30회 적은 시행으로 숙달에 이르렀다 ([Thai 2015](https://escholarship.org/content/qt8nv5m69d/qt8nv5m69d.pdf)).

문제 배열에서는 묶기와 섞기의 순서가 중요하다. 화가 12명의 화풍을 익히는 실험에서 작가를 섞어 보여 준 쪽이 새 그림 판별에서 **61% 대 35%**로 앞섰고, 그런데도 참가자의 83%는 묶어 보는 쪽이 같거나 낫다고 평가했다 ([Kornell & Bjork 2008](https://bjorklab.psych.ucla.edu/wp-content/uploads/sites/13/2016/07/Kornell_Bjork_2008_PsychScience.pdf)). 중학교 수학에서는 섞은 연습이 30일 뒤 74% 대 42%였다 ([Rohrer 외 2014](https://Www.Gwern.net/doc/psychology/spaced-repetition/2014-rohrer-2.pdf)). 다만 학습자가 대응할 배경 지식이 없으면 어려움은 득이 되지 않는다 ([Bjork & Bjork](https://bjorklab.psych.ucla.edu/wp-content/uploads/sites/13/2016/04/EBjork_RBjork_2011.pdf)). 그래서 새 개념은 처음 몇 문제만 묶어서 내고 이후 복습에서는 이전 개념과 섞는 것이 맞다. 섞은 복습은 체감 만족도가 낮게 나오므로 세션 정답률이나 "쉬웠다"는 응답만으로 커리큘럼을 조정하면 안 된다. 복습 간격은 기억을 유지하려는 기간이 길수록 길게 잡아야 한다 ([Cepeda 외 2008](https://pubmed.ncbi.nlm.nih.gov/19076480/)).

숙달 기준과 난이도에는 빌려 올 수 있는 수치가 둘 있다. Kellman 계열 적응형 시스템은 정확도·반응 시간·마지막 출제 이후 경과를 합쳐 약한 범주를 더 자주 내고, 연속 3–4회 정답이면서 각 15초 이내일 때 그 범주를 졸업시켰다 ([Thai 2015](https://escholarship.org/content/qt8nv5m69d/qt8nv5m69d.pdf)). 정답률 목표로 자주 인용되는 85%는 이진 분류를 배우는 모형 학습자에 대해 유도된 값으로, 최적 오답률이 약 15.87%다 ([Wilson 외 2019](https://ideas.repec.org/a/nat/natcom/v10y2019i1d10.1038_s41467-019-12552-4.html)). 사람의 디자인 훈련에서 측정된 값이 아니므로 둘 중 고르기 문항의 난이도를 80–90% 정답률 근처로 맞추는 내부 휴리스틱으로만 써야 한다. 피드백은 즉시 주되 점수만 던지지 말아야 한다. 기술을 처음 익히는 단계에서는 즉시 피드백이 유리하고 구체적 코멘트가 점수보다 효과적이라는 정리가 있는데, 이는 실무자용 연구 요약에 의존한 2차 근거다 ([ASCD](https://ascd.org/el/articles/research-says-good-feedback-is-targeted-specific-timely)).

습관 장치는 근거의 성격을 구분해서 써야 한다. Duolingo는 리그 도입으로 총 학습 시간이 17% 늘었고 ([Lenny's Newsletter](https://lennysnewsletter.com/p/how-duolingo-reignited-user-growth)), 연속 기록 보호권을 두 개까지 허용하자 일일 활성 학습자가 0.38% 늘었다고 밝혔다 ([Duolingo 블로그](https://blog.duolingo.com/how-duolingo-streak-builds-habit)). 이 수치들은 전부 자사 실험의 참여 지표이지 실력 향상 측정이 아니다. 같은 회사가 다른 게임에서 빌려 온 "이동 횟수 제한"은 효과가 완전히 중립이었다. 게이미피케이션 메타분석은 인지적 학습 성과에 g = .49의 효과를 보고했고 엄격한 연구들에서도 이 효과만 안정적이었다 ([Sailer & Homner 2020](https://opus.bibliothek.uni-augsburg.de/opus4/frontdoor/index/index/docId/109056)). 초기 사용자 수가 적은 앱이라면 리그보다 연속 기록과 보호권이 싸고 근거 있는 출발점이다. 반면 피드백 없는 습관 챌린지는 오래 가지 않는다. Daily UI는 40일 뒤 참가자의 20% 미만만 남았다는 보고가 인용된다 ([UX Planet](https://uxplanet.org/daily-ui-makes-you-a-better-designer-sort-of-d87b603e5499)).

## 2차 출처에 기댔거나 확인하지 못한 수치

아래 항목은 앱에 싣기 전에 1차 문서로 다시 확인해야 한다. 표 안에서 2차·미확인으로 표시한 것을 한곳에 모았다.

| 항목 | 상태 | 이 보고서의 처리 |
|---|---|---|
| Refactoring UI 책 본문(간격 눈금, 25% 규칙, 행간·자간, 덜 중요한 것 낮추기, 음영 채도·색상 20–30° 이동) | 책은 유료라 읽지 못함. 독자 노트 2–3종에 의존. 저자 Medium 글과 공개 미리보기 챕터만 직접 확인 | 2차로 표기. 인용 전 책 대조 필요. 눈금에 256이 있는지도 미확인 |
| Apple HIG 수치(44pt, 최소 28pt, 글자 크기 17/11pt, 텍스트 스타일 행간, 컨트롤 여백 12·24pt) | 공식 페이지를 열지 못해 미러 2곳에 의존. HIG 색 페이지와 SF Symbols 페이지는 확인 | 2차로 표기 |
| Material 3 전반 | m3.material.io가 렌더링되지 않음. 8dp 그리드·키라인·아이콘 수치는 Material 1 보관본, 48dp는 Google 접근성 도움말 기준 | M3의 창 크기 등급(600·840dp), 13단계 톤 값과 역할 대응, 모양 토큰은 미확인이므로 싣지 않음 |
| Material 2 다크 테마(흰 글자 불투명도 87·60·38% 등) | 페이지 미확인. `#121212`만 업체 블로그 경유로 확인 | 불투명도 수치는 싣지 않음 |
| KRDS·토스 수치 | 공식 문서가 아닌 제3자 갤러리 페이지. KRDS 제목 행간과 모바일 여백, 토스 자간(−0.01~−0.04em)과 간격 체계는 그 페이지 작성자의 추정 | 2차로 표기. 추정값은 채점 기준에 쓰지 않음 |
| Williams의 네 원칙, Bringhurst의 45–75자, Karow의 오버슈트 3%·5% | 원서를 읽지 못함. 각각 블로그 요약, 웹 번안판, Wikipedia 경유 | 2차로 표기 |
| Arnheim의 무게 요인·구조 골격·지렛대 원리 | 원전과 검증 논문 모두 열지 못함 | 이론·2차로 표기. 측정 기준처럼 쓰지 않음 |
| 요즘IT의 자간 −0.3 | 단위가 기사에 없음 | "단위 미표기"로 표기. −0.018em 환산은 추정 |
| 시각적 중심의 위쪽 이동량, Figma 코너 스무딩 60% | 수치를 준 1차 출처 없음 | 미확인으로 표기 |
| 색각 이상 전체 인구 비율(약 2.5%), 한국 유병률 | 자동 요약에서만 확인되거나 자료 없음 | 싣지 않음. 남 1/12·여 1/200만 사용 |
| 조화 각도, 거터 폭 | 각도는 라이브러리 문서 기준, 유사색 30°는 기본값일 뿐. 거터 16–24px는 출처 없음 | 각도는 관례로 표기. 거터 수치는 싣지 않음 |
| 흰 배경 대비 앵커와 색 쌍 대비 값 | W3C 공식으로 조사 중 계산한 값 | 계산값으로 표기. 구현 후 검산 필요 |
| Can't Unsee·Method of Action의 현재 운영 상태와 세부 방식 | 공식 사이트 미접속, 2019년 전후 기사에 의존 | 방식만 인용 |
| 85% 규칙, 전문성 역전, 피드백 시점 | 논문 전문 대신 초록 기록·보도자료·Wikipedia·실무 요약에 의존 | 휴리스틱·2차로 표기 |
| Shift Nudge 커리큘럼 | 공식 여부를 확인하지 못한 미러 페이지 | 순서 논거에서 제외 |
| 한국어 인터랙티브 디자인 퀴즈의 부재 | 제한된 검색에서 찾지 못했을 뿐 | 확인된 사실로 쓰지 않음 |

조사 범위 밖이어서 비어 있는 것도 있다. 한국형 웹 콘텐츠 접근성 지침(KWCAG)은 확인하지 않았고, 한글의 버튼 내 세로 중앙 맞춤(대문자 높이 개념이 없음)과 한글 자간 기준 데이터는 출처를 찾지 못했다. 색각 시뮬레이션 행렬과 APCA 공식도 수집하지 않았다.

## Conclusion

이 조사가 바꾼 관점은 "감각"이 훈련 불가능한 취향이 아니라는 것이다. 52개 개념 중 절반 이상이 좌표·개수·범위·수식으로 판정되고, 판정이 어려운 것은 서체 짝짓기와 균형처럼 뒤 단계에 몰려 있다. 그래서 커리큘럼 순서는 주제의 중요도보다 **정답의 객관성이 높은 것에서 낮은 것으로** 흐르게 짜는 편이 맞고, 화면마다 "표준"과 "권장"을 구분해 보여 주는 것이 선행 서비스가 받은 비판을 피하는 가장 값싼 방법이다.

만들면서 직접 채워야 할 공백이 세 가지 남는다. 첫째, 허용오차는 어디에도 공개된 값이 없으므로 초기 사용자의 응답 분포를 모아 통과 구간을 보정해야 한다. 둘째, 한글 전용 자극(자간·행간·어절 줄바꿈·버튼 내 세로 정렬)은 기존 영어권 게임이 다루지 않은 영역이라 차별점이 되지만 기준 데이터도 직접 만들어야 한다. 셋째, 연속 기록 같은 참여 지표와 실력 유지는 별개이므로, 며칠 뒤 새 자극으로 다시 묻는 지연 재시험을 처음부터 넣어 "계속 오는가"와 "눈이 좋아졌는가"를 따로 재야 한다.
