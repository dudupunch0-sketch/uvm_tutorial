참고:
책 인쇄본의 uvm_utilities 코드에는 몇 가지 오타가 있었습니다.
실제 코드에서는 이것들이 수정되었습니다. 잘못된 파일들이 선택되어 포함된 것입니다.


------------------------------------

책 Part 1의 예제들은 이 디렉터리 아래의 하위 디렉터리에 있습니다.
run 디렉터리에는 makefile이 3개 있습니다. simulator마다 하나씩 있습니다.

여러 가지 이유로 run 디렉터리에 다른 두 simulator의 로그 파일은 제공하지 않았다는 점을 참고해 주세요.
Questa 및 IUS simulator용 makefile은 CVC Bangalore의 Srinivasan Venkataraman이 제공했습니다. srini@cvcblr.com
그가 기여해 준 것에 감사드립니다.

VCS simulator용 makefile은 검증되었으며 로그 파일과 함께 run 디렉터리에 제공되었습니다.

커뮤니티 여러분께 부탁드립니다. 이 예제들을 실행하고, 다른 simulator에 필요한 조정을 한 뒤, 해당 로그 파일을 공유해 주세요.
로그 파일 기여는 진심으로 감사히 받겠습니다.



참고 사항:
IUS 및 Questa의 경우:
UVM tarball을 다운로드해 둔 위치로 환경 변수 UVM_HOME을 설정해야 할 수 있습니다. 이것은 makefile에 포함되어 있지 않습니다.
simulator에서 설정을 제공할 수도 있으니 문서를 확인해 보시기 바랍니다.
확실하지 않다면 다음에서 tarball을 다운로드할 수 있습니다: http://www.accellera.org/images/downloads/standards/uvm/uvm-1.2.tar.gz
압축을 풀고 UVM_HOME을 src/ 하위 디렉터리의 위치로 설정하세요.

VCS simulator의 경우, VCS에 번들로 포함된 내장 UVM 사본을 사용하도록 설정되어 있습니다.

이 파일들에 문제가 있으면 수정할 수 있도록 알려 주세요.
Questa 및 IUS에 대한 이 안내에 잘못된 점이 있고 해결 방법을 찾았다면, 변경 사항을 알려 주세요. main repository에 반영하겠습니다.

감사합니다!
Srivatsa
2018년 7월
