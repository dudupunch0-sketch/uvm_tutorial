

이 파일은 wb_conmax 예제에 대한 설명입니다. 컴파일하려면 이 디렉터리보다 한 단계 위에 있는 common 디렉터리의 코드가 필요합니다.


src 디렉터리의 거의 모든 파일은 이 예제와 관련이 있습니다.

특정 test를 실행하려면 다음을 실행하십시오.

make UVM_TEST=<name of test class>


*************************************************************
예제 컴파일 및 실행 절차
*************************************************************

참고:
  1) VCS 설치에 포함된 UVM1.2 내장 소스를 포함하려면:
     Makefile에서 UVM_HOME 포함 설정을 -ntb_opts uvm 명령으로 대체할 수 있습니다.
  2) VCS 설치 디렉터리가 아닌 다른 UVM 소스를 사용하려면:
     환경 변수 VCS_UVM_HOME을 uvm-1.2 설치 디렉터리로 설정하십시오.

*************************************************************
UVMGEN이 생성한 environment의 디렉터리 구조
*************************************************************
-EXAMPLE
	|
       -README.md (이 파일)
       |
       -hdl/        ---> top module과 모든 environment 파일 include를 포함합니다.
       |
       | - wb_env_top.sv  -- 모든 것을 인스턴스화하는 top-level 파일
       | - dut.v     -- 더미 DUT
       |
       -env/        ---> environment 관련 파일(environment, ralenv)을 포함합니다.
       |
       | - wb_slave_agent.sv  -- top-level slave agent 파일
       | - wb_master_agent.sv -- top-level master agent 파일
       | - wb_env_env.sv      -- 완전한 environment
       |
       -include/
       |
       -src/        ---> Transaction, configuration, driver, monitor, master/slave subenv, scoreboard, coverage 관련 파일을 포함합니다.
       |
       | - wb_slave.sv     --- Slave driver
       | - wb_slave_mon.sv  -- Slave monitor
       | - wb_slave_if.sv   -- slave interface
       | - wb_transaction.sv  -- transaction class
       | - wb_slave_seqr.sv   -- Slave Sequencer. 이 예제에서는 사용되지 않습니다.
       | - wb_master.sv     -- master driver
       | - wb_master_seqr.sv  -- master sequencer
       | - wb_master_agent_sequence_library.sv -- master용 모든 sequence는 여기에 있습니다.
       | - wb_master_if.sv  -- master interface
       | - wb_master_mon.sv  -- master monitor
       | - wb_env_cov.sv   -- coverage
       | - wb_env_cfg.sv   -- 예제로 제공되는 env config class입니다. 이 예제에서는 많이 사용되지 않습니다.
       |
       -tests/      ---> testbench module과 testcase를 포함합니다.
       |
        | - wb_env_tb_mod.sv
        | - wb_env_test.sv
	| - wb_conmax_alter_message.sv
	| - wb_conmax_alter_verbosity.sv
	| - wb_conmax_base_test.sv
	| - wb_conmax_commandline_test_1.sv
	| - wb_conmax_env_tb_mod.sv
	| - wb_conmax_factory_instance_override_cmdline.sv
	| - wb_conmax_factory_instance_override.sv
	| - wb_conmax_factory_type_override.sv
	| - wb_conmax_flat_sequence.sv
	| - wb_conmax_instance_callback_test.sv
	| - wb_conmax_parallel_sequence.sv
	| - wb_conmax_report_file.sv
	| - wb_conmax_sequence_config.sv
	| - wb_conmax_simple_cmdline_proc.sv
	| - wb_conmax_typewide_callback_test.sv

       -run/        ---> Makefile
	| - Makefile
	| - simv.log -- run log 파일
	| - vcs.log  -- compile log 파일
