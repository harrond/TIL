#LXC
Linux Containers로 단일 컨트롤 호스트 상에서 여러 개의 고립된 리눅스 시스템들을 실행하기 위한 운영 시스템 레벨 가상화 방법.
OS의 내부는 물리적 자원을 관리하는 Kernel공간과 사용자 프로세스를 실행하는 사용자 공간으로 나뉘는데 LXC는 사용자 공간을 여러 개로 나누어 각각의 사용자 프로세스에서 보이는 리소스를 제한 하는 것이다.
LXC는 cgroups와 namespace를 결합하여 애플리케이션을 위한 고립된 환경을 제공한다.

##KVM과 차이점
**KVM**과 같은 가상화 기술은 VM이 실제 물리적인 하드웨어를 Emulate하기 때문에 OS가 필요하다.
이 경우 VM을 실행하는 호스트 OS와 게스트 OS를 완전히 불리 할 수 있다는 장점이 있지만 오버 헤드가 증가하는 단점이 있다.
**Linux Container**는 모든 프로세스는 호스트 OS에서 바로 시작한다. 일반적인 프로세스의 동작과 다른 점은 그 과정의 일부를 그룹화하고 다른 그룹이나 그룹에 속하지 않는 프로세스에서 단절된 공간으로 동작하는 것이다. 이처럼 독립된 공간에 프로세스가 들어 있기 때문에 Container라고 부른다.
**즉, VM을 생성하는 것이 아닌 OS가 사용하는 자원을 분리하여 여러 환경을 만들 수 있도록 하는 것.**
Docker를 예로 들면 Host위에 Docker Engine이 떠서 수행을 하는데 VM처럼 Hardware를 가상화 해주는 것이 아닌 Container(Guest OS)를 Isolation해준다. Container의 OS는 기본적으로 Linux OS만 지원하는데 Container자체에 Kernel등의 OS이미지가 들어가 있는 것이 아니라 Kernel은 Host OS를 그대로 사용하고 Host OS와 Container의 OS의 다른 부분만 Container내에 같이 Packing 된다.
>예를 들어 Host OS가 Ubuntu이고 Container OS가 CentOS면 Container에는 Ubuntu와 CentOS의 차이가 되는 부분만 패키징이 된다.

##장점과 단점
####장점
1. 빠른 시작과 종료
2. 높은 집적도
3. 낮은 오버헤드
4. 애플리케이션 Container 지원
####단점
1. Host OS에 종속적
2. Container별 Kernel 구성이 불가능
##Container마다 분할되는 자원
*프로세스 테이블
Container마다 별도의 프로세스 테이블로 관리하여 Container의 프로세스에서 다른 Container의 프로세스가 보이지 않도록 한다.
*파일 시스템
Container마다 특정 디렉토리를 루트 파일 시스템으로 보이게 한다.
*네트워크
네트워크 네임 스페이스의 기능을 이용하여 Container마다 별도의 네트워크 설정을 구성한다.
*CPU, 메모리 장치
Cgroups의 기능은 Container에서 사용할 수 있는 범위를 제한한다.
