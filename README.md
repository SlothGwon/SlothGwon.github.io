# SlothGwon.github.io
3D - AR



## Pytcharm 디버깅


**- MobaXterm 과 같은 터미널의 파일 실행 위치와, Pycharm의 디버깅에서 파일 실행 위치가 다를때에는 코드 상에서 아래의 os.chdir 함수를 사용하여 현재 위치를 수정해 주면 코드 위치를 통일시킬 수 있다**

import os
os.chdir("/3DOD/GUPNet/code")



**- F8을 누르며 디버깅시에, 변수 값이 보이지 않는다면 아래의 설정을 참고하여 보면 해결하게 될 수도 있다**

build, Execution, debelopment\
-python debugger\
--gevent compatilble 체크 할것



pycharm 경로 탐색 버그시 아래의 코드를 사용하여, cahche경로에서 docker경로로 돌아올것\
import os\
import sys\
BASE_DIR = os.path.dirname(os.path.abspath(\__file\__))\
ROOT_DIR = os.path.dirname(BASE_DIR)\
sys.path.append(ROOT_DIR)



