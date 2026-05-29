
WISHBONE DMA/Bridge 프로젝트 페이지는 다음과 같습니다:
http://www.opencores.org/cores/wb_dma/

저(Rudolf Usselmann)에 대해 더 알고 싶다면 다음을 방문하세요:
http://www.asics.ws

디렉터리 구조
-------------------
[core_root]
 |
 +-doc                        문서
 |
 +-bench--+                   테스트 벤치
 |        +- verilog          Verilog 소스
 |        +-vhdl              VHDL 소스
 |
 +-rtl----+                   Core RTL 소스
 |        +-verilog           Verilog 소스
 |        +-vhdl              VHDL 소스
 |
 +-sim----+
 |        +-rtl_sim---+       기능 검증 디렉터리
 |        |           +-bin   Makefile/실행 스크립트
 |        |           +-run   작업 디렉터리
 |        |
 |        +-gate_sim--+       기능 및 타이밍 게이트 레벨
 |                    |       검증 디렉터리
 |                    +-bin   Makefile/실행 스크립트
 |                    +-run   작업 디렉터리
 |
 +-lint--+                    Lint 디렉터리 트리
 |       +-bin                Makefile/실행 스크립트
 |       +-run                작업 디렉터리
 |       +-log                Linter 로그 및 결과 파일
 |
 +-syn---+                    Synthesis 디렉터리 트리
 |       +-bin                Synthesis 스크립트
 |       +-run                작업 디렉터리
 |       +-log                Synthesis 로그 파일
 |       +-out                Synthesis 출력
