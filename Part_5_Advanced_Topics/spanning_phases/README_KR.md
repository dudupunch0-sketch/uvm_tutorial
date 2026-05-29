
각 예제는 자체 완결형(SELF Contained)이 되도록 설계되었습니다.
다른 예제에서 반복되는 코드도 포함되어 있습니다.

일반적으로 각 예제에서 다른 예제와 차이가 있는 파일은 1~2개뿐입니다. *** 줄 사이의 영역을 보세요.

*********************
이 특정 예제에서 다른 예제와 다른 유일한 파일은 다음과 같습니다:
1) src 디렉터리의 wb_master_phase_mon.sv.
2) Environment 자체가 monitor를 instance화하고 VIF에 연결합니다.
*****************************************
이 예제들에서 다른 모든 파일은 PART_2의 예제와 다르지 않습니다

나머지 파일은 디렉터리를 그대로 복사해 두고
큰 작업 없이 바로 컴파일할 수 있도록 포함되어 있습니다.

위 파일의 monitor를 수정해 보면서 UVM에 대해 더 배우길 기대합니다.




*************************************************************
예제 컴파일 및 실행 단계
*************************************************************

참고:
  1) VCS 설치에 포함된 UVM1.0 내장 source를 포함하려면:
     Makefile에서 UVM_HOME 포함은 -ntb_opts uvm 명령으로 대체할 수 있습니다
  2) VCS 설치 디렉터리 외부의 UVM source를 사용하려면:
     환경 변수 VCS_UVM_HOME을 uvm-1.0 설치 디렉터리로 설정하세요

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
       | - wb_slave.sv     --- Slave driver
       | - wb_slave_mon.sv  -- Slave monitor
       | - wb_slave_if.sv   -- slave interface
       | - wb_transaction.sv  -- transaction class
       | - wb_slave_seqr.sv   -- Slave Sequencer. 이 예제에서는 사용되지 않습니다
       | - wb_master.sv     -- master driver
       | - wb_master_seqr.sv  -- master sequencer
       | - wb_master_agent_sequence_library.sv -- master를 위한 모든 sequence는 여기에 있습니다
       | - wb_master_if.sv  -- master interface
       | - wb_master_phase_mon.sv  -- master monitor
       | - wb_env_cov.sv   -- coverage
       | - wb_env_cfg.sv   -- env config class 예제입니다. 이 예제에서는 많이 사용되지 않습니다
       |
       -tests/      ---> testbench module과 testcase를 포함합니다
       |
       | - wb_env_tb_mod.sv
       | - wb_env_test.sv
       | - wb_env_test_phase_cb.sv   --- 실제로 살펴봐야 할 test입니다
       |
       -run/        ---> Makefile
