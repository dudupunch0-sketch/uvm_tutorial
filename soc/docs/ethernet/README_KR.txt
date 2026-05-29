//////////////////////////////////////////////////////////////////////
////                                                              ////
////  README.txt                                                  ////
////                                                              ////
////  This file is part of the Ethernet IP core project           ////
////  http://www.opencores.org/projects/ethmac/                   ////
////                                                              ////
////  Author(s):                                                  ////
////      - Igor Mohor (igorM@opencores.org)                      ////
////                                                              ////
////                                                              ////
//////////////////////////////////////////////////////////////////////
////                                                              ////
//// Copyright (C) 2001, 2002 Authors                             ////
////                                                              ////
//// This source file may be used and distributed without         ////
//// restriction provided that this copyright statement is not    ////
//// removed from the file and that any derivative work contains  ////
//// the original copyright notice and the associated disclaimer. ////
////                                                              ////
//// This source file is free software; you can redistribute it   ////
//// and/or modify it under the terms of the GNU Lesser General   ////
//// Public License as published by the Free Software Foundation; ////
//// either version 2.1 of the License, or (at your option) any   ////
//// later version.                                               ////
////                                                              ////
//// This source is distributed in the hope that it will be       ////
//// useful, but WITHOUT ANY WARRANTY; without even the implied   ////
//// warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR      ////
//// PURPOSE.  See the GNU Lesser General Public License for more ////
//// details.                                                     ////
////                                                              ////
//// You should have received a copy of the GNU Lesser General    ////
//// Public License along with this source; if not, download it   ////
//// from http://www.opencores.org/lgpl.shtml                     ////
////                                                              ////
//////////////////////////////////////////////////////////////////////
//
// CVS Revision History
//
// $Log: not supported by cvs2svn $
//
//
//

ModelSIM에서 simulation/Testbench 실행하기:

ModelSIM project 열기: ethernet/sim/rtl_sim/modelsim_sim/bin/ethernet.mpf
macro do.do를 실행합니다(command window에 "do do.do" 입력).
Simulation은 자동으로 시작됩니다. 로그는 /log
directory에 저장됩니다. tb_ethernet test가 수행됩니다.



Ncsim에서 simulation/Testbench 실행하기:

ethernet\sim\rtl_sim\ncsim_sim\run directory로 이동합니다.
run_eth_sim_regr.scr script를 실행합니다. Simulation은 자동으로 시작됩니다. 로그는
/log directory에 저장됩니다. script를 다시 실행하기 전에 이전 실행에서 생성된
파일을 삭제하는 clean script를 실행하십시오. tb_ethernet test가 수행됩니다.






eth_cop.v, eth_host.v, eth_memory, tb_cop.v 및 tb_ethernet_with_cop.v
파일은 무엇에 사용됩니까?

testbench에는 traffic coprocessor가 포함되어 있지 않지만, coprocessor는
ethernet environment의 일부입니다. eth_cop는 4개 module 사이에서
두 개의 wishbone interface를 multiplex합니다:
- 첫 번째 wishbone master interface는 HOST(eth_host)에 연결됩니다.
- 두 번째 wishbone master interface는 Ethernet Core에 연결됩니다
  (memory(eth_memory)의 data에 접근하기 위함).
- 첫 번째 wishbone slave interface는 Ethernet Core에 연결됩니다
  (register 및 buffer descriptor에 접근하기 위함).
- 두 번째 wishbone slave interface는 memory(eth_memory)에 연결되어
  host가 memory에 data를 쓰거나 memory에서 data를 읽을 수 있게 합니다.

tb_cop.c는 traffic coprocessor(eth_cop) 전용 testbench입니다.
tb_ethernet_with_cop.v는 위에서 언급한 모든 module이 하나의 environment로
연결된 단순한 testbench입니다. 몇 개의 packet이 송신되고 수신됩니다.
"main" testbench는 tb_ethernet.v 파일입니다. 이 파일은 여러 test를 수행합니다
(eth_cop는 simulation environment의 일부가 아닙니다).
