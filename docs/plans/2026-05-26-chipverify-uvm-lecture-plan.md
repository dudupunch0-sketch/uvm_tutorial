# ChipVerify UVM 기반 한국어 HTML 강의자료 제작 계획

> **For Hermes:** Planning only. Do not implement the lecture pages from this plan until the user explicitly asks for execution.

**Goal:** 기존 `lectures/day*.html`와 같은 학습용 HTML workbook 형식으로, ChipVerify UVM tutorial 흐름을 바탕으로 한 별도 한국어 강의자료 세트를 만든다.

**Architecture:** 기존 repo-grounded 강의(`lectures/`)와 섞지 않고, ChipVerify 기반 강의는 별도 출력 폴더에 둔다. ChipVerify 원문은 통째로 복제하지 않고, 각 Day 페이지에서 원문 URL을 명시하고 한국어 설명/퀴즈/실습/LLM prompt를 새로 작성한다.

**Tech Stack:** 정적 HTML/CSS/vanilla JS, 로컬 SystemVerilog/UVM syntax highlighting, preview HTTP server, Node.js inline-script syntax check.

---

## 1. 새 출력 폴더

새 강의자료 폴더:

```text
/home/dudupunch0/company/uvm-practical-learning/lectures_chipverify_uvm/
```

예상 구조:

```text
lectures_chipverify_uvm/
  index.html
  day0_chipverify_uvm_orientation.html
  day1_uvm_overview_ovm_to_uvm.html
  day2_installation_hello_uvm.html
  ...
  day30_interview_review_and_next_steps.html
  sources/
    chipverify_uvm_source_map.json
    chipverify_uvm_curriculum.json
  assets/
    README.md
```

선택적으로 새 project-local skill도 만든다:

```text
/home/dudupunch0/company/uvm-practical-learning/skills/chipverify-uvm-lecture-builder/SKILL.md
/home/dudupunch0/company/uvm-practical-learning/skills/chipverify-uvm-lecture-builder/references/curriculum.md
```

기존 강의 폴더는 그대로 유지:

```text
/home/dudupunch0/company/uvm-practical-learning/lectures/
```

Preview URL 예상:

```text
http://127.0.0.1:8765/lectures_chipverify_uvm/index.html
```

---

## 2. 현재 확인한 외부 source 구조

사용자가 지정한 시작점:

```text
https://chipverify.com/tutorials/uvm/
```

확인 결과, 상세 tutorial 링크들은 `https://chipverify.com/tutorials/uvm/*`가 아니라 주로 아래 형태로 연결된다:

```text
https://chipverify.com/uvm/<topic-slug>
```

따라서 source scope는 다음 둘을 모두 포함한다:

1. `https://chipverify.com/tutorials/uvm/`
2. 위 페이지에서 연결되는 `https://chipverify.com/uvm/...` UVM tutorial pages

중요한 사용 원칙:

- ChipVerify 페이지를 wholesale mirror하지 않는다.
- 긴 원문 문단이나 전체 code block을 복사하지 않는다.
- 각 Day는 원문 URL을 출처로 링크하고, 설명은 한국어로 새로 재구성한다.
- 필요한 경우 짧은 용어/짧은 code idiom만 인용하고, 가능하면 repo-local 또는 직접 작성한 mini example로 대체한다.
- 요청당 crawl은 rate-limit하고, source inventory와 요약 metadata만 저장한다.

---

## 3. 강의자료 page contract

기존 `uvm-practical-lecture-builder` 형식을 유지하되, source가 repo file이 아니라 ChipVerify tutorial URL이라는 점만 바꾼다.

각 Day HTML에 포함할 항목:

1. 한국어 제목, 목표, 완료 기준
2. 오늘 읽을 ChipVerify 원문 링크 카드
3. 3개의 mental-model 카드
4. 읽는 순서 trace
5. 핵심 SystemVerilog/UVM syntax 또는 mini example 카드
6. source mapping 카드
   - 원문 URL
   - 관련 ChipVerify topic title
   - 이 Day에서 재구성한 핵심 질문
7. checklist with localStorage progress
8. quiz
9. 작은 실습 또는 사고 실험
10. LLM에게 이어서 질문하기 위한 prompt box

기존 repo-grounded 강의와 다른 점:

- `source excerpt`는 repo line range 대신 `source URL + topic summary + short re-authored example`로 대체한다.
- 원문 code를 길게 복사하지 않고, 직접 만든 compact example을 사용한다.
- 각 페이지 마지막에 “원문과 함께 확인할 질문” 섹션을 둔다.

---

## 4. 제안 커리큘럼: 31일 구성

너무 잘게 80개 page를 1:1로 만들기보다, 학습 흐름 기준으로 2~4개 ChipVerify topic을 하루에 묶는다.

### Module A. Orientation and first UVM run

#### Day 0. ChipVerify UVM course orientation

Sources:
- `https://chipverify.com/tutorials/uvm/`

Goal:
- 이 강의 세트의 사용법, 원문 링크를 읽는 법, 기존 repo-grounded 강의와의 차이를 이해한다.

Output file:
- `lectures_chipverify_uvm/day0_chipverify_uvm_orientation.html`

#### Day 1. UVM overview: OVM에서 UVM까지

Sources:
- `https://chipverify.com/tutorials/uvm/`
- `https://chipverify.com/uvm/uvm-introduction`

Goal:
- UVM이 왜 생겼고, testbench를 어떤 추상화로 나누는지 이해한다.

Output file:
- `day1_uvm_overview_ovm_to_uvm.html`

#### Day 2. UVM installation and Hello UVM

Sources:
- `https://chipverify.com/uvm/uvm-installation`
- `https://chipverify.com/uvm/uvm-hello-world`

Goal:
- `import uvm_pkg::*`, `` `include "uvm_macros.svh" ``, `run_test()`의 최소 실행 흐름을 이해한다.

Output file:
- `day2_installation_hello_uvm.html`

### Module B. Base classes and object/component mental model

#### Day 3. Base classes: object vs component

Sources:
- `https://chipverify.com/uvm/base-classes`
- `https://chipverify.com/uvm/uvm-root`

Goal:
- UVM class hierarchy에서 `uvm_root`, `uvm_object`, `uvm_component`의 역할을 구분한다.

Output file:
- `day3_base_classes_root_object_component.html`

#### Day 4. uvm_object lifecycle and utilities

Sources:
- `https://chipverify.com/uvm/uvm-object`
- `https://chipverify.com/uvm/uvm-object-copy-clone`
- `https://chipverify.com/uvm/uvm-object-compare`
- `https://chipverify.com/uvm/uvm-object-print`
- `https://chipverify.com/uvm/uvm-object-pack-unpack`

Goal:
- transaction 객체가 왜 object 계층에 있고, copy/clone/compare/print/pack이 왜 필요한지 이해한다.

Output file:
- `day4_uvm_object_lifecycle_utilities.html`

#### Day 5. uvm_component hierarchy and phases preview

Sources:
- `https://chipverify.com/uvm/uvm-component`
- `https://chipverify.com/uvm/uvm-testbench-top`
- `https://chipverify.com/uvm/uvm-test`

Goal:
- component tree, parent/child 관계, testbench top과 test class의 연결을 이해한다.

Output file:
- `day5_uvm_component_testbench_top.html`

### Module C. Testbench components

#### Day 6. Environment and agent composition

Sources:
- `https://chipverify.com/uvm/uvm-environment`
- `https://chipverify.com/uvm/uvm-agent`

Goal:
- env와 agent가 reusable verification component를 구성하는 방법을 이해한다.

Output file:
- `day6_environment_and_agent.html`

#### Day 7. Driver, monitor, subscriber

Sources:
- `https://chipverify.com/uvm/uvm-driver`
- `https://chipverify.com/uvm/uvm-monitor`
- `https://chipverify.com/uvm/uvm-subscriber`

Goal:
- active stimulus path와 passive observation path를 구분한다.

Output file:
- `day7_driver_monitor_subscriber.html`

#### Day 8. Sequencer and scoreboard

Sources:
- `https://chipverify.com/uvm/uvm-sequencer`
- `https://chipverify.com/uvm/uvm-scoreboard`

Goal:
- sequencer가 sequence와 driver 사이에서 하는 일, scoreboard가 expected/actual을 비교하는 위치를 이해한다.

Output file:
- `day8_sequencer_and_scoreboard.html`

### Module D. Phases and simulation lifetime

#### Day 9. UVM phases

Sources:
- `https://chipverify.com/uvm/uvm-phases`

Goal:
- build/connect/end_of_elaboration/start_of_simulation/run/extract/check/report/final phase의 의도를 구분한다.

Output file:
- `day9_uvm_phases.html`

#### Day 10. Objection and user-defined phases

Sources:
- `https://chipverify.com/uvm/uvm-objection`
- `https://chipverify.com/uvm/uvm-user-defined-phase`

Goal:
- run phase가 언제 끝나는지, objection이 왜 필요한지 이해한다.

Output file:
- `day10_objection_and_custom_phase.html`

### Module E. Sequences and stimulus generation

#### Day 11. Sequence basics

Sources:
- `https://chipverify.com/uvm/uvm-sequence`
- `https://chipverify.com/uvm/how-to-create-and-use-a-sequence`

Goal:
- `uvm_sequence`, sequence item, `body()`의 기본 구조를 이해한다.

Output file:
- `day11_sequence_basics.html`

#### Day 12. Starting sequences and macros

Sources:
- `https://chipverify.com/uvm/how-to-execute-sequences-via-start-method`
- `https://chipverify.com/uvm/how-to-execute-sequences-via-uvm-do-macros`
- `https://chipverify.com/uvm/uvm-do-macros`
- `https://chipverify.com/uvm/sequence-action-macros-for-pre-existing-items`

Goal:
- `start()`와 `` `uvm_do `` 계열 macro의 차이를 이해하고, macro 사용의 장단점을 판단한다.

Output file:
- `day12_sequence_start_and_macros.html`

#### Day 13. Virtual sequence, virtual sequencer, sequence library

Sources:
- `https://chipverify.com/uvm/uvm-virtual-sequence`
- `https://chipverify.com/uvm/uvm-virtual-sequencer`
- `https://chipverify.com/uvm/uvm-sequence-library`
- `https://chipverify.com/uvm/uvm-sequence-arbitration`

Goal:
- multi-agent coordination과 arbitration 개념을 이해한다.

Output file:
- `day13_virtual_sequence_and_arbitration.html`

#### Day 14. Transaction object and driver handshake

Sources:
- `https://chipverify.com/uvm/uvm-transaction-object`
- `https://chipverify.com/uvm/uvm-using-get-next-item`
- `https://chipverify.com/uvm/driver-using-get-and-put`

Goal:
- sequence item이 driver까지 전달되는 handshake model을 이해한다.

Output file:
- `day14_transaction_and_driver_handshake.html`

### Module F. TLM communication

#### Day 15. TLM overview and blocking put/get

Sources:
- `https://chipverify.com/uvm/uvm-tlm`
- `https://chipverify.com/uvm/uvm-tlm-blocking-put-port`
- `https://chipverify.com/uvm/uvm-tlm-blocking-get-port`

Goal:
- port/export/imp, blocking put/get의 mental model을 만든다.

Output file:
- `day15_tlm_blocking_put_get.html`

#### Day 16. TLM FIFO and example

Sources:
- `https://chipverify.com/uvm/uvm-tlm-fifo`
- `https://chipverify.com/uvm/uvm-tlm-example`

Goal:
- FIFO가 producer/consumer를 느슨하게 연결하는 방법을 이해한다.

Output file:
- `day16_tlm_fifo_and_example.html`

#### Day 17. Analysis port, sockets, nonblocking TLM

Sources:
- `https://chipverify.com/uvm/uvm-tlm-analysis-port`
- `https://chipverify.com/uvm/uvm-tlm-sockets`
- `https://chipverify.com/uvm/using-decl-macro-in-tlm`
- `https://chipverify.com/uvm/uvm-tlm-nonblocking-put-port`
- `https://chipverify.com/uvm/uvm-tlm-port-export-imp`
- `https://chipverify.com/uvm/uvm-tlm-nonblocking-get-port`

Goal:
- monitor에서 scoreboard/coverage로 fanout하는 analysis path와 nonblocking TLM 차이를 이해한다.

Output file:
- `day17_analysis_port_and_nonblocking_tlm.html`

### Module G. Configuration, factory, resource DB

#### Day 18. Factory override

Sources:
- `https://chipverify.com/uvm/uvm-factory-override`

Goal:
- source를 수정하지 않고 test에서 type/instance override하는 이유를 이해한다.

Output file:
- `day18_factory_override.html`

#### Day 19. Configure components and config_db

Sources:
- `https://chipverify.com/uvm/configure-components`
- `https://chipverify.com/uvm/uvm-config-db`
- `https://chipverify.com/uvm/uvm-config-db-examples`

Goal:
- interface handle, knobs, env settings를 config_db로 전달하는 흐름을 이해한다.

Output file:
- `day19_configure_components_and_config_db.html`

#### Day 20. Resource database

Sources:
- `https://chipverify.com/uvm/understanding-the-resource-database`

Goal:
- config_db와 resource DB의 관계와 beginner가 피해야 할 남용 패턴을 이해한다.

Output file:
- `day20_resource_database.html`

### Module H. RAL and register verification

#### Day 21. RAL overview and register model classes

Sources:
- `https://chipverify.com/uvm/uvm-register-layer`
- `https://chipverify.com/uvm/uvm-register-model`

Goal:
- register abstraction layer가 bus transaction과 register intent를 분리하는 이유를 이해한다.

Output file:
- `day21_ral_overview_and_model_classes.html`

#### Day 22. Register environment and connection

Sources:
- `https://chipverify.com/uvm/uvm-register-environment`
- `https://chipverify.com/uvm/connecting-register-env`

Goal:
- adapter, predictor, sequencer 연결 흐름을 이해한다.

Output file:
- `day22_register_environment_connection.html`

#### Day 23. Backdoor access and register model example

Sources:
- `https://chipverify.com/uvm/uvm-register-backdoor-access`
- `https://chipverify.com/uvm/uvm-register-model-example`

Goal:
- frontdoor/backdoor의 차이와 RAL example의 전체 실행 흐름을 이해한다.

Output file:
- `day23_ral_backdoor_and_example.html`

### Module I. Reporting, callbacks, events, macros

#### Day 24. Reporting and printer/comparer policy

Sources:
- `https://chipverify.com/uvm/reporting-classes`
- `https://chipverify.com/uvm/report-functions`
- `https://chipverify.com/uvm/uvm-printer`
- `https://chipverify.com/uvm/uvm-comparer`

Goal:
- report verbosity/severity, object print/compare policy를 debugging 도구로 이해한다.

Output file:
- `day24_reporting_printer_comparer.html`

#### Day 25. Callback and events

Sources:
- `https://chipverify.com/uvm/uvm-callback`
- `https://chipverify.com/uvm/uvm-event`
- `https://chipverify.com/uvm/uvm-event-pool`

Goal:
- callback과 event를 통해 component를 직접 수정하지 않고 hook을 추가하는 방식을 이해한다.

Output file:
- `day25_callback_and_events.html`

#### Day 26. Utility and field macros, HDL access, singleton

Sources:
- `https://chipverify.com/uvm/uvm-utility-field-macros`
- `https://chipverify.com/uvm/uvm-field-macros`
- `https://chipverify.com/uvm/uvm-hdl-access-routines`
- `https://chipverify.com/uvm/uvm-singleton-object`

Goal:
- macro 자동화의 편의성과 숨겨지는 비용, HDL access routine의 사용 경계를 이해한다.

Output file:
- `day26_macros_hdl_access_singleton.html`

### Module J. Reuse, examples, review

#### Day 27. Reusable verification components

Sources:
- `https://chipverify.com/uvm/reusable-verification-components`
- `https://chipverify.com/uvm/verification-components`

Goal:
- reusable VIP를 설계/사용할 때의 boundary, config, sequence strategy를 이해한다.

Output file:
- `day27_reusable_verification_components.html`

#### Day 28. Full verification testbench example

Sources:
- `https://chipverify.com/uvm/uvm-verification-testbench-example`

Goal:
- 지금까지 배운 component, phase, sequence, TLM, scoreboard가 한 testbench에서 어떻게 연결되는지 trace한다.

Output file:
- `day28_full_verification_testbench_example.html`

#### Day 29. Testbench examples 1 and 2

Sources:
- `https://chipverify.com/uvm/uvm-testbench-example-1`
- `https://chipverify.com/uvm/uvm-testbench-example-2`

Goal:
- 예제 간 구조 차이를 비교하고, 직접 확장할 지점을 찾는다.

Output file:
- `day29_testbench_examples_comparison.html`

#### Day 30. Interview review and next steps

Sources:
- `https://chipverify.com/uvm/uvm-interview-questions-set-1`
- `https://chipverify.com/uvm/uvm-interview-questions-set-2`
- `https://chipverify.com/uvm/uvm-interview-questions-set-3`
- `https://chipverify.com/uvm/uvm-interview-questions-set-4`
- `https://chipverify.com/uvm-reference`
- `https://www.accellera.org/downloads/standards/uvm`

Goal:
- 핵심 개념을 interview-style 질문으로 복습하고, Accellera UVM reference로 넘어갈 준비를 한다.

Output file:
- `day30_interview_review_and_next_steps.html`

---

## 5. 구현 단계 계획

### Task 1. Source inventory 작성

Objective:
- ChipVerify UVM 시작 페이지에서 tutorial topic URL/title 목록을 뽑아 `source_map`으로 정리한다.

Files:
- Create: `lectures_chipverify_uvm/sources/chipverify_uvm_source_map.json`
- Create: `lectures_chipverify_uvm/sources/chipverify_uvm_curriculum.json`

Steps:
1. `https://chipverify.com/tutorials/uvm/`에서 UVM 관련 링크 목록만 수집한다.
2. `https://chipverify.com/uvm/...` topic URL을 dedupe한다.
3. 각 URL에 title, slug, module, day assignment를 붙인다.
4. 원문 content는 저장하지 않는다. 필요하면 요약/metadata만 저장한다.

Verification:
- JSON parse 성공
- 모든 assigned source URL이 curriculum day에 최소 1번 연결됨
- source map에 raw full article body가 들어가지 않음

### Task 2. ChipVerify lecture-builder skill 작성

Objective:
- 기존 `uvm-practical-lecture-builder`와 같은 page format을 ChipVerify URL-source용으로 고정한다.

Files:
- Create: `skills/chipverify-uvm-lecture-builder/SKILL.md`
- Create: `skills/chipverify-uvm-lecture-builder/references/curriculum.md`

Steps:
1. page contract를 `source URL card` 중심으로 작성한다.
2. copyright/attribution guardrail을 명시한다.
3. validation checklist를 추가한다.

Verification:
- skill frontmatter YAML parse 가능
- `references/curriculum.md`가 Day 0~30 전체를 포함

### Task 3. Static template 확정

Objective:
- 기존 HTML lecture 스타일을 유지하면서 ChipVerify source card를 표시하는 reusable template을 확정한다.

Files:
- Read: `lectures/day1_uvm_mental_model.html`
- Create: `lectures_chipverify_uvm/day0_chipverify_uvm_orientation.html`

Steps:
1. 기존 강의의 layout, color, checklist, quiz, prompt box 구조를 읽는다.
2. source excerpt 영역을 `원문 링크 / 핵심 질문 / 직접 작성 mini example` 영역으로 바꾼다.
3. 외부 CSS/JS 없이 self-contained HTML로 만든다.

Verification:
- `node --check`로 inline script syntax 확인
- `day0`가 remote CSS/JS asset을 참조하지 않음
- localStorage key가 기존 `lectures/`와 충돌하지 않음

### Task 4. Day 1~10 생성

Objective:
- foundation, base class, component, phase 영역을 먼저 만든다.

Files:
- Create: `lectures_chipverify_uvm/day1_*.html` through `day10_*.html`
- Modify: `lectures_chipverify_uvm/index.html`

Steps:
1. Day별 source URL을 열고 topic structure를 확인한다.
2. 한국어 explanation을 새로 작성한다.
3. 각 Day마다 mini UVM snippet 또는 trace diagram을 직접 작성한다.
4. checklist/quiz/practice/LLM prompt를 추가한다.

Verification:
- Day 1~10 HTML 존재
- 각 page에 source URL 링크가 1개 이상 있음
- 각 page에 quiz/checklist/prompt가 있음
- internal index link가 모두 존재

### Task 5. Day 11~20 생성

Objective:
- sequence/stimulus, TLM, factory/config/resource DB 영역을 만든다.

Files:
- Create: `lectures_chipverify_uvm/day11_*.html` through `day20_*.html`
- Modify: `lectures_chipverify_uvm/index.html`

Verification:
- Day 11~20 HTML 존재
- sequence/TLM/config 주요 용어가 glossary 카드에 포함
- `uvm_do` macro 사용시 장단점/주의점을 설명

### Task 6. Day 21~30 생성

Objective:
- RAL, reporting, callback/event, reusable VC, full example, interview review를 만든다.

Files:
- Create: `lectures_chipverify_uvm/day21_*.html` through `day30_*.html`
- Modify: `lectures_chipverify_uvm/index.html`

Verification:
- Day 21~30 HTML 존재
- RAL 관련 Day는 frontdoor/backdoor/adapter/predictor 용어를 구분
- final review Day가 전체 curriculum으로 역링크 제공

### Task 7. Index와 navigation 완성

Objective:
- `lectures_chipverify_uvm/index.html`을 학습 dashboard처럼 만든다.

Files:
- Modify: `lectures_chipverify_uvm/index.html`

Steps:
1. 전체 Day 목록을 module별로 그룹화한다.
2. 각 Day 카드에 source count, 목표, 예상 소요 시간을 표시한다.
3. 기존 repo-grounded 강의 `lectures/index.html`로 가는 cross-link를 추가한다.

Verification:
- index의 모든 href target이 존재
- Day page에서 previous/next/index navigation이 동작

### Task 8. Validation script 또는 one-off 검증 실행

Objective:
- 생성물이 self-contained HTML lecture set로 열리는지 검증한다.

Checks:
1. HTML 파일 수 확인: `index.html + day0~day30 = 32 files`
2. 모든 internal href target 존재
3. remote CSS/JS asset 없음
4. inline JavaScript `node --check` 통과
5. source URL 링크 목록 존재
6. long copied text guardrail: ChipVerify 원문 문단을 대량 복제하지 않았는지 spot check
7. preview server에서 `http://127.0.0.1:8765/lectures_chipverify_uvm/index.html` HTTP 200
8. 대표 페이지 HTTP 200:
   - `day1_uvm_overview_ovm_to_uvm.html`
   - `day15_tlm_blocking_put_get.html`
   - `day21_ral_overview_and_model_classes.html`
   - `day30_interview_review_and_next_steps.html`

---

## 6. 권장 학습 운영 방식

각 Day를 공부할 때 순서:

1. 생성된 한국어 Day page를 먼저 읽는다.
2. Day page의 source URL 버튼으로 ChipVerify 원문을 연다.
3. 원문의 code/example를 직접 눈으로 확인한다.
4. Day page의 quiz를 풀고, 틀린 항목을 LLM prompt box로 질문한다.
5. 가능하면 기존 `lectures/` repo-grounded 강의에서 대응되는 Day를 찾아 실제 repo 코드와 비교한다.

예시 연결:

```text
ChipVerify Day 2 Hello UVM
  -> existing lectures Day 2 top module/run_test

ChipVerify Day 7 Driver/Monitor
  -> existing lectures Day 6 interface/driver
  -> existing lectures Day 7 monitor/analysis port

ChipVerify Day 18 Factory
  -> existing lectures Day 10 config_db/factory

ChipVerify Day 21~23 RAL
  -> existing lectures Day 15 RAL/register model
```

---

## 7. Risks / tradeoffs

1. 저작권/콘텐츠 재배포 위험
   - 완화: 원문을 복제하지 않고, 링크+재구성 설명+짧은 직접 작성 예제로 구성한다.

2. ChipVerify URL 구조 변경
   - 완화: `sources/chipverify_uvm_source_map.json`에 title/URL/last_checked를 기록하고, 생성 시 링크 검증을 수행한다.

3. 31일 분량이 길 수 있음
   - 완화: index에서 “빠른 14일 코스”와 “전체 31일 코스”를 둘 다 표시할 수 있다.

4. 기존 repo-grounded 강의와 중복
   - 완화: ChipVerify 세트는 개념 중심, 기존 `lectures/` 세트는 실제 repo source-reading 중심으로 역할을 분리한다.

5. 상용 simulator 부재
   - 완화: 이 host에서는 실행 검증이 아니라 code-reading/mental-model 학습자료로 다룬다. 실제 simulator 실습은 사용자의 EDA 환경에서 수행한다.

---

## 8. Open questions before execution

1. 총 분량을 31일 전체 코스로 만들지, 14일 압축 코스로 줄일지?
   - Default: 31일 전체 코스 생성, index에 “빠른 코스” 표시.

2. ChipVerify 원문 code를 어느 정도까지 페이지 안에 포함할지?
   - Default: 긴 code block은 포함하지 않고, 직접 작성한 compact mini example만 포함.

3. 기존 `lectures/index.html`에서 새 폴더로 링크를 걸지?
   - Default: 새 `lectures_chipverify_uvm/index.html`만 만들고, 기존 index는 건드리지 않음. 사용자가 원하면 나중에 cross-link 추가.

4. 한국어 설명 톤을 Day 0~21 기존 강의와 완전히 맞출지, 더 교과서식으로 할지?
   - Default: 기존 강의와 동일한 workbook 톤.

---

## 9. Definition of done

완료 조건:

- `lectures_chipverify_uvm/index.html` 존재
- `lectures_chipverify_uvm/day0_*.html` through `day30_*.html` 존재
- 각 Day page가 ChipVerify source URL을 명시
- 각 Day page가 한국어 설명, mental model, trace, mini example, checklist, quiz, practice, LLM prompt를 포함
- 원문 대량 복제 없음
- inline JS syntax check 통과
- internal links 검증 통과
- preview URL HTTP 200
- 기존 `lectures/` 강의자료는 변경하지 않음
