# 12th-education

IT 연합동아리 '코테이토' 12기 교육팀 발표 자료 폴더입니다.

교육팀은 CS지식, 기술 면접에 자주 출제되는 주제를 매주 공부하고 이를 바탕으로 '코테이토 12기 정규세션'에서 해당 주제들을 발표합니다. 세션간 정규 교육은 6개월간 9회 진행될 계획입니다.

# Goals

1. CS와 기술 면접 주제에 대해 공부를 진행하고 서로 피드백한다.
2. 상호 피드백과 검증을 통해 올바른 지식 전달을 위해 노력한다.
3. 아는 것에 그치지 않고 타인에게 설명할 수 있는 능력을 기른다.
   <br>

# Members

| <img src="https://github.com/kimminna.png" width=120/> | <img src="https://github.com/DandelionQZ.png" width=120/> | <img src="https://github.com/JiiminHa.png" width=120 /> | <img src="https://github.com/kangcheolung.png" width=120 /> | <img src="https://github.com/hyunj24.png" width=120 /> | <img src="https://github.com/JikkeunWoo.png" width=120 /> |
| :-------: | :-------: | :-------: | :-------: | :-------: | :-------: |
| [김민아](https://github.com/kimminna) | [양희정](https://github.com/DandelionQZ) | [하지민](https://github.com/JiiminHa) | [강철웅](https://github.com/kangcheolung) | [박현정](https://github.com/hyunj24) | [우재원](https://github.com/JikkeunWoo) |
| [ 11기 FE ] 교육팀장 | [ 11기 FE ] 교육팀장 | [ 11기 FE ] 교육팀장 | [ 12기 BE ] 교육팀원 | [ 12기 BE ] 교육팀원 | [ 12기 PM ] 교육팀원 |

# What we Studied

|       |     주제      | 발표자 |       날짜       |
| :---: | :-----------: | :----- | :--------------: |
| 1주차 | Git | 양희정 | 2025년 9월 5일 |
| 2주차 | Agile | 하지민 | 2025년 9월 19일 |
| 3주차 | 미정 | 미정 | 2025년 10월 31일 |
| 4주차 | 미정 | 미정 | 2025년 11월 7일 |
| 5주차 | 미정 | 미정 | 2025년 11월 14일 |
| 6주차 | 미정 | 김민아 | 2025년 12월 26일 |
| 7주차 | 미정 | 미정 | 2026년 1월 46일 |
| 8주차 | 미정 | 미정 | 2026년 1월 30일 |
| 9주차 | 미정 | 미정 | 2026년 2월 6일 |
| 10주차 | 골든 포테이토 | 운영진 | 2026년 2월 6일 |

# Rules

- 발표자는 발표전 주 수요일 정기 회의때 주제를 선정해 팀원들에게 안내한다.
- 발표자는 발표주차 화요일 18시까지 발표자료 초안, 대본을 팀원들에게 필수로 공유한다.
- 교육팀원들은 매주 수요일 회의전까지 발표자료를 검토하고, 관련된 CS퀴즈 각각 2-3문제씩 제작한다.
- 매주 수요일 정규회의때 CS퀴즈 10문제를 선정한다.

# Directory Structure

```plainText
│
├─ 12th-Educatoin
│     │
│     ├─ Week01 (dir)
│     │     │
│     │     ├─  kimminna (dir) // 해당 주차 발표자
│     │     │    ├─ 주제.md // 해당 주차 정리 내용. 파일명은 확장자는 `.md`
│     │     │    └─ `기타 소스 코드 및 자료들`
│     │     │
│     │     ├─  DandelionQZ (dir) // 발표자 외의 팀원들 (Option)
│     │     │    ├─ 주제.md
│     │     │    └─ `기타 자료`//참고한 자료들
│     │     │
│     │     ├─  JiiminHa (dir) // 발표자 외의 팀원들 (Option)
│     │     │    ├─ 주제.md
│     │     │    └─ `기타 자료`//참고한 자료들
│     │     │
│     │     └─ 최종 발표 자료.pdf //확장자명은 .pdf
│     │
│     │
│     ├─ .. 이하 동일
│
│
```

## Git Rule

- git clone <주소>를 통해 Repository를 clone 받는다.
- `git checkout -b 본인 핸들명-주차` 명령어를 통해 본인 브랜치를 생성한다.
- 해당 브랜치에서 작업 후 커밋한다. (절대! main 브랜치에서 작업하지 않는다.)
- 작업 후 main 브랜치로 PR을 날린다.
- 작업 후 로컬에서 `git checkout main`로 브랜치를 돌린 후 `git branch -D 본인 핸들명-주차`을 통해 로컬 브랜치를 삭제한다.
- 팀원들은 해당 PR에 대해 피드백, 리뷰를 남긴다.
- 작업 후 `교육팀장`은 `Squash and Merge`를 통해 PR을 merge하고 원격 브랜치를 삭제한다.
- 다시 작업을 시작하고 싶으면 main 브랜치의 최신 내용을 pull받은 후 `git checkout -b 본인 핸들명-주차`으로 브랜치를 로컬에서 생성해 작업한다.<br>

## Convention

발표자료 업로드: `docs: [000] n주차 발표자료 업로드`<br>
발표외 공부자료 업로드: `docs: [000] n주차 공부자료 업로드`<br>

### Pull request convention

[OOO] n주차 \_\_자료 제출합니다. (발표 or 공부)
