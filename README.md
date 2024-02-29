# SlothGwon.github.io
3D - AR



## Pytcharm 디버깅


**- MobaXterm 과 같은 터미널의 파일 실행 위치와, Pycharm의 디버깅에서 파일 실행 위치가 다를때에는 코드 상에서 아래의 os.chdir 함수를 사용하여 현재 위치를 수정해 주면 코드 위치를 통일시킬 수 있다**

import os\
os.chdir("/3DOD/GUPNet/code")

**- 위를 했음에도 pycharm 경로 탐색 버그가 생길시 아래의 코드를 사용하여, cahche경로에서 docker경로로 돌아올것**  
import os\
import sys\
BASE_DIR = os.path.dirname(os.path.abspath(\_\_file\_\_))\
ROOT_DIR = os.path.dirname(BASE_DIR)\
sys.path.append(ROOT_DIR)



**- F8을 누르며 디버깅시에, 변수 값이 보이지 않는다면 아래의 설정을 적용해 해결할 수 있다**

build, Execution, debelopment\
-python debugger\
--gevent compatilble 체크 할것




starter, ender = torch.cuda.Event(enable_timing=True), torch.cuda.Event(enable_timing=True)
repetitions = 300
timings=np.zeros((repetitions,1))

for _ in range(10):
    _ = model(dummy_input)
    

**- 모델을 GPU에서 돌릴때의 속도를 측정하기 위해서는 gpu가 시작될 때와 끝날때를 짚는것이 중요하다, 이를 위해서는 cuda.synchronize 함수를 사용해야한다**  

with torch.no_grad():  
    for rep in range(repetitions):  
        starter.record()  
        _ = model(dummy_input)  
        ender.record()  
        # WAIT FOR GPU SYNC  
        torch.cuda.synchronize()  
        curr_time = starter.elapsed_time(ender)  
        timings[rep] = curr_time  



**- Deformable conv시 디버깅이 안되는 버그가 있을경우**  

_C를 Import 하지 못하겠다는 버그 발생의 경우 환경이 detectron을 잡지 못하는 문제이다.  
프로젝트 폴더 안에 있는 detectron 폴더를 detectron__과같이 이름을 바꾸면 해결 할 수 있다



## SimKD  

**- Teacher model과 Student모델간의 공유되는 부분만 Student model로 가져오기 위해서는 아래의 코드를 사용해야한다**

model_dict = student_model.state_dict()  

pretrained_dict = {k: v for k, v in teacher_model_dict['model_state'].items() if k in model_dict}  
model_dict.update(pretrained_dict)  
student_model.load_state_dict(model_dict)  


## MonoRcnn
**- pycharm 에서 remote_source로 연결이 될때에**  

1. github에서 git clone 한다음 local 파일을 사용하기 위해선 아래의 코드를 입력하면 된다  
  
   python setup.py build develop  

2. path_mapping을 사용해 local폴더와 remote 폴더를 연결 해 준다


**- kitti bash 문제**
evaluate_object.cpp:12:10: fatal error: boost/numeric/ublas/matrix.hpp: No such file or directory  

apt-get update  
apt-get install libboost-all-dev  
입력


**3DODKD 구현**
MonoRCNN의 경우 json 파일을 읽어서 data loader 작성함\
이를 위해서 python prepare_KITTI_teacher.py 를 실행해 json 만들 필요가 있음









