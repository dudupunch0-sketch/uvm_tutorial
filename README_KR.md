
**** 중요 - 반드시 읽어 주세요 **********************

이 저장소를 zip으로 다운로드하지 말고 FORK해 주세요. 누군가 업데이트를 하거나 수정된 이슈를 발견했을 때
알릴 수 있도록 하고 싶기 때문입니다.

모든 예제는 UVM-1.2 및 VCS 2016.06-SP1에서 테스트되었습니다.
각 RUN 디렉터리에는 예제가 정상적으로 실행됨을 보여 주는 로그를 제공했습니다.

컴파일 로그: vcs.log
실행 로그 : simv.log

UVM 1.2가 최신 버전이므로, 예제는 UVM-1.2를 준수하도록 작성되었습니다.
컴파일 시 +UVM_NO_DEPRECATED define을 사용했습니다.

따라서 일부 예제는 uvm-1.1d에서 컴파일되지 않을 수 있습니다. 그런 변형이 필요하다면 알려 주세요. 가능한 한 대응해 보겠습니다.

명확하지 않거나 세부 내용이 빠진 부분이 있으면 버그를 등록하거나 알려 주세요. 가능한 한 수정하겠습니다.

****
# Book_Examples
이 예제들은 Srivatsa Vasudevan이 쓴 Practical UVM Step By Step 책의 예제입니다.


각 예제는 자체 완결형(SELF Contained)이 되도록 설계되었습니다.
다른 예제에서 반복되는 코드도 포함되어 있습니다.

일반적으로 각 예제에서 다른 예제와 차이가 있는 파일은 1~2개뿐입니다.

각 파일을 일일이 파고들지 마세요. 그렇게 하면 시간을 낭비하게 됩니다.
각 README에서 특정 파일을 보려면 아래 섹션만 확인하세요.

*********이 예제에서 변경된 파일 *****


<Part 2 예제 대비 변경된 파일 목록>


*************


나머지 파일은 디렉터리를 그대로 복사해 두고
큰 작업 없이 바로 컴파일할 수 있도록 포함되어 있습니다.


대부분의 모든 디렉터리는 테스트벤치 예제에서 아래 접근 방식으로 구성되어 있습니다.


env  --> 모든 environment container 파일이 들어 있습니다. Register Abstraction RALF 파일이 있다면 여기에 있습니다.<br>
hdl  --> 일반적으로 최상위 testbench가 들어 있습니다 <br>
include --> include 파일 목록 <br>
README --> 이 파일 <br>
run --> 모든 runtime 파일이 여기에 보관됩니다. Makefile도 여기에 있습니다. <br>
src --> 예제의 source입니다. wishbone 예제인 경우, 예제에 따라 한 단계 위 common 디렉터리에 파일이 있을 수 있습니다. <br>
tests --> 모든 UVM test가 여기에 저장됩니다 <br>

<!-- HERMES_LEARNING_ARTIFACTS_START -->
---

## 이 로컬 학습 프로젝트에 추가된 자료 (2026-05-29)

이 working tree에는 원본 `Practical-UVM-Step-By-Step` 예제 위에 한국어 학습용 문서와 HTML workbook이 추가되어 있습니다. 원본 RTL/UVM 예제 코드는 학습 자료 생성을 위해 수정하지 않았습니다.

### 1. Repo-grounded 한국어 HTML workbook

- Index: `lectures/index.html`
- 구성: `day0_repo_orientation*.html` 2개와 Day 1~21 page, 총 HTML 24개
- 성격: 이 저장소의 실제 UVM/SystemVerilog source excerpt를 직접 보여 주면서 `top -> test -> env -> agent -> sequence -> driver/monitor -> scoreboard/coverage` 흐름을 공부하는 자료
- Builder skill: `skills/uvm-practical-lecture-builder/SKILL.md`
- Curriculum reference: `skills/uvm-practical-lecture-builder/references/curriculum.md`

### 2. ChipVerify UVM 기반 한국어 HTML workbook

- Index: `lectures_chipverify_uvm/index.html`
- 구성: Day 0~30, 총 HTML 32개
- Source metadata: `lectures_chipverify_uvm/sources/chipverify_uvm_source_map.json`
- Curriculum metadata: `lectures_chipverify_uvm/sources/chipverify_uvm_curriculum.json`
- 성격: `https://chipverify.com/tutorials/uvm/` 및 연결된 `https://chipverify.com/uvm/...` topic들을 출처 URL로 삼아, 원문을 대량 복제하지 않고 한국어 mental model, 직접 작성한 compact UVM 예제, quiz, checklist, LLM 질문 prompt로 재구성한 자료
- Builder skill: `skills/chipverify-uvm-lecture-builder/SKILL.md`
- Curriculum reference: `skills/chipverify-uvm-lecture-builder/references/curriculum.md`

### 3. 학습 운영 문서

- 단계별 체크리스트: `UVM_LEARNING_CHECKLIST.ko.md`
- 한국어 번역 manifest: `TRANSLATION_MANIFEST_KR.md`
- 현재 진행상황 기록: `Daily_0529.md`

### 4. 현재 검증 상태

- HTML file/link/inline JavaScript 검증은 통과했습니다.
- 이 host에는 VCS/Questa/Xcelium 같은 상용 simulator가 없으므로 현재 자료는 실행 검증물이 아니라 code-reading 및 개념 학습용 artifact입니다.
- 미리보기가 필요하면 repo root에서 다음 명령으로 로컬 서버를 다시 띄우면 됩니다.

```bash
python3 -m http.server 8765 --bind 127.0.0.1
```

그 다음 브라우저에서 아래를 엽니다.

```text
http://127.0.0.1:8765/lectures/index.html
http://127.0.0.1:8765/lectures_chipverify_uvm/index.html
```

<!-- HERMES_LEARNING_ARTIFACTS_END -->
