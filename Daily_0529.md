# Daily 0529 - UVM 학습 프로젝트 진행상황

기준 시각: 2026-05-29 07:27:31 UTC

## 프로젝트 위치

- Repo: `/home/dudupunch0/company/uvm-practical-learning`
- Branch: `master`
- Remote tracking: `origin/master`

## 오늘 기준 목표

SystemVerilog UVM 검증 환경을 LLM과 함께 단계적으로 공부할 수 있도록, 기존 Practical-UVM-Step-By-Step repo와 ChipVerify UVM tutorial을 각각 다른 관점의 한국어 HTML workbook으로 정리한다.

## 완료된 작업

### 1. repo 기반 학습 자료

- `UVM_LEARNING_CHECKLIST.ko.md` 작성
  - 중심 예제: `Part_2-Putting_it_all_Together`
  - 기본 흐름: `top module + run_test -> test -> env -> agent -> sequence/sequencer -> driver/interface -> monitor -> scoreboard/coverage`
- `lectures/index.html` 생성
- `lectures/day*.html` 생성
  - Day 0 orientation
  - Day 1~21 repo source-reading workbook
  - Day 0은 기존/한국어 variant가 함께 존재한다.
- 각 page에 포함된 요소
  - 목표/완료 기준
  - mental model 카드
  - 실제 repo source excerpt
  - SystemVerilog/UVM syntax highlighting
  - checklist
  - quiz
  - 작은 실습
  - LLM 질문 prompt
- project-local skill 생성
  - `skills/uvm-practical-lecture-builder/SKILL.md`
  - `skills/uvm-practical-lecture-builder/references/curriculum.md`

### 2. ChipVerify 기반 학습 자료

- 실행 전 plan 작성
  - `docs/plans/2026-05-26-chipverify-uvm-lecture-plan.md`
- 새 강의자료 폴더 생성
  - `lectures_chipverify_uvm/`
- `lectures_chipverify_uvm/index.html` 생성
- `lectures_chipverify_uvm/day0_*.html` through `day30_*.html` 생성
  - Day 0~30, 총 31일 구성
  - 전체 HTML 파일 수: 32개
- source/curriculum metadata 생성
  - `lectures_chipverify_uvm/sources/chipverify_uvm_source_map.json`
  - `lectures_chipverify_uvm/sources/chipverify_uvm_curriculum.json`
- source inventory 기준
  - 시작 URL: `https://chipverify.com/tutorials/uvm/`
  - 연결 topic: 주로 `https://chipverify.com/uvm/<topic-slug>` 형태
  - source URL/title inventory: 80개
- 저작권/재배포 guardrail
  - ChipVerify 원문 article body를 mirror하지 않음
  - 긴 원문 code block을 복사하지 않음
  - 각 Day page는 원문 URL을 source card로 링크하고, 한국어 설명과 compact UVM 예제는 직접 작성한 형태로 구성
- project-local skill 생성
  - `skills/chipverify-uvm-lecture-builder/SKILL.md`
  - `skills/chipverify-uvm-lecture-builder/references/curriculum.md`

### 3. 한국어 문서/번역 자료

- 원본 텍스트 문서의 한국어 번역본 다수 생성
- manifest 작성/최신화
  - `TRANSLATION_MANIFEST_KR.md`
- root Korean README 최신화
  - `README_KR.md`
- checklist 최신화
  - `UVM_LEARNING_CHECKLIST.ko.md`
  - `UVM_LEARNING_CHECKLIST.ko_KR.md`

## 검증 결과

### HTML/workbook 검증

검증 통과 항목:

- `lectures_chipverify_uvm/` HTML 파일 수: 32개
- `lectures_chipverify_uvm/` Day page 수: 31개
- `chipverify_uvm_source_map.json` JSON parse 성공
- `chipverify_uvm_curriculum.json` JSON parse 성공
- inline JavaScript `node --check` 통과
- internal href link 검증 통과
- remote CSS/JS asset 없음 확인
- 대표 page HTTP 200 확인 완료 이력
  - `lectures_chipverify_uvm/index.html`
  - `day1_uvm_overview_ovm_to_uvm.html`
  - `day15_tlm_blocking_put_get.html`
  - `day21_ral_overview_and_model_classes.html`
  - `day30_interview_review_and_next_steps.html`

주의:

- browser 자동 snapshot은 현재 host에 Chrome이 없어 수행하지 못했다.
- 현재 시점에는 `127.0.0.1:8765` preview listener가 떠 있지 않다. 필요하면 repo root에서 다시 실행한다.

```bash
python3 -m http.server 8765 --bind 127.0.0.1
```

## 현재 산출물 요약

### 주요 entry point

- Repo 기반 강의 index:
  - `lectures/index.html`
- ChipVerify 기반 강의 index:
  - `lectures_chipverify_uvm/index.html`
- 학습 체크리스트:
  - `UVM_LEARNING_CHECKLIST.ko.md`
- 한국어 README:
  - `README_KR.md`
- 번역/학습 artifact manifest:
  - `TRANSLATION_MANIFEST_KR.md`

### 추천 학습 순서

1. `README_KR.md`에서 이 로컬 프로젝트에 추가된 자료 위치를 확인한다.
2. `UVM_LEARNING_CHECKLIST.ko.md`의 전체 지도와 현재 진행 상태를 본다.
3. `lectures/index.html`에서 repo 실제 code-reading Day 0~3을 먼저 본다.
4. 개념 보강이 필요하면 `lectures_chipverify_uvm/index.html`에서 대응 Day를 본다.
5. 각 Day page의 prompt box를 복사해 LLM에게 내 요약/질문을 넣고 복습한다.

## 아직 남은 일

- 실제 학습 진행은 아직 시작 단계다. 자료 생성 완료와 학습 완료는 다르다.
- 다음 실질 학습 slice는 다음 중 하나가 적절하다.
  1. `lectures/index.html` 기준 Day 0~3을 사용자와 함께 진행
  2. ChipVerify workbook Day 0~2로 UVM 개념/Hello UVM 흐름을 먼저 복습
  3. 두 workbook을 cross-reference하는 “빠른 14일 코스”를 별도 문서로 정리
- 상용 simulator가 없는 현재 host에서는 실행 검증 대신 code-reading 중심으로 진행한다.
- 실제 compile/run 실습은 VCS/Questa/Xcelium 또는 EDA Playground 같은 환경이 준비되면 진행한다.

## Git 상태 메모

현재 생성/수정된 문서와 HTML artifact는 아직 stage/commit하지 않은 working tree 변경으로 남아 있다. 기존 repo에는 다른 한국어 번역 문서와 lecture artifact도 untracked 상태로 함께 존재한다. commit할 때는 의도한 문서/강의자료만 선별해서 stage해야 한다.
