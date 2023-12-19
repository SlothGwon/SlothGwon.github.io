# SlothGwon.github.io
3D - AR



## Pytcharm 디버깅


**- MobaXterm 과 같은 터미널의 파일 실행 위치와, Pycharm의 디버깅에서 파일 실행 위치가 다를때에는 코드 상에서 아래의 os.chdir 함수를 사용하여 현재 위치를 수정해 주면 코드 위치를 통일시킬 수 있다**

import os
os.chdir("/3DOD/GUPNet/code")



**- F8을 누르며 디버깅시에, 변수 값이 보이지 않는다면 아래의 설정을 적용해 해결할 수 있다**

build, Execution, debelopment\
-python debugger\
--gevent compatilble 체크 할것



**- pycharm 경로 탐색 버그시 아래의 코드를 사용하여, cahche경로에서 docker경로로 돌아올것**  

import os\
import sys\
BASE_DIR = os.path.dirname(os.path.abspath(\_\_file\_\_))\
ROOT_DIR = os.path.dirname(BASE_DIR)\
sys.path.append(ROOT_DIR)


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



## SimKD

model_dict = student_model.state_dict()  

pretrained_dict = {k: v for k, v in teacher_model_dict['model_state'].items() if k in model_dict}  
model_dict.update(pretrained_dict)  
student_model.load_state_dict(model_dict)  




