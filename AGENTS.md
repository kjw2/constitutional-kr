# constitutional-kr — Agent Guidelines

## Repository

- 헌법재판소 결정례 Markdown 데이터 저장소입니다.
- 데이터는 `legalize-pipeline`의 `constitutional/` 파이프라인에서 생성합니다.
- 원천 데이터는 국가법령정보센터 OpenAPI `target=detc`입니다.

## Rules

- 생성된 Markdown 파일은 가능하면 직접 수정하지 말고 파이프라인을 수정한 뒤
  재생성합니다.
- 경로 형식은 `{사건종류}/{재판부}/{종국일자}_{사건번호}_{헌재결정례일련번호}.md`입니다.
- 파일명과 경로는 NFC 정규화를 유지합니다.
- `헌재결정례일련번호`는 frontmatter와 커밋 메시지에 반드시 포함합니다.
- `metadata.json`과 `stats.json`은 저장소 내부에 두지 않습니다. 필요한 통계는
  웹 빌드 또는 별도 인덱서가 이 저장소를 스캔해 생성합니다.

## Commit Convention

파이프라인 커밋 메시지는 다음 형식을 사용합니다.

```text
헌재결정례: {사건명}

헌재결정례: https://www.law.go.kr/DRF/lawService.do?target=detc&ID={헌재결정례일련번호}
종국일자: YYYY-MM-DD
사건번호: {사건번호}
사건종류: {사건종류}
재판부: {재판부}
헌재결정례일련번호: {헌재결정례일련번호}
```
