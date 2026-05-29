/////////////////////////////////////////////////////////////////////
////                                                             ////
////  Author: Srivatsa Vasudevan                                 ////
////          srivatsa@uvmbook.com                               ////
////                                                             ////
////                                                             ////
/////////////////////////////////////////////////////////////////////
////                                                             ////
//// Copyright (C) 2010-2015 Srivatsa  Vasudevan	         ////
////                                                             ////
//// 이 소스 파일은 Practical UVM 책과 함께 UVM을 배우기 위해 ////
//// 사용할 수 있습니다. 단, copyright statement를 어떤 방식으로도 ////
//// 변경하거나 파일에서 제거해서는 안 되며, 파생 작업에는 원래의 ////
//// copyright notice와 관련 disclaimer가 포함되어야 합니다.      ////
////                                                             ////
//// 독자가 이 책과 함께 UVM을 배우는 과정에서 파일을 자유롭게  ////
//// 복사하고 수정할 수 있도록 license가 부여됩니다.             ////
////                                                             ////
//// 그 밖의 명시적 또는 묵시적 사용에 대해서는 저자에게 문의하십시오 ////
////                                                             ////
////     이 소프트웨어는 어떠한 명시적 또는 묵시적 보증 없이       ////
//// ``AS IS'' 상태로 제공됩니다. 여기에는 상품성 및 특정 목적에 ////
//// 대한 적합성의 묵시적 보증도 포함되지만 이에 한정되지 않습니다. ////
//// 어떠한 경우에도 저자 또는 기여자는 직접적, 간접적, 우발적,  ////
//// 특별, 징벌적 또는 결과적 손해(대체 상품 또는 서비스 조달,    ////
//// 사용 손실, 데이터 손실, 이익 손실, 사업 중단 등을 포함하나   ////
//// 이에 한정되지 않음)에 대해 책임을 지지 않습니다. 이는       ////
//// 계약, 엄격 책임, 불법 행위(과실 포함) 등 어떤 책임 이론에   ////
//// 근거하든, 이 소프트웨어 사용으로 인해 어떤 방식으로 발생했든 ////
//// 마찬가지이며, 그러한 손해 가능성을 고지받은 경우에도 같습니다. ////
////                                                             ////
/////////////////////////////////////////////////////////////////////
이 파일은 메인 VGA LCD 예제입니다.
이 예제는 VGA LCD BLOCK에 대해 register model을 사용하는 방법을 보여주기 위한 것입니다.
    env -> top-level environment 파일
     |vga_lcd_env.ralf
     |ral_vga_lcd.sv
     |vga_lcd_env_cfg.sv
     |vga_lcd_env_cov.sv
     |ral_vga_lcd_env.sv
     |vga_lcd_env.sv
    tests -> UVM testcase
     |vga_lcd_env_tb_mod.sv
     |vga_lcd_env_test.sv
     |vga_lcd_env_base_test.sv
     |vga_lcd_test_pkg.sv
     |vga_lcd_reg_access.sv
     |vga_lcd_reg_hw_reset.sv
     |vga_lcd_reg_single_access.sv
     hdl
     |vga_lcd_env_top.sv
     |sync_check.v
     |test_bench_top.v
     |tests.v
     |wb_b3_check.v
     |wb_mast_model.v
     |wb_model_defines.v
     |wb_slv_model.v
     |vga_enh_top_wrap.sv
      run
      | Makefile
     src
     |vga_dvi_agent.sv
     |vga_dvi_mon.sv
     |ral_single.sv
     |mon_2cov.sv
     |vga_lcd_scbd.sv
     |vga_disp_txn.sv
     |vga_dvi_drv.sv
     |vga_dvi_agent_sequence_library.sv
     |vga_dvi_sqr.sv
     |wb_env_cfg.sv
     |wb_vga_disp_if.sv
     |reg_bus_adapters.sv
     |wb_env_cov.sv
     |wb_slave_agent.sv
     |wb_slave_if.sv
     |wb_config.sv
     |wb_slave_mon.sv
     |wb_slave.my.sv
     |wb_master_agent_sequence_library.sv
     |wb_slave_seqr.sv
     |license.txt
     |wb_transaction.sv
     |wb_package.sv
     |wb_slave_agent_sequence_library.sv
./README.md
