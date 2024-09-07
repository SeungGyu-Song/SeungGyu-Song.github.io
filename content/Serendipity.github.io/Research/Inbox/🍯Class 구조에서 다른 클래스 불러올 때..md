[[OpenVins]] 코드에서 보면
본격적으로 class를 시작하기 전에 header파일에서 내가 참고해야할 class를 선언하는 것을 볼 수 있다.
즉, 예를 들어 현재 나는 Propagator.h 파일안에 있는데 State class를 parameter로 선언해주어야할 때 필요하니까 아래와 같이 작성할 수 있다.
```C++
### Propagator.h

#include <atomic>
#include <memory>
#include <mutex>

#include "utils/sensor_data.h"
#include "utils/NoiseManager.h"

namespace ov_msckf {
class State;

class Propagator {
public : 
...

bool fast_staet_propagate(std::shared_ptr<State> state, ...);

}


}
```

추가적으로, 실제 함수 안에서는 state안의 변수, 함수를 접근해야하니까 Propagator.cpp 파일 안에서  `#include "state/State.h`를 하는 것을 볼 수 있다.


---
반면 KLT OpticalFlow에서 Grider_GRID라는 class가 있는데 얘는 static 함수로만 이루어져있다. 즉, 객체를 선언할 게 아니라 그냥 함수를 활용하려고만 만든 함수라서 

TrackKLT.h에서는 얘를 굳이 위처럼 선언하지 않고, 그냥 include해서 불러온다.