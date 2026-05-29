# ChipVerify UVM Curriculum

Generated Day 0-30 map for `lectures_chipverify_uvm/`.

## Day 0. ChipVerify UVM course orientation

- Module: A - Orientation and first UVM run
- Output: `lectures_chipverify_uvm/day0_chipverify_uvm_orientation.html`
- Goal: 이 강의 세트의 사용법, 원문 링크를 읽는 법, 기존 repo-grounded 강의와의 차이를 이해한다.
- Sources:
  - UVM Tutorial: https://chipverify.com/tutorials/uvm/

## Day 1. UVM overview: OVM에서 UVM까지

- Module: A - Orientation and first UVM run
- Output: `lectures_chipverify_uvm/day1_uvm_overview_ovm_to_uvm.html`
- Goal: UVM이 왜 생겼고 testbench를 어떤 추상화로 나누는지 이해한다.
- Sources:
  - UVM Tutorial: https://chipverify.com/tutorials/uvm/
  - UVM Introduction: https://chipverify.com/uvm/uvm-introduction

## Day 2. UVM installation and Hello UVM

- Module: A - Orientation and first UVM run
- Output: `lectures_chipverify_uvm/day2_installation_hello_uvm.html`
- Goal: `import uvm_pkg::*`, `include "uvm_macros.svh"`, `run_test()`의 최소 실행 흐름을 이해한다.
- Sources:
  - UVM Installation: https://chipverify.com/uvm/uvm-installation
  - Hello UVM !: https://chipverify.com/uvm/uvm-hello-world

## Day 3. Base classes: object vs component

- Module: B - Base classes and object/component mental model
- Output: `lectures_chipverify_uvm/day3_base_classes_root_object_component.html`
- Goal: UVM class hierarchy에서 `uvm_root`, `uvm_object`, `uvm_component`의 역할을 구분한다.
- Sources:
  - Base Classes: https://chipverify.com/uvm/base-classes
  - UVM Root [uvm_root]: https://chipverify.com/uvm/uvm-root

## Day 4. uvm_object lifecycle and utilities

- Module: B - Base classes and object/component mental model
- Output: `lectures_chipverify_uvm/day4_uvm_object_lifecycle_utilities.html`
- Goal: transaction 객체가 왜 object 계층에 있고 copy/clone/compare/print/pack이 왜 필요한지 이해한다.
- Sources:
  - UVM Object [uvm_object]: https://chipverify.com/uvm/uvm-object
  - UVM Object Copy/Clone: https://chipverify.com/uvm/uvm-object-copy-clone
  - UVM Object Compare: https://chipverify.com/uvm/uvm-object-compare
  - UVM Object Print: https://chipverify.com/uvm/uvm-object-print
  - UVM Object Pack/Unpack: https://chipverify.com/uvm/uvm-object-pack-unpack

## Day 5. uvm_component hierarchy and phases preview

- Module: B - Base classes and object/component mental model
- Output: `lectures_chipverify_uvm/day5_uvm_component_testbench_top.html`
- Goal: component tree, parent/child 관계, testbench top과 test class의 연결을 이해한다.
- Sources:
  - UVM Component [uvm_component]: https://chipverify.com/uvm/uvm-component
  - UVM Testbench Top: https://chipverify.com/uvm/uvm-testbench-top
  - UVM Test [uvm_test]: https://chipverify.com/uvm/uvm-test

## Day 6. Environment and agent composition

- Module: C - Testbench components
- Output: `lectures_chipverify_uvm/day6_environment_and_agent.html`
- Goal: env와 agent가 reusable verification component를 구성하는 방법을 이해한다.
- Sources:
  - UVM Environment [uvm_env]: https://chipverify.com/uvm/uvm-environment
  - UVM Agent | uvm_agent: https://chipverify.com/uvm/uvm-agent

## Day 7. Driver, monitor, subscriber

- Module: C - Testbench components
- Output: `lectures_chipverify_uvm/day7_driver_monitor_subscriber.html`
- Goal: active stimulus path와 passive observation path를 구분한다.
- Sources:
  - UVM Driver [uvm_driver]: https://chipverify.com/uvm/uvm-driver
  - UVM Monitor [uvm_monitor]: https://chipverify.com/uvm/uvm-monitor
  - Subscriber [uvm_subscriber]: https://chipverify.com/uvm/uvm-subscriber

## Day 8. Sequencer and scoreboard

- Module: C - Testbench components
- Output: `lectures_chipverify_uvm/day8_sequencer_and_scoreboard.html`
- Goal: sequencer가 sequence와 driver 사이에서 하는 일, scoreboard가 expected/actual을 비교하는 위치를 이해한다.
- Sources:
  - UVM Sequencer [uvm_sequencer]: https://chipverify.com/uvm/uvm-sequencer
  - UVM Scoreboard: https://chipverify.com/uvm/uvm-scoreboard

## Day 9. UVM phases

- Module: D - Phases and simulation lifetime
- Output: `lectures_chipverify_uvm/day9_uvm_phases.html`
- Goal: build/connect/end_of_elaboration/start_of_simulation/run/extract/check/report/final phase의 의도를 구분한다.
- Sources:
  - UVM Phases: https://chipverify.com/uvm/uvm-phases

## Day 10. Objection and user-defined phases

- Module: D - Phases and simulation lifetime
- Output: `lectures_chipverify_uvm/day10_objection_and_custom_phase.html`
- Goal: run phase가 언제 끝나는지, objection이 왜 필요한지 이해한다.
- Sources:
  - UVM Objection: https://chipverify.com/uvm/uvm-objection
  - Creating user-defined phases: https://chipverify.com/uvm/uvm-user-defined-phase

## Day 11. Sequence basics

- Module: E - Sequences and stimulus generation
- Output: `lectures_chipverify_uvm/day11_sequence_basics.html`
- Goal: `uvm_sequence`, sequence item, `body()`의 기본 구조를 이해한다.
- Sources:
  - UVM Sequence [uvm_sequence]: https://chipverify.com/uvm/uvm-sequence
  - How to create and use a sequence: https://chipverify.com/uvm/how-to-create-and-use-a-sequence

## Day 12. Starting sequences and macros

- Module: E - Sequences and stimulus generation
- Output: `lectures_chipverify_uvm/day12_sequence_start_and_macros.html`
- Goal: `start()`와 `uvm_do` 계열 macro의 차이를 이해하고 macro 사용의 장단점을 판단한다.
- Sources:
  - How to execute sequences via start(): https://chipverify.com/uvm/how-to-execute-sequences-via-start-method
  - Executing sequence macros: https://chipverify.com/uvm/how-to-execute-sequences-via-uvm-do-macros
  - How to use `uvm_do sequence macros ?: https://chipverify.com/uvm/uvm-do-macros
  - Sequence action macros for pre-existing items: https://chipverify.com/uvm/sequence-action-macros-for-pre-existing-items

## Day 13. Virtual sequence, virtual sequencer, sequence library

- Module: E - Sequences and stimulus generation
- Output: `lectures_chipverify_uvm/day13_virtual_sequence_and_arbitration.html`
- Goal: multi-agent coordination과 arbitration 개념을 이해한다.
- Sources:
  - UVM Virtual Sequence: https://chipverify.com/uvm/uvm-virtual-sequence
  - UVM Virtual Sequencer: https://chipverify.com/uvm/uvm-virtual-sequencer
  - UVM Sequence Library: https://chipverify.com/uvm/uvm-sequence-library
  - UVM Sequence Arbitration: https://chipverify.com/uvm/uvm-sequence-arbitration

## Day 14. Transaction object and driver handshake

- Module: E - Sequences and stimulus generation
- Output: `lectures_chipverify_uvm/day14_transaction_and_driver_handshake.html`
- Goal: sequence item이 driver까지 전달되는 handshake model을 이해한다.
- Sources:
  - Transaction Object: https://chipverify.com/uvm/uvm-transaction-object
  - Using get_next_item(): https://chipverify.com/uvm/uvm-using-get-next-item
  - Using get() and put(): https://chipverify.com/uvm/driver-using-get-and-put

## Day 15. TLM overview and blocking put/get

- Module: F - TLM communication
- Output: `lectures_chipverify_uvm/day15_tlm_blocking_put_get.html`
- Goal: port/export/imp, blocking put/get의 mental model을 만든다.
- Sources:
  - UVM TLM: https://chipverify.com/uvm/uvm-tlm
  - UVM TLM Blocking Put Port: https://chipverify.com/uvm/uvm-tlm-blocking-put-port
  - UVM TLM Blocking Get Port: https://chipverify.com/uvm/uvm-tlm-blocking-get-port

## Day 16. TLM FIFO and example

- Module: F - TLM communication
- Output: `lectures_chipverify_uvm/day16_tlm_fifo_and_example.html`
- Goal: FIFO가 producer/consumer를 느슨하게 연결하는 방법을 이해한다.
- Sources:
  - UVM TLM Fifo [uvm_tlm_fifo]: https://chipverify.com/uvm/uvm-tlm-fifo
  - UVM TLM Example: https://chipverify.com/uvm/uvm-tlm-example

## Day 17. Analysis port, sockets, nonblocking TLM

- Module: F - TLM communication
- Output: `lectures_chipverify_uvm/day17_analysis_port_and_nonblocking_tlm.html`
- Goal: monitor에서 scoreboard/coverage로 fanout하는 analysis path와 nonblocking TLM 차이를 이해한다.
- Sources:
  - UVM TLM Analysis Port: https://chipverify.com/uvm/uvm-tlm-analysis-port
  - UVM TLM Sockets: https://chipverify.com/uvm/uvm-tlm-sockets
  - Using _decl macro in TLM: https://chipverify.com/uvm/using-decl-macro-in-tlm
  - UVM TLM Nonblocking Put Port: https://chipverify.com/uvm/uvm-tlm-nonblocking-put-port
  - UVM TLM Port to Export to Imp: https://chipverify.com/uvm/uvm-tlm-port-export-imp
  - UVM TLM Non-blocking Get Port: https://chipverify.com/uvm/uvm-tlm-nonblocking-get-port

## Day 18. Factory override

- Module: G - Configuration, factory, resource DB
- Output: `lectures_chipverify_uvm/day18_factory_override.html`
- Goal: source를 수정하지 않고 test에서 type/instance override하는 이유를 이해한다.
- Sources:
  - UVM Factory Override: https://chipverify.com/uvm/uvm-factory-override

## Day 19. Configure components and config_db

- Module: G - Configuration, factory, resource DB
- Output: `lectures_chipverify_uvm/day19_configure_components_and_config_db.html`
- Goal: interface handle, knobs, env settings를 config_db로 전달하는 흐름을 이해한다.
- Sources:
  - Configure Components: https://chipverify.com/uvm/configure-components
  - UVM config database: https://chipverify.com/uvm/uvm-config-db
  - uvm_config_db Examples: https://chipverify.com/uvm/uvm-config-db-examples

## Day 20. Resource database

- Module: G - Configuration, factory, resource DB
- Output: `lectures_chipverify_uvm/day20_resource_database.html`
- Goal: config_db와 resource DB의 관계와 beginner가 피해야 할 남용 패턴을 이해한다.
- Sources:
  - Understanding the resource database: https://chipverify.com/uvm/understanding-the-resource-database

## Day 21. RAL overview and register model classes

- Module: H - RAL and register verification
- Output: `lectures_chipverify_uvm/day21_ral_overview_and_model_classes.html`
- Goal: register abstraction layer가 bus transaction과 register intent를 분리하는 이유를 이해한다.
- Sources:
  - UVM Register Abstraction Layer: https://chipverify.com/uvm/uvm-register-layer
  - UVM Register Model Classes: https://chipverify.com/uvm/uvm-register-model

## Day 22. Register environment and connection

- Module: H - RAL and register verification
- Output: `lectures_chipverify_uvm/day22_register_environment_connection.html`
- Goal: adapter, predictor, sequencer 연결 흐름을 이해한다.
- Sources:
  - UVM Register Environment: https://chipverify.com/uvm/uvm-register-environment
  - Connecting register env: https://chipverify.com/uvm/connecting-register-env

## Day 23. Backdoor access and register model example

- Module: H - RAL and register verification
- Output: `lectures_chipverify_uvm/day23_ral_backdoor_and_example.html`
- Goal: frontdoor/backdoor의 차이와 RAL example의 전체 실행 흐름을 이해한다.
- Sources:
  - UVM Register Backdoor Access: https://chipverify.com/uvm/uvm-register-backdoor-access
  - UVM Register Model Example: https://chipverify.com/uvm/uvm-register-model-example

## Day 24. Reporting and printer/comparer policy

- Module: I - Reporting, callbacks, events, macros
- Output: `lectures_chipverify_uvm/day24_reporting_printer_comparer.html`
- Goal: report verbosity/severity, object print/compare policy를 debugging 도구로 이해한다.
- Sources:
  - Reporting Classes: https://chipverify.com/uvm/reporting-classes
  - Reporting Functions: https://chipverify.com/uvm/report-functions
  - How to use uvm_printer: https://chipverify.com/uvm/uvm-printer
  - Setting policy using uvm_comparer: https://chipverify.com/uvm/uvm-comparer

## Day 25. Callback and events

- Module: I - Reporting, callbacks, events, macros
- Output: `lectures_chipverify_uvm/day25_callback_and_events.html`
- Goal: callback과 event를 통해 component를 직접 수정하지 않고 hook을 추가하는 방식을 이해한다.
- Sources:
  - UVM Callback: https://chipverify.com/uvm/uvm-callback
  - UVM Event: https://chipverify.com/uvm/uvm-event
  - UVM Event Pool: https://chipverify.com/uvm/uvm-event-pool

## Day 26. Utility and field macros, HDL access, singleton

- Module: I - Reporting, callbacks, events, macros
- Output: `lectures_chipverify_uvm/day26_macros_hdl_access_singleton.html`
- Goal: macro 자동화의 편의성과 숨겨지는 비용, HDL access routine의 사용 경계를 이해한다.
- Sources:
  - UVM utility & field macros: https://chipverify.com/uvm/uvm-utility-field-macros
  - UVM Field Macros: https://chipverify.com/uvm/uvm-field-macros
  - HDL access routines: https://chipverify.com/uvm/uvm-hdl-access-routines
  - UVM Singleton Object: https://chipverify.com/uvm/uvm-singleton-object

## Day 27. Reusable verification components

- Module: J - Reuse, examples, review
- Output: `lectures_chipverify_uvm/day27_reusable_verification_components.html`
- Goal: reusable VIP를 설계/사용할 때의 boundary, config, sequence strategy를 이해한다.
- Sources:
  - Guide - Developing Reusable Verification Components: https://chipverify.com/uvm/reusable-verification-components
  - Guide - Using Verification Components: https://chipverify.com/uvm/verification-components

## Day 28. Full verification testbench example

- Module: J - Reuse, examples, review
- Output: `lectures_chipverify_uvm/day28_full_verification_testbench_example.html`
- Goal: 지금까지 배운 component, phase, sequence, TLM, scoreboard가 한 testbench에서 어떻게 연결되는지 trace한다.
- Sources:
  - UVM Verification Testbench Example: https://chipverify.com/uvm/uvm-verification-testbench-example

## Day 29. Testbench examples 1 and 2

- Module: J - Reuse, examples, review
- Output: `lectures_chipverify_uvm/day29_testbench_examples_comparison.html`
- Goal: 예제 간 구조 차이를 비교하고 직접 확장할 지점을 찾는다.
- Sources:
  - UVM Testbench Example 1: https://chipverify.com/uvm/uvm-testbench-example-1
  - UVM Testbench Example 2: https://chipverify.com/uvm/uvm-testbench-example-2

## Day 30. Interview review and next steps

- Module: J - Reuse, examples, review
- Output: `lectures_chipverify_uvm/day30_interview_review_and_next_steps.html`
- Goal: 핵심 개념을 interview-style 질문으로 복습하고 Accellera UVM reference로 넘어갈 준비를 한다.
- Sources:
  - UVM Interview Questions Set 1: https://chipverify.com/uvm/uvm-interview-questions-set-1
  - UVM Interview Questions Set 2: https://chipverify.com/uvm/uvm-interview-questions-set-2
  - UVM Interview Questions Set 3: https://chipverify.com/uvm/uvm-interview-questions-set-3
  - UVM Interview Questions Set 4: https://chipverify.com/uvm/uvm-interview-questions-set-4
  - UVM Reference: https://chipverify.com/uvm-reference
  - Accellera UVM standards: https://www.accellera.org/downloads/standards/uvm
