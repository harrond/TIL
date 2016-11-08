#KVM
 
###KVM이란?
Linux Kernel에서 지원하는 가상화로 Hypervisor를 메모리 관리자나 파일 시스템등과 같은 Kernel의 sub module로 취급한다.
+*Full virtualization(전 가상화)*방식
>Guest OS가 Hypervisor의 존재를 알지 못한다. Binary Translation기법으로 가상화

+*Para Virtualization(반 가상화)*방식
>Hypervisor에서 인식이 가능한 hyper call을 사용해 가상화

##제약
가상화를 제공하기 위해서는 CPU에서 *HVM(Hardware Virtual Machine)기능*을 제공해야 한다.

####HVM
>X86의 아키텍처의 HVM으로는 inter의 VT-x와 AMD의 SVM이 있다.
>가상화 기능이 벤더마다 다르므로 벤더 별로 구현해야 하는 단점이 있다.

