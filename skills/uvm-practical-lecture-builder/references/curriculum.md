# UVM Practical Lecture Curriculum

Day 0은 hand-authored orientation입니다. Day 1-21은 동일한 workbook 형식으로 생성된 source-grounded HTML 강의자료입니다.

| Day | Topic | File |
|---:|---|---|
| 0 | Repo orientation | `lectures/day0_repo_orientation.html` |
| 1 | UVM 전체 구조 mental model | `lectures/day1_uvm_mental_model.html` |
| 2 | Simulation entry point: top module과 run_test | `lectures/day2_top_and_run_test.html` |
| 3 | UVM test class와 phase | `lectures/day3_test_class_and_phase.html` |
| 4 | Transaction / sequence item | `lectures/day4_transaction_item.html` |
| 5 | Sequence와 Sequencer | `lectures/day5_sequence_and_sequencer.html` |
| 6 | Interface와 Driver | `lectures/day6_interface_and_driver.html` |
| 7 | Monitor와 analysis port | `lectures/day7_monitor_analysis_port.html` |
| 8 | Agent와 Env | `lectures/day8_agent_and_env.html` |
| 9 | Scoreboard와 Coverage | `lectures/day9_scoreboard_and_coverage.html` |
| 10 | Config DB와 Factory | `lectures/day10_config_db_factory.html` |
| 11 | Run flow / Makefile 읽기 | `lectures/day11_run_flow_makefile.html` |
| 12 | 첫 수정 실습: transaction field 추가 사고 실험 | `lectures/day12_transaction_change_lab.html` |
| 13 | 첫 구현 실습: 새 sequence 설계 | `lectures/day13_new_sequence_lab.html` |
| 14 | Advanced 1: phase callback | `lectures/day14_phase_callbacks.html` |
| 15 | Advanced 2: RAL/register model | `lectures/day15_ral_register_model.html` |
| 16 | Part 1: UVM core utilities | `lectures/day16_part1_core_utilities.html` |
| 17 | Part 3: Stimulus generation | `lectures/day17_part3_stimulus_generation.html` |
| 18 | Advanced 3: Reactive slave sequence | `lectures/day18_reactive_slave_sequence.html` |
| 19 | Advanced 4: Spanning phases | `lectures/day19_spanning_phases.html` |
| 20 | Advanced 5: Coverage closure와 wb_dma | `lectures/day20_coverage_closure_wb_dma.html` |
| 21 | SOC-scale case studies: ethernet, wb_conmax, vga_lcd | `lectures/day21_soc_case_studies.html` |

## Design rules

- 실제 repo file line range를 source card로 넣는다.
- `.sv`, `.svh`, `.incl` 발췌만 SystemVerilog highlighter 대상으로 삼는다.
- README/Makefile/log는 plain excerpt로 유지한다.
- 각 Day는 mental model, trace, source excerpts, checklist, quiz, practice, LLM prompt를 포함한다.
- 현재 host에는 VCS/Questa/Xcelium이 없으므로 실행 검증이 아니라 code-reading workbook으로 다룬다.
