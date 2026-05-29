# 한국어 문서 번역 manifest

이 파일은 프로젝트 안에서 사람이 읽는 텍스트 문서에 대해 생성한 한국어 번역본 목록입니다.

명명 규칙:
- 확장자가 있는 파일: `원본이름_KR.확장자`
  - 예: `README.md` -> `README_KR.md`
  - 예: `README.txt` -> `README_KR.txt`
- 확장자가 없는 파일: `원본이름_KR`
  - 예: `README` -> `README_KR`

번역 원칙:
- 원본 파일은 수정하지 않았습니다.
- prose는 한국어로 번역했습니다.
- 파일 경로, URL, 이메일 주소, 명령어, class/module/signal 이름, 코드 블록은 가능한 한 그대로 유지했습니다.
- `LICENSE_KR.md`는 비공식 한국어 번역입니다. 법적 기준은 원본 영어 `LICENSE.md`입니다.

## 생성한 한국어 텍스트 문서

- `LICENSE_KR.md`
- `README_KR.md`
- `README_SOC_KR.md`
- `Part_1/uvm_core_utilities/README_KR.md`
- `Part_1/uvm_core_utilities/src/README_KR`
- `Part_2-Putting_it_all_Together/README_KR.md`
- `Part_3_Stimulus_Generation/README_KR.md`
- `Part_5_Advanced_Topics/config_db_regular_expressions/src/README_KR.md`
- `Part_5_Advanced_Topics/CoverageClosure_non_UVM/doc/README_KR.txt`
- `Part_5_Advanced_Topics/CoverageClosure_non_UVM/doc/STATUS_KR.txt`
- `Part_5_Advanced_Topics/CoverageClosure_non_UVM/README_KR.md`
- `Part_5_Advanced_Topics/phase_callbacks/README_KR.md`
- `Part_5_Advanced_Topics/registers_example/README_KR.md`
- `Part_5_Advanced_Topics/spanning_phases/README_KR.md`
- `Part_5_Advanced_Topics/uvm_reactive_seq_slave/README_KR.md`
- `soc/docs/ethernet/README_KR.txt`
- `soc/docs/fpu/README_KR`
- `soc/docs/uart16550/CHANGES_KR.txt`
- `soc/docs/wb_conmax/README_KR.txt`
- `soc/docs/wb_conmax/STATUS_KR.txt`
- `soc/rtl/clkgen/README_KR`
- `soc/rtl/ethmac/README_KR`
- `soc/rtl/i2c_master_slave/README_KR`
- `soc/rtl/jtag/README_KR`
- `soc/rtl/jtag_tap/README_KR`
- `soc/rtl/rom/README_KR`
- `soc/rtl/simple_spi/README_KR`
- `soc/rtl/smii/README_KR`
- `soc/rtl/uart16550/README_KR`
- `soc/rtl/usbhostslave/README_KR`
- `soc/tb/uvm/ethernet/README_KR.md`
- `soc/tb/uvm/ethernet/src/layering/README_KR.md`
- `soc/tb/uvm/vga_lcd/README_KR.md`
- `soc/tb/uvm/wb_conmax/README_KR.md`
- `soc/tb/uvm/wb_conmax/tests/README_KR`
- `soc/tb/verilog_tb/uart16550/readme_KR.txt`
- `UVM_LEARNING_CHECKLIST.ko_KR.md`
- `lectures/day0_repo_orientation_KR.html`

## 이번에 별도 처리 대상으로 남겨둔 바이너리 문서

아래 PDF/DOC 파일들은 사람이 읽는 문서이지만, 텍스트 파일과 달리 별도 추출 및 대용량 번역 과정이 필요합니다. 현재 텍스트 문서 번역 범위에는 포함하지 않았습니다.

PDF:
- `Part_5_Advanced_Topics/CoverageClosure_non_UVM/doc/dma_doc.pdf`
- `soc/docs/common/wbspec_b3.pdf`
- `soc/docs/ethernet/eth_design_document.pdf`
- `soc/docs/ethernet/eth_speci.pdf`
- `soc/docs/ethernet/ethernet_datasheet_OC_head.pdf`
- `soc/docs/ethernet/ethernet_product_brief_OC_head.pdf`
- `soc/docs/fpu/FPU.pdf`
- `soc/docs/gpio/gpio_spec.pdf`
- `soc/docs/or1k/dvc-or1k-verification.pdf`
- `soc/docs/or1k/openrisc1200_spec.pdf`
- `soc/docs/smii/SMII.pdf`
- `soc/docs/spi_ctrl/simple_spi.pdf`
- `soc/docs/uart16550/UART_spec.pdf`
- `soc/docs/usb/ep0_rtl.pdf`
- `soc/docs/usb/phy_rtl.pdf`
- `soc/docs/usb/sie_rtl.pdf`
- `soc/docs/usb/usb_rtl.pdf`
- `soc/docs/usb/usb_testbench.pdf`
- `soc/docs/vga_lcd/vga_core.pdf`
- `soc/docs/wb_conmax/conmax.pdf`

DOC:
- `soc/docs/ethernet/src/eth_design_document.doc`
- `soc/docs/ethernet/src/eth_speci.doc`
- `soc/docs/ethernet/src/ethernet_datasheet_OC_head.doc`
- `soc/docs/ethernet/src/ethernet_product_brief_OC_head.doc`
- `soc/docs/gpio/src/gpio_spec.doc`
- `soc/docs/or1k/openrisc1200_spec.doc`

참고:
- DOC 파일 대부분은 같은 이름의 PDF가 함께 있습니다.
- PDF 전체 번역을 진행하려면 각 PDF에서 텍스트를 추출한 뒤 `_KR.md` 형태의 한국어 번역본을 만드는 방식이 가장 안전합니다.

## 추가 학습 artifact (번역 manifest 외)

아래 항목은 단순 번역본이 아니라, 이 로컬 학습 프로젝트를 위해 새로 생성한 한국어 학습 artifact입니다.

- `UVM_LEARNING_CHECKLIST.ko.md` - repo 기반 단계별 학습 체크리스트
- `lectures/index.html` - repo 실제 source excerpt 기반 HTML workbook index
- `lectures/day*.html` - Practical-UVM-Step-By-Step source-reading Day별 HTML workbook
- `lectures_chipverify_uvm/index.html` - ChipVerify UVM tutorial 기반 HTML workbook index
- `lectures_chipverify_uvm/day*.html` - ChipVerify source URL 기반 Day별 HTML workbook
- `lectures_chipverify_uvm/sources/chipverify_uvm_source_map.json` - ChipVerify source URL/title inventory
- `lectures_chipverify_uvm/sources/chipverify_uvm_curriculum.json` - Day 0~30 curriculum metadata
- `skills/uvm-practical-lecture-builder/SKILL.md` - repo-grounded workbook 생성/수정 skill
- `skills/chipverify-uvm-lecture-builder/SKILL.md` - ChipVerify 기반 workbook 생성/수정 skill
- `Daily_0529.md` - 2026-05-29 기준 진행상황 기록
