---
layout: single

title:  "관리자들의 관리자, Hpyervisor에 대하여"
excerpt: ""

categories:
    - Docker
tags: [DevOps, Docker, Virtualization, Hypervisor]

toc: true
author_profile: false
sidebar:
    nav: "docs"

date: 2022-08-03
last_modified_at: 2022-08-03
---

#### 각 벤더들이 정의하는 hypervisor
1. Redhat
    hypervisor란 운영체제로부터 H/W를 추상화하는 S/W 레이어이며 하나의 H/W 상에서 여러 OS가 구동이 가능하게 한다. hypervisor는 호스트 시스템에서 구동되며 가상머신들이 호스트 H/W 위 작동을 가능하게 한다.
2. VMWare
3. Xen.org

#### Hypervisor 종류
- Type I Hypervisor = native hypervisor = bare metal
  : OS 위가 아닌 H/W 위에서 바로 구동되어 시스템 자원의 스케줄링 및 할당을 지원한다. 이때 Hypervisor가 Guest OS의 H/W에 직접 접근을 지원하는 디바이스 드라이버를 제공한다. 예시로는 VMWare ESX, Xen 등이 있다.
- Type II Hypervisor = hosted VMM 
  hosted VMM이라는 이름처럼 hypervisor가 호스트 OS 위에 하나의 애플리케이션으로 호스팅되어 구동되는 방식이다.
  이때 호스트 OS는 VMM을 여타 프로세스들과 동일하게 취급한다.

  (게스트 OS의 입출력을 대신하는 주체가 뭔가? 호스트 OS? hypervisor)


이번엔 상용 제품을 비교 분석하며 Hypervisor가 실제로 어떻게 구현되고 있는지 살펴보자.

#### 상용 제품
1. Windows Hyper-V
Window Hyper-V는 x86-64 아키텍처를 위한 hypervisor 기반 가상화 시스템으로
고객들에게 신뢰할만한 가상화 환경과 통합적 관리를 제공하며, 비용을 절감시킨다.




2. KVM
KVM은 Kernel-based Virtual Machine의 줄임말로 리눅스 커널을 베어메탈 하이퍼바이저로 전환하는 loadable kernel module로 구현되어 있다. 
KVM은 하드웨어 가상화 extension를 지원하지 않는 CPU(Intel VT-X, AMD) 상에서는 구동되지 않는다. 
<br>
KVM은 두가지 모듈로 구성되어 있다.
- Kvm.ko : 코어 가상화 인프라스트럭쳐를 제공하는 loadable kernel module
- Kbm-[intel|amd].ko : 프로세서 지원을 위한 구체화 모듈(Intel 혹은 AMD)

3. XEN
Xen Hypervisor는 하드웨어 위에 직접적으로 얹는 S/W 레이어로 가상 Guest OS 여러 개를 안전하고, 효과적인 방식으로 동시 실행을 지원한다.

Xen Hypervisor는 core hypervisor 활동에 responsible 하다. 

Xen은 두 가지 중요한 구별되는 영역이 있다.
Dom 0 and Dom U. 
- Dom 0
    - a special priviledge modified running 
    - has special right to access phyiscal Linux OS.
    - create and configure Dom Us.
- Dom U = guset domains

- All Xen virtualization environments require Dom 0 to be running before any other virtual machine.`    

4. VMWare


#### 비유
- 하나의 H/W 자원으로부터 여러 OS를 돌릴 수 있다는 측면에서 다중인격 같은 느낌이 들었다.
- Type 2 Hypervisor에서 Guest OS는 점장/Hypervisor는 지부장/Host OS는 사장 느낌

#### 확인 문제
1. Hypervisor Type I과 Hypervisor Type II의 공통점/차이점을 각각 한 문장으로 서술하시오.
    공통점: 시스템 자원 사용의 효율화
    차이점: 1은 베어메탈 위에서 구동, 2는 운영체제 위에서 구동

2. Hypervisor Type I/II의 장점/단점에 대해 각각 서술하시오.
- I
- II
    - 장점: 
    - 단점: OS 레이어가 하나 더 있기에 -> Type 1에 비해 레이턴시 존재



3. I/II는 각각 언제 사용하면 좋을지 서술하시오.

---
#### 참고자료
1. https://www.techtarget.com/searchitoperations/tip/Whats-the-difference-between-Type-1-vs-Type-2-hypervisor
2. 