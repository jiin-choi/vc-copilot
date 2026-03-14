# VC Copilot

Claude Code 커스텀 슬래시 커맨드로 만든 **VC 심사역 워크플로우 자동화** 스킬 모음입니다.

> 한국 VC 심사역의 소싱 → 평가 → 운영 전 과정을 Claude Code가 보조합니다.

## 스킬 맵

### Sourcing (소싱)

| 스킬 | 설명 | 깊이 |
|------|------|------|
| `/news` | 복수 매체 보도 기준 뉴스 다이제스트 | 빠르게 · 시장 읽기 |
| `/signal` | 5대 카테고리 위클리 시그널 스캔 | 깊게 · 시장 읽기 |
| `/deal` | 3-Tier Alpha Sourcing — VC Blind Spot 기업 포착 | 빠르게 · 기업 액션 |
| `/thesis` | 섹터/테마 딥리서치 + 스타트업 발굴 | 깊게 · 기업 액션 |

### Evaluation (평가)

| 스킬 | 설명 |
|------|------|
| `/premeeting` | 오늘 미팅 기업 자동 리서치 → 2분 브리핑 |
| `/postmeeting` | 미팅 후 구조화된 투자 메모 (Bull/Bear Case) |

### Operations (운영)

| 스킬 | 설명 |
|------|------|
| `/ipo` | KRX 예비심사 현황 크롤링 → Google Sheets + 임플리케이션 |

## 소싱 2x2

|  | 시장 (읽기) | 기업 (액션) |
|--|-----------|-----------|
| **빠르게** | `/news` | `/deal` |
| **깊게** | `/signal` | `/thesis` |

## 사용법

### 1. 스킬 파일 복사
```bash
# Claude Code 프로젝트의 .claude/commands/ 디렉토리에 복사
cp commands/*.md /your-project/.claude/commands/
```

### 2. 환경 설정
스킬들은 `CLAUDE.md`(프로젝트 설정)와 `MEMORY.md`(학습 데이터)를 참조합니다. 스킬 파일을 복사한 뒤, Claude Code에게 본인 환경에 맞게 설정해달라고 요청하세요. 투자 섹터, Notion DB ID, Slack 연동 등을 대화하면서 세팅할 수 있습니다.

### 3. 필요한 MCP 서버 연동

| MCP 서버 | 사용하는 스킬 |
|----------|-------------|
| Google Calendar | `/premeeting`, `/postmeeting` |
| Notion | `/deal`, `/thesis`, `/signal`, `/premeeting`, `/postmeeting` |
| Slack | `/deal`, `/thesis`, `/signal`, `/news`, `/premeeting`, `/postmeeting` |
| Gmail | `/deal`, `/thesis` |
| Google Sheets | `/ipo` |

> MCP 서버 연동 없이도 WebSearch 기반 기능(뉴스 수집, 기업 리서치 등)은 동작합니다.

### 4. 크로스 스킬 학습 (MEMORY.md)

스킬들은 `MEMORY.md`를 통해 학습 데이터를 공유합니다:

- **선호 프로파일**: 심사역의 선택 패턴을 누적 학습 (보수적: 2회+ 확인 시만 반영)
- **Drop 패턴**: 탈락 사유를 학습하여 소싱 시 경고 시그널로 활용
- **Watchlist**: 관심 기업 자동 추적 + 에이징 관리

```
읽기: /deal, /thesis, /signal, /premeeting
쓰기: /deal, /thesis (선택 후)
```

## 설계 원칙

- **AI는 판단 재료를 정리하고, 심사역이 판단한다**: 결론을 단정짓지 않고 선택지와 트레이드오프를 제시
- **반론·리스크 필수**: 모든 분석에 Bear Case 포함
- **보수적 학습**: 같은 패턴이 2회 이상 확인될 때만 프로파일 반영
- **편향 차단**: `/deal`의 컨트래리언 픽 — 선호에 반하는 기업 1개 강제 포함
- **출처 필수**: 모든 데이터에 출처 명시, 미확인 정보는 "확인 필요" 표시

## License

MIT
