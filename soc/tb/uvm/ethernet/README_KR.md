이 파일은 메인 ethernet 예제입니다.
대체로 이 예제는 다음 내용을 보여줍니다.

1) 계층형 Sequence.
2) sequence 안에서의 Register 사용.
3) Interrupt Sequence
4) uvm_barrier 예제
5) UVM event 예제




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
       -tests/      ---> testbench module과 testcase를 포함합니다.
       |
       | - wb_env_tb_mod.sv
       | - wb_env_test.sv
       | - wb_env_test_phase_cb.sv   --- 실제로 살펴봐야 할 테스트입니다.
       |
       -run/        ---> Makefile
	| - Makefile
	| - simv.log -- run log 파일
	| - vcs.log  -- compile log 파일
       -src/        ---> Transaction, configuration, driver, monitor, master/slave subenv, scoreboard, coverage 관련 파일을 포함합니다.
        |common_if.sv
        |eth_base_pkt.sv
        |eth_blk_env_cfg.sv
        |eth_blk_env_cov.sv
        |eth_env_cfg.sv
        |eth_env_cov.sv
        |eth_phy_defines.v
        |eth_test_cfg.sv
        |eth_wrap_top.sv
        |layering  -> README를 참고하십시오. 이 파일들은 여러분을 위한 실습 과제입니다.
        |mac_transaction.sv
        |mii_if.sv   --> MII interface
        |mii_rx_agent.sv  -> 모든 MII 파일은 아래 참고를 보십시오.
        |mii_rx_drv.sv
        |mii_rx_mon.sv
        |mii_rx_seqr.sv
        |mii_scbd.sv
        |mii_transaction.sv
        |mii_tx_agent_sequence_library.sv
        |mii_tx_agent.sv
        |mii_tx_drv.sv
        |mii_tx_mon.sv
        |mii_tx_seqr.sv
        |mon_2cov.sv
        |ral_single.sv
        |reg_bus_adapters.sv
        |wb_config.sv
        |wb_env_cfg.sv
        |wb_env_cov.sv
        |wb_ethernet_mac_sequencer.sv
        |wb_ethernet_mac_sequence.sv
        |wb_eth_mac_hierarchical_seq.sv
        |wb_eth_scoreboard.sv
        |wb_eth_tx_library.sv
        |wb_eth_virt_seqr.sv
        |wb_master_agent_sequence_library.sv
        |wb_master_agent.sv
        |wb_master_behavioral.v
        |wb_master_if.sv
        |wb_master_mon.sv
        |wb_master_seqr.sv
        |wb_master.sv
        |wb_mii_sequence_library.sv
        |wb_model_defines.v
        |wb_package.sv
        |wb_slave_agent_sequence_library.sv
        |wb_slave_agent.sv
        |wb_slave_behavioral.v
        |wb_slave_if.sv
        |wb_slave_mem_mam.sv
        |wb_slave_mon.sv
        |wb_slave.my.sv
        |wb_slave_seqr.sv
        |wb_slave.sv
        |wb_transaction.sv
        |wb_virt_sequence.sv

* 모든 MII 파일은 기본적으로 템플릿입니다. 독자가 이 파일들을 바탕으로 완전한 environment를 만들 것을 기대합니다.
