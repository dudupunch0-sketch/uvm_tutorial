# SystemVerilog UVM 학습 체크리스트

이 문서는 `Practical-UVM-Step-By-Step` 저장소를 이용해서 SystemVerilog UVM 검증 환경을 단계적으로 공부하기 위한 학습 지도입니다.

선택한 repo:
- https://github.com/Practical-UVM-Step-By-Step/Practical-UVM-Step-By-Step

로컬 위치:
- `/home/dudupunch0/company/uvm-practical-learning`

중심 예제:
- `/home/dudupunch0/company/uvm-practical-learning/Part_2-Putting_it_all_Together`

왜 이 repo를 선택했나:
- UVM testbench의 표준 구성요소가 거의 모두 들어 있다.
- `transaction -> sequence -> sequencer -> driver -> interface -> monitor -> scoreboard -> coverage -> env -> test` 흐름을 실제 코드로 볼 수 있다.
- README 자체가 Part 2를 기준 예제로 삼고, 다른 예제들은 Part 2에서 바뀐 파일 중심으로 보라고 안내한다.
- 고급 주제로 `config_db`, phase callback, RAL/register, reactive sequence, coverage closure 예제가 있다.

주의:
- 이 repo는 UVM-1.2 + VCS 중심의 오래된 예제다.
- 현재 이 머신에는 `vcs`, `vsim`, `xrun`, `iverilog`, `verilator`가 PATH에 없다.
- 따라서 처음에는 실행보다 코드 구조 이해, 파일 간 연결 추적, 작은 수정 과제 설계 중심으로 학습한다.
- 시뮬레이션은 나중에 VCS/Questa/Xcelium 또는 EDA Playground 같은 환경이 생기면 진행한다.

---

## 학습 방식

각 단계마다 다음 순서로 진행한다.

1. 내가 핵심 개념을 짧게 설명한다.
2. 해당 repo의 실제 파일을 함께 본다.
3. 파일의 역할, 주요 class/task/function, 다른 파일과의 연결을 정리한다.
4. 체크 질문 3~5개를 낸다.
5. 사용자가 답하면 내가 채점/보충한다.
6. 작은 수정 실습 또는 사고 실험을 제시한다.

사용자 진행 명령 예시:
- `다음` : 다음 체크리스트 항목으로 진행
- `퀴즈` : 현재 항목에 대한 확인 문제 요청
- `다시 설명` : 현재 개념을 더 쉽게 다시 설명
- `파일 열어봐` : 관련 파일을 더 자세히 분석
- `실습 내줘` : 현재 개념 기반 작은 과제 요청

---

## 전체 지도

UVM testbench의 큰 흐름은 다음과 같다.

```text
DUT signal
  ^
  |
interface
  ^                    monitor -> analysis_port -> scoreboard / coverage
  |                       |
driver <- sequencer <- sequence
  ^
  |
agent
  ^
  |
env
  ^
  |
test
  ^
  |
top module + run_test()
```

Part 2 예제에서 이 흐름은 대략 다음 파일들에 대응된다.

```text
tests/wb_env_tb_mod.sv                  : testbench top module, run_test 시작점
hdl/wb_env_top.sv                       : DUT/top 연결
hdl/dut2.sv                             : dummy DUT
include/wb_env.sv                       : include 묶음
src/wb_transaction.sv                   : sequence item / transaction
src/wb_master_agent_sequence_library.sv : sequence 정의
src/wb_master_seqr.sv                   : sequencer
src/wb_master.sv                        : master driver
src/wb_master_if.sv                     : master interface
src/wb_master_mon.sv                    : master monitor
src/wb_slave.sv                         : slave driver
src/wb_slave_if.sv                      : slave interface
src/wb_slave_mon.sv                     : slave monitor
env/wb_master_agent.sv                  : master agent
env/wb_slave_agent.sv                   : slave agent
env/wb_env_env.sv                       : env container
src/wb_scoreboard.sv                    : scoreboard
src/wb_env_cov.sv                       : functional coverage
tests/wb_env_test.sv                    : UVM test, config_db, default_sequence
run/Makefile                            : VCS compile/run recipe
```

---

## 체크리스트

### 0. Repo orientation

목표:
- 저장소가 어떤 목적의 예제 모음인지 이해한다.
- 왜 Part 2를 중심 예제로 보는지 이해한다.

읽을 파일:
- `README.md`
- `Part_2-Putting_it_all_Together/README.md`

확인할 것:
- [ ] repo가 UVM-1.2 + VCS 기준이라는 점을 이해했다.
- [ ] 예제들이 self-contained라서 코드 반복이 많다는 점을 이해했다.
- [ ] 모든 파일을 처음부터 다 읽지 않고 Part 2 중심으로 본다는 전략을 이해했다.
- [ ] `env`, `hdl`, `include`, `run`, `src`, `tests` 디렉터리의 역할을 말할 수 있다.

완료 기준:
- `Part_2-Putting_it_all_Together` 안의 각 디렉터리가 무엇을 담는지 한 문장씩 설명할 수 있다.

---

### 1. UVM 전체 구조 mental model

목표:
- UVM testbench가 왜 여러 class/component로 나뉘는지 이해한다.
- `test`, `env`, `agent`, `sequencer`, `driver`, `monitor`, `scoreboard`, `coverage`, `transaction`의 역할을 구분한다.

읽을 파일:
- `Part_2-Putting_it_all_Together/README.md`
- `Part_2-Putting_it_all_Together/include/wb_env.sv`

확인할 것:
- [ ] transaction은 “신호 한 싸이클”이 아니라 “의미 있는 bus operation”이라는 점을 이해했다.
- [ ] sequence는 transaction을 만들어내는 stimulus generator라는 점을 이해했다.
- [ ] driver는 transaction을 pin-level signal로 바꾸는 역할임을 이해했다.
- [ ] monitor는 pin-level signal을 다시 transaction으로 복원하는 역할임을 이해했다.
- [ ] scoreboard는 expected/actual 비교를 담당한다는 점을 이해했다.
- [ ] coverage는 “검증이 충분했는가”를 측정한다는 점을 이해했다.

완료 기준:
- 위 구성요소들을 데이터 흐름 기준으로 연결해서 설명할 수 있다.

---

### 2. Simulation entry point: top module과 run_test

목표:
- SystemVerilog module world와 UVM class world가 어디서 연결되는지 이해한다.

읽을 파일:
- `Part_2-Putting_it_all_Together/tests/wb_env_tb_mod.sv`
- `Part_2-Putting_it_all_Together/hdl/wb_env_top.sv`
- `Part_2-Putting_it_all_Together/hdl/dut2.sv`

확인할 것:
- [ ] top module이 clock/reset/interface/DUT를 준비한다는 점을 이해했다.
- [ ] `run_test()`가 UVM test를 시작한다는 점을 이해했다.
- [ ] `+UVM_TESTNAME=...`가 어떤 test class를 실행할지 고른다는 점을 이해했다.
- [ ] virtual interface가 module world와 class world를 연결하는 통로라는 점을 이해했다.

완료 기준:
- “시뮬레이터가 시작된 뒤 어떤 순서로 UVM test까지 도달하는가?”를 말할 수 있다.

---

### 3. UVM test class와 phase

목표:
- `uvm_test`가 환경 생성, config 설정, sequence 선택을 담당한다는 점을 이해한다.

읽을 파일:
- `Part_2-Putting_it_all_Together/tests/wb_env_test.sv`
- `Part_2-Putting_it_all_Together/tests/wb_env_base_test.sv`
- `Part_2-Putting_it_all_Together/tests/wb_env_test_extended.sv`

확인할 것:
- [ ] `build_phase`에서 component/config를 만든다는 점을 이해했다.
- [ ] `uvm_config_db::set`이 어떤 component에 설정을 전달하는지 이해했다.
- [ ] `default_sequence` 설정이 어떤 sequencer에서 어떤 sequence를 돌릴지 정한다는 점을 이해했다.
- [ ] `report_phase`에서 pass/fail 메시지를 낼 수 있다는 점을 이해했다.

완료 기준:
- `wb_env_test.sv`의 build_phase를 줄 단위로 설명할 수 있다.

---

### 4. Transaction / sequence item

목표:
- UVM에서 transaction class가 무엇을 표현하는지 이해한다.

읽을 파일:
- `Part_2-Putting_it_all_Together/src/wb_transaction.sv`
- `Part_2-Putting_it_all_Together/src/wb_transaction_extended.sv`

확인할 것:
- [ ] transaction의 field가 bus operation의 정보를 담는다는 점을 이해했다.
- [ ] randomization/constraint가 stimulus space를 정의한다는 점을 이해했다.
- [ ] `uvm_object_utils`와 factory 등록의 목적을 이해했다.
- [ ] print/copy/compare 관련 macro 또는 method의 의미를 이해했다.

완료 기준:
- 새 field 하나를 transaction에 추가한다면 어느 부분을 고쳐야 하는지 말할 수 있다.

---

### 5. Sequence와 Sequencer

목표:
- sequence가 transaction을 생성하고 sequencer를 통해 driver에게 전달하는 구조를 이해한다.

읽을 파일:
- `Part_2-Putting_it_all_Together/src/wb_master_agent_sequence_library.sv`
- `Part_2-Putting_it_all_Together/src/wb_slave_agent_sequence_library.sv`
- `Part_2-Putting_it_all_Together/src/wb_master_seqr.sv`
- `Part_2-Putting_it_all_Together/src/wb_slave_seqr.sv`

확인할 것:
- [ ] sequence의 `body()`에서 item을 만들고 randomize하는 흐름을 이해했다.
- [ ] sequencer는 sequence와 driver 사이의 중재자라는 점을 이해했다.
- [ ] default_sequence가 main_phase에 연결되는 방식을 이해했다.

완료 기준:
- 간단한 read/write sequence 하나를 pseudo-code로 작성할 수 있다.

---

### 6. Interface와 Driver

목표:
- transaction이 실제 DUT pin-level signal로 변환되는 과정을 이해한다.

읽을 파일:
- `Part_2-Putting_it_all_Together/src/wb_master_if.sv`
- `Part_2-Putting_it_all_Together/src/wb_master.sv`
- `Part_2-Putting_it_all_Together/src/wb_slave_if.sv`
- `Part_2-Putting_it_all_Together/src/wb_slave.sv`

확인할 것:
- [ ] interface가 signal bundle과 timing task를 담는다는 점을 이해했다.
- [ ] driver가 `seq_item_port`에서 item을 받아오는 구조를 이해했다.
- [ ] driver가 transaction field를 bus signal로 drive한다는 점을 이해했다.
- [ ] clocking/timing을 driver/interface 어느 쪽에서 담당하는지 추적할 수 있다.

완료 기준:
- transaction 하나가 driver를 거쳐 DUT signal로 바뀌는 과정을 설명할 수 있다.

---

### 7. Monitor와 analysis port

목표:
- monitor가 DUT signal을 관찰해서 transaction으로 복원하고, scoreboard/coverage로 broadcast하는 구조를 이해한다.

읽을 파일:
- `Part_2-Putting_it_all_Together/src/wb_master_mon.sv`
- `Part_2-Putting_it_all_Together/src/wb_slave_mon.sv`
- `Part_2-Putting_it_all_Together/src/mon_2cov.sv`

확인할 것:
- [ ] monitor는 DUT를 drive하지 않고 관찰만 한다는 점을 이해했다.
- [ ] analysis_port는 여러 subscriber에게 transaction을 전달할 수 있다는 점을 이해했다.
- [ ] monitor가 어떤 조건에서 transaction을 만들고 write하는지 추적할 수 있다.

완료 기준:
- monitor output이 scoreboard와 coverage로 흘러가는 경로를 설명할 수 있다.

---

### 8. Agent와 Env

목표:
- driver/sequencer/monitor를 agent로 묶고, agent들을 env로 묶는 계층 구조를 이해한다.

읽을 파일:
- `Part_2-Putting_it_all_Together/env/wb_master_agent.sv`
- `Part_2-Putting_it_all_Together/env/wb_slave_agent.sv`
- `Part_2-Putting_it_all_Together/env/wb_env_env.sv`

확인할 것:
- [ ] agent가 active/passive 개념을 가질 수 있다는 점을 이해했다.
- [ ] build_phase에서 하위 component를 만든다는 점을 이해했다.
- [ ] connect_phase에서 TLM port/export를 연결한다는 점을 이해했다.
- [ ] env가 agent, scoreboard, coverage를 조립하는 container라는 점을 이해했다.

완료 기준:
- “왜 driver/monitor를 test에 직접 만들지 않고 agent/env로 감싸는가?”에 답할 수 있다.

---

### 9. Scoreboard와 Coverage

목표:
- 검증 환경이 단순히 stimulus를 넣는 것이 아니라 결과 확인과 coverage 수집까지 해야 함을 이해한다.

읽을 파일:
- `Part_2-Putting_it_all_Together/src/wb_scoreboard.sv`
- `Part_2-Putting_it_all_Together/src/wb_env_cov.sv`
- `Part_2-Putting_it_all_Together/src/mon_2cov.sv`

확인할 것:
- [ ] scoreboard가 expected와 actual을 비교한다는 점을 이해했다.
- [ ] coverage group/coverpoint가 어떤 검증 목표를 측정하는지 이해했다.
- [ ] monitor transaction이 coverage sampling으로 연결되는 흐름을 이해했다.

완료 기준:
- address range coverage point 하나를 추가한다면 어디에 넣을지 말할 수 있다.

---

### 10. Config DB와 Factory

목표:
- UVM에서 component를 느슨하게 연결하고 override 가능한 구조를 만드는 방식을 이해한다.

읽을 파일:
- `Part_2-Putting_it_all_Together/tests/wb_env_test.sv`
- `Part_2-Putting_it_all_Together/src/wb_config.sv`
- `Part_5_Advanced_Topics/config_db_regular_expressions/src/README.md`
- `Part_5_Advanced_Topics/config_db_regular_expressions/src/top.sv`

확인할 것:
- [ ] `uvm_config_db::set/get`의 path와 field name 의미를 이해했다.
- [ ] 잘못된 path가 설정 누락을 만들 수 있다는 점을 이해했다.
- [ ] `type_id::create`가 factory를 통해 object/component를 만든다는 점을 이해했다.
- [ ] factory override가 테스트별 behavior 교체에 쓰일 수 있다는 점을 이해했다.

완료 기준:
- config_db set/get 한 쌍을 찾아서 “누가 넣고 누가 받는지” 설명할 수 있다.

---

### 11. Run flow / Makefile 읽기

목표:
- 실제 시뮬레이션 명령이 어떤 파일들을 compile하고 어떤 test를 실행하는지 이해한다.

읽을 파일:
- `Part_2-Putting_it_all_Together/run/Makefile`
- `Part_2-Putting_it_all_Together/run/vcs.log`
- `Part_2-Putting_it_all_Together/run/simv.log` 또는 존재하는 run log

확인할 것:
- [ ] `+incdir+`가 include search path라는 점을 이해했다.
- [ ] compile 대상 파일과 include 파일의 차이를 이해했다.
- [ ] `+UVM_TESTNAME=wb_env_test`의 역할을 이해했다.
- [ ] `+UVM_CONFIG_DB_TRACE`가 config_db debugging에 유용하다는 점을 이해했다.

완료 기준:
- VCS가 있다고 가정했을 때 `make`가 어떤 순서로 동작할지 설명할 수 있다.

---

### 12. 첫 수정 실습: transaction field 추가 사고 실험

목표:
- UVM 환경에서 data model 변경이 여러 계층에 어떻게 전파되는지 이해한다.

수정 후보:
- `wb_transaction.sv`에 `delay` 또는 `burst_len` field 추가

확인할 것:
- [ ] transaction field 선언 위치를 찾았다.
- [ ] random constraint 추가 위치를 찾았다.
- [ ] print/copy/compare에 반영해야 하는지 판단했다.
- [ ] sequence가 새 field를 어떻게 randomize할지 생각했다.
- [ ] driver가 새 field를 timing에 반영해야 하는지 생각했다.
- [ ] coverage에 새 field를 sampling할지 생각했다.

완료 기준:
- “transaction field 하나 추가”가 단일 파일 변경이 아닐 수 있음을 이해한다.

---

### 13. 첫 구현 실습: 새 sequence 설계

목표:
- UVM에서 test case 변화는 주로 sequence/test 설정으로 만든다는 점을 이해한다.

구현 후보:
- fixed address write/read sequence
- random address write sequence
- corner-case max/min address sequence

확인할 것:
- [ ] 기존 sequence class를 하나 골라 구조를 이해했다.
- [ ] 새 sequence class 이름을 정했다.
- [ ] `body()`에서 몇 개의 transaction을 생성할지 정했다.
- [ ] `uvm_do_with` 또는 create/start_item/finish_item 패턴 중 하나를 선택했다.
- [ ] test에서 default_sequence로 연결하는 방법을 이해했다.

완료 기준:
- 새 sequence의 pseudo-code를 작성할 수 있다.

---

### 14. Advanced 1: phase callback

목표:
- UVM phase와 callback을 이용해 testbench behavior를 확장하는 방법을 본다.

읽을 파일:
- `Part_5_Advanced_Topics/phase_callbacks/README.md`
- `Part_5_Advanced_Topics/phase_callbacks/tests/wb_env_test_phase_cb.sv`

확인할 것:
- [ ] Part 2 대비 어떤 파일만 달라졌는지 확인했다.
- [ ] callback이 기존 component 코드를 직접 수정하지 않고 behavior를 바꾸는 방법임을 이해했다.

완료 기준:
- callback을 쓰는 이유를 한 문장으로 설명할 수 있다.

---

### 15. Advanced 2: RAL/register model

목표:
- UVM Register Abstraction Layer의 기본 목적을 이해한다.

읽을 파일:
- `Part_5_Advanced_Topics/registers_example/README.md`
- `Part_5_Advanced_Topics/registers_example/env/ral_simple_ral_env.sv`
- `Part_5_Advanced_Topics/registers_example/src/*ral*` 관련 파일

확인할 것:
- [ ] RAL이 register access를 추상화한다는 점을 이해했다.
- [ ] frontdoor/backdoor access 개념을 구분한다.
- [ ] adapter가 bus transaction과 register operation 사이를 변환한다는 점을 이해한다.

완료 기준:
- “왜 register를 그냥 address write/read로만 테스트하지 않고 RAL을 쓰는가?”에 답할 수 있다.

---

## 생성된 HTML workbook 자료

현재 이 repo에는 두 종류의 한국어 HTML workbook이 생성되어 있다.

1. `lectures/index.html`
   - repo 실제 source excerpt를 기반으로 한 Practical-UVM-Step-By-Step 학습 자료
   - `day0_repo_orientation*.html` 2개와 Day 1~21 page를 포함한다.
   - 실제 파일 경로/line range를 보며 UVM testbench 구조를 추적한다.

2. `lectures_chipverify_uvm/index.html`
   - ChipVerify UVM tutorial URL을 source map으로 삼은 개념 중심 학습 자료
   - Day 0~30 page를 포함한다.
   - 원문 article을 대량 복제하지 않고, 출처 URL + 한국어 설명 + 직접 작성한 compact UVM 예제로 구성한다.

관련 builder skill:
- `skills/uvm-practical-lecture-builder/SKILL.md`
- `skills/chipverify-uvm-lecture-builder/SKILL.md`

관련 metadata:
- `lectures_chipverify_uvm/sources/chipverify_uvm_source_map.json`
- `lectures_chipverify_uvm/sources/chipverify_uvm_curriculum.json`

---

## 현재 진행 상태

자료 생성과 실제 학습 진행은 분리해서 본다. 아래 `[x]`는 학습자료/문서 artifact 생성 완료를 뜻하며, 사용자가 각 Day를 실제로 공부했다는 의미는 아니다.

- [x] repo clone
- [x] 중심 예제 선정: `Part_2-Putting_it_all_Together`
- [x] 체크리스트 문서 작성: `UVM_LEARNING_CHECKLIST.ko.md`
- [x] 원본 텍스트 문서 한국어 번역본 생성 및 `TRANSLATION_MANIFEST_KR.md` 작성
- [x] repo-grounded HTML workbook 생성: `lectures/index.html`
- [x] repo-grounded lecture builder skill 생성: `skills/uvm-practical-lecture-builder/SKILL.md`
- [x] ChipVerify 기반 HTML workbook 생성: `lectures_chipverify_uvm/index.html`
- [x] ChipVerify source/curriculum metadata 생성
- [x] ChipVerify lecture builder skill 생성: `skills/chipverify-uvm-lecture-builder/SKILL.md`
- [x] HTML internal link, inline JavaScript, remote asset 여부 검증
- [ ] 실제 학습 진행: Day 0부터 사용자가 workbook을 보며 순차 진행
- [ ] simulator 실습: VCS/Questa/Xcelium 또는 EDA Playground 같은 실행 환경 확보 후 진행

---

## 첫 번째 수업에서 다룰 내용

시작점:
- `README.md`
- `Part_2-Putting_it_all_Together/README.md`

핵심 질문:
1. 이 repo는 왜 모든 예제가 self-contained인가?
2. 왜 Part 2가 중심 예제인가?
3. `env`, `hdl`, `include`, `run`, `src`, `tests`는 각각 무엇인가?
4. UVM testbench에서 “코드가 많아지는 이유”는 무엇인가?

첫 번째 완료 조건:
- 사용자가 Part 2 디렉터리 구조를 보고 “어느 파일부터 읽어야 하는지” 스스로 판단할 수 있다.
