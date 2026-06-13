# constitutional-kr

대한민국 헌법재판소 결정례 Markdown 데이터 저장소입니다.

이 저장소는 `legalize-pipeline`의 헌재결정례 파이프라인이 생성하는 출력
저장소입니다. 원천 데이터는 국가법령정보센터 OpenAPI의 헌재결정례 API입니다.

## 데이터 출처

- 목록: `lawSearch.do?target=detc`
- 본문: `lawService.do?target=detc&ID={헌재결정례일련번호}`

## 디렉터리 구조

```text
{사건종류}/{재판부}/{종국일자}_{사건번호}_{헌재결정례일련번호}.md
```

예시:

```text
헌법소원/전원재판부/2024-03-28_2020헌마123_123456.md
위헌법률심판/지정재판부/2024-01-10_2021헌가7_123457.md
```

사건명은 파일명에 넣지 않고 frontmatter와 문서 제목에 기록합니다. 긴 사건명으로
인한 파일명 제한 문제를 피하고, `헌재결정례일련번호`로 고유성을 보존하기
위함입니다.

## Markdown 형식

각 파일은 YAML frontmatter와 본문으로 구성됩니다.

```yaml
---
헌재결정례일련번호: '123456'
사건번호: '2020헌마123'
사건명: 자동차관리법 제26조 등 위헌확인
사건종류: 헌법소원
사건종류코드: ''
재판부: 전원재판부
재판부구분코드: '430201'
종국일자: 2024-03-28
출처: https://www.law.go.kr/DRF/lawService.do?target=detc&ID=123456
첨부파일: []
---
```

본문 섹션은 가능한 경우 다음 순서로 렌더링합니다.

```markdown
# 사건명

## 판시사항

## 결정요지

## 심판대상조문

## 참조조문

## 참조판례

## 전문
```

## 생성

이 저장소는 수작업 편집보다 파이프라인 재생성을 우선합니다.

```bash
python -m constitutional.fetch_cache
python -m constitutional.import_decisions --git
python -m constitutional.validate "$CONSTITUTIONAL_KR_REPO"
```

증분 업데이트는 다음 형태를 목표로 합니다.

```bash
python -m constitutional.update --days 14 --commit
```
