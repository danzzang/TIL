# computer Architecture

## 1. ARM 프로세서

> ARM (Advanced RISC Machine) 약자로 임베디드 기기에 주로 사용되는 32bit 프로세서



** 프로세서

> 메모리에 저장된 명령어들을 실행하는 유한 상태 오토마톤



#### 1) **RISC**

> RISC(Reduced Instruction Set Computer)는 CISC(Complex Instruction Set Computer)에 비해 명령어 구조가 간단하고 명령어 수가 적어 보다 빠르고 효율적인 처리가 가능 

> Host PC에서 사용하는 대부분의 프로세서는 CISC, 이 프로세서는 열이 많이 발생하기 때문에 반드시 열을 내려주는 냉각팬이 필요하다. 
>
> 하지만 RISC는 냉각팬이 필요하지 않다. 그만큼 부피가 작는 휴대기기를 만들 수 있다는 뜻 
>
> 그래서 대부분의 임베디드 시스템에서는 RISC 아키텍처를 선호한다.



** 명령어와 내부 레지스터가 32bit

> ARM Core에는 37개의 레지스터들이 있는데, 37개의 레지스터들 모두가 32bit의 길이를 가지고 있을 때, 32bit 구성이라고 부른다. 



#### 2) **ARM 전체 흐름**

<img src="http://pds23.egloos.com/pds/201112/25/90/c0098890_4ef7005727010.jpg" alt="img" style="zoom: 67%;" />

> 1) 메모리부터 CPU 안 (CPU Core)으로 패치 (Fatch)
>
> 2) ARM Core는 메모리부터 데이터를 읽어 드린 후, ARM 어셈블리 명령어로 해석 
>
> 	- ARM 어셈블리 명령어를 32 bit에 맞게 해석 되는 과정을 디코딩이라고 한다. 
> 	- 반드시 32bit 명령어 형태로 변환되는 것이 아닌, 컴파일 할 때 어떤 옵션을 사용했느냐에 따라 32bit or 16bit 명령어 형태로 변환된다.



** **Makefile**

> C언어로 만든 소스를 컴파일 하기 위해서 makefile을 많이 사용
>
> `-marm` 을  `-mthumb` 라는 옵션으로 하면 16bit 어셈블리 명령어로 만들어지게 한다.



** 두 가지 명령어가 시스템에 미치는 영향

> - ARM 명령어보다 THUMB 명령어는 메모리 공간도 효율적으로 사용하게 된다. 
> - Big Endian :vs: Little Endian 
>   - 개발자가 만든 소스를 컴파일하고 나면 바이너리가 생성되는데, 어떤 배열의 순서로 만들것인가를 결정



#### 3) ARM 구조

<img src="https://camo.githubusercontent.com/566b26ea8deb53645b0f78a525c81864b78fe7abf0d5bb627a74000132149ca6/68747470733a2f2f74312e6461756d63646e2e6e65742f6366696c652f746973746f72792f323537383843333535304341463837333141" alt="img" style="zoom:33%;" />

>RISC, 즉, 단순한 명령 집합은 적은 수의 트랜지스터만 필요하므로 간결한 설계와 더 작은 크기를 가능하게 한다. 따라서, 명령 집합의 수가 적기 때문에 트랜지스터 수가 적고 이를 통해 크기가 작고 전원 소모가 낮은 ARM CPU가 스마트폰, 테블릿 PC와 같은 모바일 기기에 많이 사용되고 있다. 



#### 4) ARM의 장점

> ARM을 위해 개발된 프로그램은 오직 ARM 프로세서가 탑재된 기기에서만 실행할 수 있다. 따라서 ARM에서 실행되던 프로그램을 x86 프로세서에서 실행되도록 하려면 프로그램에 수정이 가해져야 한다.
>
> 하지만, 하나의 ARM 기기에 동작하는 OS는 다른 ARM 기반 기기에서도 잘 동작한다. 덕분에 수 많은 버전의 안드로이드가 탄생하고 있으며,  HP나 블랙베리의 테블릿에서도 안드로이드가 탑재될 수 있는 가능성이 생기게 된 것.



## 2. Byte Order 

### 1. Big Endian (MSB - Most Significant Byte)

> 최상위 바이트부터 차례로 저장하는 방식

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/54/Big-Endian.svg/1200px-Big-Endian.svg.png" alt="엔디언 - 위키백과, 우리 모두의 백과사전" style="zoom: 25%;" />

** 빅 엔디안 장점

- 소프트웨어의 디버그를 편하게 해주는 경향이 있다. 사람이 숫자를 읽고 쓰는 방법과 같기 때문에



** 빅 엔디안 단점

- 메모리에 저장된 값의 하위 바이트들만 사용할 때, 변수 주소에 2바이트 또는 3바이트를 더해야 한다. 



### 2. Little Endian (LSB - Least Significant Byte)

> 최하위 바이트부터 차례로 저장하는 방식

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Little-Endian.svg/200px-Little-Endian.svg.png" alt="엔디언 - 위키백과, 우리 모두의 백과사전" style="zoom:150%;" />

** 리틀 엔디안 장점

- 메모리에 저장된 값의 하위 바이트들만 사용할 때 별도의 계산이 필요 없다. 

- 가산기가 덧셈을 하는 과정은 LSB부터 시작하여 자리 올림을 계산하기 때문에, 첫 번째 바이트가 LSB인 리틀 엔디언에서는 가산기 설계가 조금 더 쉽다.

  

<img src="https://www.researchgate.net/publication/335670464/figure/fig1/AS:800303620300800@1567818660327/Representation-of-0x1A2B3C4D5E6F7080-in-big-endian-and-little-endian.ppm" alt="Representation of 0x1A2B3C4D5E6F7080 in big-endian and little-endian. |  Download Scientific Diagram" style="zoom:50%;" />



### 3. Middle Endian	

> 두 경우에 속하지 않거나, 둘을 모두 지원하는 경우

