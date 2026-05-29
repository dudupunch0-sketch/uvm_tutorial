//////////////////////////////////////////////////////////////////////
////                                                              ////
////  readme.txt                                                  ////
////                                                              ////
////                                                              ////
////  이 파일은 "UART 16550 compatible" 프로젝트의 일부입니다. ////
////  http://www.opencores.org/projects/uart16550/                ////
////                                                              ////
////  이 프로젝트 관련 문서:                                      ////
////  http://www.opencores.org/projects/uart16550/                ////
////                                                              ////
////  프로젝트 호환성:                                            ////
////  - WISHBONE                                                  ////
////  RS232 Protocol                                              ////
////  16550D uart (대부분 지원됨)                                 ////
////                                                              ////
////  개요(주요 기능):                                            ////
////  테스트 목적의 device interface                              ////
////                                                              ////
////  알려진 문제(제한 사항):                                     ////
////                                                              ////
////  할 일:                                                      ////
////  없음.                                                       ////
////                                                              ////
////  저자:                                                       ////
////      - Igor Mohor (igorm@opencores.org)                      ////
////                                                              ////
////  생성 및 업데이트:   (수정 이력은 log를 참조)                ////
////                                                              ////
////                                                              ////
//////////////////////////////////////////////////////////////////////
////                                                              ////
//// Copyright (C) 2001 Authors                                   ////
////                                                              ////
//// 이 소스 파일은 이 copyright statement가 파일에서 제거되지 않고 ////
//// 모든 파생 작업이 원래의 copyright notice와 관련 disclaimer를 ////
//// 포함한다는 조건하에 제한 없이 사용 및 배포될 수 있습니다.    ////
////                                                              ////
//// 이 소스 파일은 free software입니다. Free Software Foundation이 ////
//// 공표한 GNU Lesser General Public License 조건에 따라 이를    ////
//// 재배포하거나 수정할 수 있습니다. License 버전 2.1 또는       ////
//// (선택에 따라) 그 이후 버전을 사용할 수 있습니다.             ////
////                                                              ////
//// 이 소스는 유용할 것이라는 희망으로 배포되지만, 어떠한 보증도 ////
//// 제공되지 않습니다. 상품성 또는 특정 목적에 대한 적합성의     ////
//// 묵시적 보증도 없습니다. 자세한 내용은 GNU Lesser General     ////
//// Public License를 참조하십시오.                               ////
////                                                              ////
//// 이 소스와 함께 GNU Lesser General Public License 사본을 받아야 ////
//// 합니다. 받지 못했다면 다음에서 다운로드하십시오.             ////
//// http://www.opencores.org/lgpl.shtml                          ////
////                                                              ////
//////////////////////////////////////////////////////////////////////
//
// CVS 수정 이력
//
// $Log: not supported by cvs2svn $
//
//
//
//


다음 파일들은 UART16550 PHY를 구성하며 테스트에 사용됩니다.

uart_device_if_defines.v  - PHY 관련 define
uart_device_if_memory.v   - PHY 초기화를 위한 module (vapi.log 파일에서 command 읽기)
uart_device_if.v          - 테스트를 위한 추가 기능이 있는 UART PHY
vapi.log                  - command가 들어 있는 파일(expected data, 보낼 data 등)
readme.txt                - 이 파일




OPERATION:
uart_device_if.v는 uart PHY이며 uart_top.v에 연결됩니다. PHY는 vapi.log 파일에서 command를 가져옵니다.
command에 따라 다음을 수행할 수 있습니다.
- mode 설정(5, 6, 7, 8-bit, parity, stop bits 등)
- frequency divider(dll) 설정
- character 전송
- character 수신 및 예상 값과 비교
- glitch 전송(특정 시간이 지난 후)
- break 전송
- break 감지
- fifo가 비어 있는지/비어 있지 않은지 확인(예상 값이 실제 값과 다르면 error 생성)
- delay(특정 수의 character 동안 아무 작업도 하지 않음)

uart의 반대쪽에는 PHY를 제어하는 어떤 형태의 host가 연결되어야 합니다.

구조는 다음과 같습니다.


 ||||||||||||||              ||||||||||||||||              ||||||||||||||||
 |            |              |              |              |              |
 |   Host     | <----------> |    UART      | <----------> |     PHY      |
 |            |              |              |              |              |
 ||||||||||||||              ||||||||||||||||              ||||||||||||||||


PHY는 host가 UART를 어떻게 설정하는지 알고 같은 mode로 동작해야 합니다. 또한 host가 무엇을 보내는지 또는 무엇을 수신할 것으로 기대하는지도 알아야 합니다. PHY의 동작은 vapi.log 파일에 작성해야 합니다.

이 testing environment를 사용할 때 저는 OpenRISC1200을 host로 사용했습니다. 모든 것이 완전히 동작합니다. UART는 hardware에서도 테스트되었으며(서로 다른 두 보드), interrupt mode와 polling mode 양쪽에서 uCLinux를 실행했습니다.
