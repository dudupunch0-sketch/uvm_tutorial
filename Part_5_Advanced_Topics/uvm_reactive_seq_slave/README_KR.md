
이 예제에서는 Part1/uvm_scoreboard의 예제와 비교해 주요 파일 세 개가 변경되었습니다.
다른 모든 파일의 내용은 대체로 동일합니다.

다음 파일들만 보세요:
wb_slave_seqr.sv
wb_slave_agent_sequence_library.sv
wb_slave.sv



*************************************************************
예제 컴파일 및 실행 단계
*************************************************************

참고:
  1) VCS 설치에 포함된 UVM1.2 내장 source를 포함하려면:
     Makefile에서 UVM_HOME 포함은 -ntb_opts uvm 명령으로 대체할 수 있습니다
  2) VCS 설치 디렉터리 외부의 UVM source를 사용하려면:
     환경 변수 VCS_UVM_HOME을 uvm-1.2 설치 디렉터리로 설정하세요

*************************************************************
UVMGEN이 생성한 environment의 디렉터리 구조
*************************************************************
-EXAMPLE
	|
       -README.md (이 파일)
       |
       -hdl/        ---> top module과 모든 environment 파일의 inclusion을 포함합니다.
       |
       | - wb_env_top.sv  -- 모든 것을 instance화하는 top level 파일
       | - dut.v     -- Dummy DUT
       |
       -env/        ---> environment 관련 파일(environment, ralenv)을 포함합니다
       |
       | - wb_slave_agent.sv  -- top level slave agent 파일
       | - wb_master_agent.sv -- top level master agent 파일
       | - wb_env_env.sv      -- 완전한 environment
       |
       -include/
       |
       -src/        ---> Transaction, configurations, driver, monitor, master/slave subenv, scoreboard, coverage 관련 파일을 포함합니다.
       |
       | - wb_slave.sv     --- Slave drive
       | - wb_slave_mon.sv  -- Slave monitor
       | - wb_slave_if.sv   -- slave interface.
       | - wb_transaction.sv  -- transaction class
       | - wb_slave_seqr.sv   -- Slave Sequencer. 이 예제에서는 사용되지 않습니다
       | - wb_master.sv     -- master driver
       | - wb_master_seqr.sv  -- master sequencer
       | - wb_master_agent_sequence_library.sv -- master를 위한 모든 sequence는 여기에 있습니다
       | - wb_slave_agent_sequence_library.sv -- master를 위한 모든 sequence는 여기에 있습니다
       | - wb_master_if.sv  -- master interface
       | - wb_master_mon.sv  -- master monitor
       | - wb_env_cov.sv   -- coverage
       | - wb_env_cfg.sv   -- env config class 예제입니다. 이 예제에서는 많이 사용되지 않습니다
       |
       -tests/      ---> testbench module과 testcase를 포함합니다
       |
       | - wb_env_tb_mod.sv
       | - wb_env_slave_test.sv -- slave reactive agent를 위한 실제 test
       |
       -run/        ---> Makefile
	| - Makefile
	| - simv.log -- 실행 로그 파일
	| - vcs.log  -- 컴파일 로그 파일
