---
layout: single

title:  "리눅스 마스터 1급 기출문제 정리 (1)"
excerpt: ""

categories: 
    - Linux
tags: [Linux, Certificates]

toc: true
author_profile: false
sidebar:
    nav: "docs"

date: 2022-08-23
last_modified_at: 2022-08-23
---

### 1 과목. 리눅스 실무의 이해

1. 
SLS(Softlanding Linux System) : 1992에 발표된 초기 리눅스 배포판
Slackware : 1993에 패트릭 볼커딩에 의해 개발
Debian : 1993에 출시되었으며, 패키지 설치 및 관리의 단순함이 특징
SUSE : 1994에 출시되었으며, 유료 라이선스인 SUSE Linux Enterprise와 무료 버전인 openSUSE로 구분됨
Fedora : 2003에 출시되었으며, RPM 기반의 소프트웨어가 결합된 리눅스 배포판
Ubuntu : 2004년에 출시되었으며, 사용자 편의성에 초점을 맞춘 리눅스
CentOS : 2004년에 출시되었으며, RHEL(RedHat Enterprise Linux)과 호환을 강조한 리눅스 배포판
**Fedora, CentOS는 레드헷 계열**의 리눅스이며, **Ubuntu는 데비안** 계열 리눅스

2. 
- Knoppix : 데비안 계열의 리눅스로 컴퓨터 구동 시압축된 파일을 램 디스크에 풀어서 바로 사용하는 **Linux Live Image(CD)**가 특징임
- BackTrack : 슬랙스 등을 기반으로 정보보안을 테스트하기 위한 도구 내장. 현재 지원 종료
- Linux Mint : 독점 소프트웨어인 자바, 플래시 등을 기본으로 포함하여 편리함 강조

3. 
- GPL : 수정한 소스코드 혹은 GPL 소스코드를 활용한 S/W 모두 GPL로 공개해야 함
- MPL : 수정한 소스코드를 MPL로 공개해야 함. 단, 단순히 활용만 할 경우 공개하지 않아도 됨
- BSD : 라이선스 및 저작권을 명시해야 함. 배포 시 라이선스 사본 첨부에 대한 내용은 명시되어 있지 않음

4. 
- 파이프 : 프로세스의 표준 출력을 다른 프로세스의 표준 입력으로 보낼 수 있는 IPC 방식
- 라이브러리 : 수정한 소스코드를 MPL로 공개해야 한다. 단, 단순히 활용만 할 경우 공개하지 않아도 됨
- 가상 콘솔 : 라이선스 및 저작권을 명시해야 함. 배포 시 라이선스 사본 첨부에 대한 내용은 명시되어 있지 않음

5. 
- Arduino : 오픈소스 하드웨어와 소프트웨어를 기반으로 하는 단일 마이크로컨트롤러 보드와 개발 환경
- Micro Bit : 오픈소스 하드웨어와 ARM 기반의 임베디드 시스템
- Scratch : 그래픽 환경에서 코딩을 할 수 있는 프로그래밍 언어와 관련 도구

6. 
- LVM(Logical Volume Storage): 가상의 블록 스토리지를 구성하여 디스크 자잋를 논리적으로 관리하는 시스템
  유연한 용량 조절, 크기 조절이 가능한 스토리지 풀, 디스크 스트라이핑 및 미러 설정 등의 정점이 있다.
  - PV(Physical Volume) : 블록 장치 전체 혹은 파티션들을 LVM에서 사용할 수 있도록 변환한 것을 의미
  - PE(Physical Extent) : PV를 구성하는 일정한 크기의 블록으로 LVM2에서 기본 4MB의 크기를 가짐
  - LV(Logical Volume) : PV들의 집합으로 LV를 할당할 수 있음
  - LE(Logical Extent) : LV를 구성하는 일정한 크기의 블록으로 PE가 1:1 매핑됨

7. 
- RAID-6는 2차 패리티 정보를 분산 저장하여 2개의 저장 장치에 문제가 발생한 경우에도 복구할 수 있다. N개의 디스크를 RAID-6 형식으로 구성할 경우,
  실제 사용 가능한 용량은 (N-2)개의 디스크 크기와 같음 
- 6개의 HDD를 RAID-6로 구성할 경우 실제 사용 가능한 디스크 공간은 4개가 되므로, 약 66.7% 비율이 됨

8. 
- 시그널 ? 커널이나 프로세스가 다른 프로세스에게 비동기적으로 event를 전달하기 위해 사용하는 기능
- 시그널을 받은 프로세스는 해당 event에 적절한 동작으로 반응
  - SIGHUP  (1)  : 로그아웃 혹은 모뎀 접속을 끊음
  - SIGINT  (2)  : Ctrl + c를 입력하면 발생하며, 프로세스 종료
  - SIGQUIT (3)  : Ctrl + \를 입력하면 밣생하며, 코어 덤프와 함꼐 프로세스 종료
  - SIGKILL (9)  : 프로세스를 즉시 종료
  - SIGTERM (15) : 소프트웨어 종료 시그널로 tracking이 가능함
  - SIGCONT (18) : SIGSTOP 혹은 SIGTSTP에 의해 정지된 프로세스를 다시 실행
  - SIGSTOP (19) : 정지 시그널로 프로세스를 무조건 정지시킴
  - SIGTSTP (20) : Ctrl + z를 입력하면 발생하며, 프로세스의 실행을 정지시킨 후 다시 실행하기 위해 대기. tracking 가능

9. 
- set : Bash의 셸 변수를 관리하는 명령어로 `set NAME=VALUE`의 형식, 혹은 `NAME=VALUE`와 같이 생략된 형식을 사용할 수 있음 
        인자 없이 set명령만 실행하면 현재 설정된 값을 출력함 
- unset : set으로 설정한 값을 제거
- env : OS의 환경변수를 관리하는 명령어로 `env NAME=VALUE`로 설정 `env -u NAME`으로 제거
        인자없이 env 명령만 실행하면 현재 설젇된 환경변수 값을 출력
- export : **셸 변수를 환경변수로 사용할 수 있도록 하는 명령어**

10. 
- xauth : 사용자의 $HOME/.Xauthority 파일 안에 있는 MIT-MAGIC-COOKIEs 키 값을 이용하여 X 서버에 대한 접근을 제어함
- xhost : X 서버에 접근 가능한 클라이언트를 지정 혹은 해제하는 명령어
  - `xhost + [IP 혹은 도메인명]`으로 접근 허용
  - `xhost - [IP 혹은 도메인명]`으로 접근 해제

11. 
지문에서 제시된 허가권은 brw-rw----로 파일 유형이 블록 디바이스이다.
따라서 하드웨어 장치에 대한 장치 파일을 저장하고 있는 /dev가 가장 적절한 답안이다.
- /boot : 커널 파일이나 initrd 등 부팅이 필요한 파일이 위치하는 디렉터리
- /proc : 메모리에 존재하는 모든 프로세스들이 파일 형태로 매핑됨. 이 디렉터리를 통해 프로세스의 상태 정보, 하드웨어 정보, 기타 시스템정보를 확인할 수 있음
- /var : 로그, 스풀 파일 등 임시로 생성되거나 상황에 따라 생성되거나 삭제될 수 있음

12. 
- exec : 현재 실행 중인 프로세스를 새로운 프로세스(명령)로 상태 변경하여 실행
- fork : 자식 프로세스를 만드는 방법으로, 부모 프로세스의 상태를 복사하여 새로운 자식 프로세스를 만들고 실행
- standalone : 서비스를 담당하는 프로세스(데몬)을 항상 실행하여 서비스하는 방식으로, 
  메모리 등의 자원을 계속 차지한다는 부담이 있지만 상대적으로 많은 사용자에게 빠른 응답을 제공할 수 있음

13. (8)과 동일 

14.  
- history : 입력한 명령어 목록을 확인하는 명령이며 `history [숫자]`의 명령 형식으로 최근 입력한 명령어 중 원하는 개수만을 확인할 수 있음
- !5 : history로 확인할 수 있는 명령어 목록 중 5번째 항목을 재실행

15. 
- Xfce : 유닉스 계열 플랫폼을 위한 데스크톱 환경으로 GTK 툴킷을 기반으로 함  
- KWin : X 윈도우 시스템의 창 관리자(Window Manager)
- Metacity : GNOME2 데스크톱 화녕을 위한 기본 창 관리자
- Mutter : GNOME3 데스크톱 환경을 위한 기본 창 관리자로 Metacity를 대체함

16. 
- /etc/sysconfig/network-scripts/ifcfg-eth0 : eth0 네트워크 장치의 설정 파일
- /etc/sysconfig/network-scripts/ifcfg-eth0의 주요설정 항목
  - DEVICE : 설정 대상이 되는 네트워크 인터페이스 이름 지정
  - BOOTPROTO : IP 주소 할당 방법 설정
  - HWADDR : 네트워크 장치의 MAC 주소 지정
  - BROADCAST : 브로드캐스트(Broadcast) 주소 지정
  - IPADDR : IP 주소 지정 
  - NETMASK : 넷마스크 지정
  - NETWORK : 네트워크 주소 지정
  - GATEWAY : 게이트웨이 주소 지정
  - ONBOOT : 시스템 시작 시 자동 활성화 여부 설정
  - PEERDNS :  DHCP 서버의 DNS 정보를 resolv.conf 파일에 저장할지 사용 ㅕ부를 설정
  - DNS1 : 1차 DNS 서버의 주소지정
  - DNS2 : 2차 DNS 서버의 주소지정
  - USRCTL : 일반 계정 권한으로 제어할 수 있는지 허가 여부 설정
  - NM_CONTROLLED : 네트워크 매니저 사용 여부 설정

17. 
재부팅하거나 네트워크 데몬을 설치하면 /etc/sysconfig/network-scripts/ifcfg-eth0 환경설정 파일에 따라 네트워크가 재설정됨
즉 ifconfig 및 route로 직접 설정한 것은 삭제됨

18. 
- 도메인 네임은 국제 인터넷 주소지원 관리기관에서 관리
- 도메인은 도메인 레지스트리를 이용하여 관리하며, 인터넷에서 도메인 이름을 이용하여 시스템에 접속할 수 있도록 한다.

19. 

20. 
cron 설정 파일은 /var/spool/cron/에 위치함
사용자가 ihduser이므로 /var/spool/cron/ihduser가 정답임

21. 



