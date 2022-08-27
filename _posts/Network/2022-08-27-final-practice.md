---
layout: single

title:  "\[Network\] 기말고사 실습"
excerpt: ""

categories: 
    - Network
tags: [network, final]

toc: true
author_profile: false
sidebar:
    nav: "docs"

date: 2022-08-27
last_modified_at: 2022-08-27
---

### 라우팅 및 서버 구성하기

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1e9585ea-d79f-4d9b-ae99-1eaf75e37ba5/Untitled.png)

```
1. 단말장치들 구성

2. Switch 구성
1) VLAN 데이터베이스 구축
Switch0의 설정
Switch>en
Switch# conf t
Switch(config)# vlan 10
Switch(config)# name Sales
Swicth(config)# vlan 20
Switch(config)# name Education
Swicth(config)# vlan 30
Switch(config)# name Marketing

2) VLAN이 소속된 해당 인터페이스에서 Access Mode로 동작하도록 연결
Switch(config)# int fa0/1
Switch(config)# switchport mode access
Switch(config)# switchport access vlan 10
Switch(config)# exit
Switch(config)# int fa0/2
Switch(config)# switchport mode access
Switch(config)# switchport access vlan 20
Switch(config)# exit
Switch(config)# int fa0/3
Switch(config)# switchport mode access
Switch(config)# switchport access vlan 30
Switch(config)# exit

3) 스위치에 트렁크 설정
Switch(config)# int fa0/24
Switch(config)# switchport trunk allowed vlan 10,20,30
Switch(config)# switchport mode trunk
Switch(config)# exit

3. Router에서의 설정
1) 기본 설정하기(fa0/0, s0/2/0)
Router> enable
Router# conf t
Router(config)# int fa0/0
Router(config)# ip add 210.20.1.2 255.255.255.0
Router(config)# no shut
Router(config)#exit
Router(config)# int s0/2/0
Router(config)# ip add 210.200.200.2 255.255.255.0
Router(config-if)# clock rate 56000
Router(config-if)# exit

2) Inter-VLAN Routing 설정하기
Router(config)# int fa0/0.10
Router(config-subif)# encapsulation dot1q 10
Router(config-subif)# ip add 210.20.10.1 255.255.255.0
Router(config-subif)# exit
Router(config)# int fa0/0.20
Router(config-subif)# encapsulation dot1q 20
Router(config-subif)# ip add 210.20.20.1 255.255.255.0
Router(config-subif)# exit
Router(config)# int fa0/0.30
Router(config-subif)# encapsulation dot1q 30
Router(config-subif)# ip add 210.20.30.1 255.255.255.0
Router(config-subif)# exit

3) RIPv2 라우팅 설정
Router(config)# router rip
Router(config-router)# version 2
Router(config-router)# network 210.200.200.2
Router(config-router)# network 210.20.1.2
Router(config-router)# network 210.20.10.0
Router(config-router)# network 210.20.20.0
Router(config-router)# network 210.20.30.0
Router(config-router)# no auto-summary
Router(config-router)# exit

4. ISP Router에서의 설정
1) 기본 설정(fa0/0, s0/2/0)
Router> enable
Router# conf t
Router(config)# hostname ISP
ISP(config)# int fa0/0
ISP(config-if)# no shut
ISP(config-if)# ip add 203.230.7.1 255.255.255.0
ISP(config-if)# exit

2) RIPv2 라우팅 설정
ISP(config)# router rip
ISP(config-router)# version 2
ISP(config-router)# network 210.200.200.3
ISP(config-router)# network 203.230.7.1
ISP(config-router)# no auto-summary
ISP(config-router)# exit

5. ping으로 연결 확인하기
PC0 / PC1 /PC2 / Router0 / ISP / TFT Server

6. ISP의 IOS를 TFTP 서버에 백업하기
ISP# show flash
ISP# copy flash tftp
Source filename[]?
Address or name of remote host[]? 203.230.7.2
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

7. PC0에서 TFTP 서버로의 웹 서버 접속
   [Desktop]의 Web Browser를 선택하고 URL에 
   http://203.230.7.2라고 입력하고 go를 클릭
```

### VTP

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/879fb933-b78a-4628-8774-01681cf0baef/Untitled.png)

주어진 네트워크 토폴로지를 참고하여 Switch0을 VTP 서버모드로 설정하고 나머지는 클라이언트 모드로 설정하시오.(단, 스위치간 VTP 도메인은 ‘vtptest’, 패스워드는 ‘vtppass’

```
**1. Switch0 설정**
Switch> en
Switch# conf t
Switch(config)# vtp version 2
Switch(config)# vtp domain vtptest
Switch(config)# vtp password vtppass
Switch(config)# int fa0/24
Switch(config)# switchport mode trunk

**2. Switch1, Switch2 설정**
Switch> en
Switch# conf t
Switch(config)# vtp version 2
Switch(config)# vtp mode version 2
Swtich(config)# vtp domain vtptest
Switch(config)# vtp password vtppass
Switch(config)# int fa0/24
Switch(config)# switchport mode trunk
```

### 라우터 기본 설정하기(RIPv2)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4539b6ca-b334-4041-9b06-8151d2bf4690/Untitled.png)

```
1. 위와 같이 구성하고 각 PC에 IP 주소를 세팅한다.
PC0: 203.230.7.2/24, GW: 203.230.7.1/24
PC1: 203.230.9.2/24, GW: 203.230.9.1/24
PC2: 203.230.8.2/24, GW: 203.230.8.1/24

2. 각 라우터의 기본 설정
1) Router0의 설정
Router> enable
Router# conf t
Router(config)# hostname R1
R1(config)# int fa0/0
R1(config-if)# ip add 203.230.7.1 255.255.255.0
R1(config-if)# no shut
R1(config)# exit
R1(config)# int se0/2/0
R1(config-if)# ip add 203.230.10.2 255.255.255.0
R1(config-if)# no shut
R1(config-if)# exit
R1(config-if)# int se0/2/1
R1(config-if)# ip add 203.230.11.2 255.255.255.0
R1(config-if)# no shut
R1(config)# exit

2) Router1의 설정
Router> enable
Router# conf t
Router(config)# hostname R2
Router(config)# int fa0/0
Router(config-if)# ip add 203.230.9.1 255.255.255.0
Router(config-if)# no shut
Router(config-if)# exit
Router(config)# int se0/2/0
Router(config-if)# ip add 203.230.10.1 255.255.2550
Router(config-if)# clock rate 64000
Router(config-if)# no shut
Router(config)# exit
Router(config)# int se0/2/1
Router(config)# ip add 203.230.12.2 255.255.255.0
Router(config-if)# clock rate 64000
Router(config-if)# no shut
Router(config)# exit

3) Router2의 설정

4) 각 PC와 라우터간 통신 확인(성공)

3. 라우팅 프로토콜 세팅하기(RIPv2)
1) R1의 라우팅 프로토콜 세팅하기
2) R2의 라우팅 프로토콜 세팅하기
3) R3의 라우팅 프로토콜 세팅하기
4) 각 PC와 라우터들간의 통신 확인
```

### 라우터 기본 설정하기(OSPF)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a6b41299-f28e-47df-b338-4e735f86b9ca/Untitled.png)

```
1. 위와 같이 구성하고 각 PC에 IP 주소를 세팅한다.
PC0: 203.230.7.2/24 GW: 203.230.7.1/24
PC1: 203.230.9.2/24 GW: 203.230.9.1/24
PC2: 203.230.8.2/24 GW: 203.230.8.1/24

2. 각 라우터의 기본 설정
1) Router0 설정
R1(config)# int loopback 0
R1(config-if)# ip add 1.1.1.1 255.255.255.0
R1(config-if)# exit

Router> enable
Router# conf t
Router(config)# hostname R1
R1(config-if)# int fa0/0
R1(config-if)# ip add 203.230.7.1 255.255.255.0
R1(config-if)# no shut
R1(config-if)# exit
R1(config)# int se0/2/0
R1(config-if)# ip add 203.230.10.2 255.255.255.0
R1(config-if)# no shut
R1(config-if)# exit
R1(config)# int se0/2/1
R1(config-if)# ip add 203.230.11.2 255.255.255.0
R1(config-if)# no shut
R1(config-if)# exit

1) Router1 설정
R2(config)# int loopback 0
R2(config-if)# ip add 2.2.2.1 255.255.255.0
R2(config-if)# exit

Router> enable
Router# conf t
Router(config)# hostname R2
R2(config-if)# int fa0/0
R2(config-if)# ip add 203.230.9.1 255.255.255.0
R2(config-if)# no shut
R2(config-if)# exit
R2(config)# int se0/2/0
R2(config-if)# ip add 203.230.10.1 255.255.255.0
R2(config-if)# clock rate 64000
R2(config-if)# no shut
R2(config-if)# exit
R2(config)# int se0/2/1
R2(config-if)# ip add 203.230.12.2 255.255.255.0
R2(config-if)# clock rate 64000
R2(config-if)# no shut
R2(config-if)# exit

1) Router2 설정
R3(config)# int loopback 0
R3(config-if)# ip add 3.3.3.1 255.255.255.0
R3(config-if)# exit

Router> enable
Router# conf t
Router(config)# hostname R3
R3(config-if)# int fa0/0
R3(config-if)# ip add 203.230.7.1 255.255.255.0
R3(config-if)# no shut
R3(config-if)# exit
R3(config)# int se0/2/0
R3(config-if)# ip add 203.230.10.2 255.255.255.0
R3(config-if)# no shut
R3(config-if)# exit
R3(config)# int se0/2/1
R3(config-if)# ip add 203.230.11.2 255.255.255.0
R3(config-if)# no shut
R3(config-if)# exit

3. 라우팅 프로토콜 세팅하기(OSPF)
1) R1의 라우팅 프로토콜 세팅하기
R1(config)# router ospf 7
R1(config-router)# router-id 1.1.1.1
R1(config-router)# network 203.230.7.0 0.0.0.255 a 0
R1(config-router)# network 203.230.10.0 0.0.0.255 a 0
R1(config-router)# network 203.230.11.0 0.0.0.255 a 0
R1(config-router)# network 1.1.1.0 0.0.0.255 a 0
R1(config-router)# exit

2) R2의 라우팅 프로토콜 세팅하기
R2(config)# router ospf 7
R2(config-router)# router-id 2.2.2.1
R2(config-router)# network 203.230.9.0 0.0.0.255 a 0
R2(config-router)# network 203.230.10.0 0.0.0.255 a 0
R2(config-router)# network 203.230.12.0 0.0.0.255 a 0
R2(config-router)# network 2.2.2.0 0.0.0.255 a 0
R2(config-router)# exit

3) R3의 라우팅 프로토콜 세팅하기
R3(config)# router ospf 7
R3(config-router)# router-id 3.3.3.1
R3(config-router)# network 203.230.8.0 0.0.0.255 a 0
R3(config-router)# network 203.230.11.0 0.0.0.255 a 0
R3(config-router)# network 203.230.12.0 0.0.0.255 a 0
R3(config-router)# network 3.3.3.0 0.0.0.255 a 0
R3(config-router)# exit

4) 각 PC와 라우터들간의 통신 확인
R1(config)# do show ip route
R2(config)# do show ip route
R3(config)# do show ip route
```

### PPP

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/41a237bb-0822-4e59-8f9b-53f89e7c807a/Untitled.png)

```
PC0: 163.180.116.2/24, GW: 163.180.116.1/24(Router0의 Fa0/0)
PC1: 150.183.235.2/24, GW: 150.183.235.1/24(Router1의 Fa0/0)
Router0의 Se0/2/0 : 203.230.7.1/24
Router1의 Se0/2/1 : 203.230.7.2/24

Router# conf t
Router(config)# hostname R1
R1(config)# int fa0/0
R1(config-if)# ip add 163.180.116.1 255.255.255.0
R1(config-if)# no shut
R1(config-if)# exit
R1(config)# int s0/2/0
R1(config-if)# ip add 203.230.7.1 255.255.255.0
R1(config-if)# clock rate 64000
R1(config-if)# no shut
R1(config-if)# exit
R1(config)# router rip
R1(config-router)# version 2
R1(config-router)# network 163.180.0.0
R1(config-router)# network 203.230.7.0
R1(config-router)# exit
---------------------------------------------------
Router# conf t
Router(config)# hostname R2
R2(config)# int fa0/0
R2(config-if)# ip add 150.183.235.1 255.255.255.0
R2(config-if)# no shut
R2(config-if)# exit
R2(config)# int s0/2/1
R2(config-if)# ip add 203.230.7.2 255.255.255.0
R2(config-if)# no shut
R2(config-if)# exit
R2(config)# router rip
R2(config-router)# version 2
R2(config-router)# exit

R1(config)# do show interfaces s0/2/0
---------------------------------------------------
...
Encapsulation HDLC, loopback not set, keepalive set(10 sec)
...
---------------------------------------------------
R1# conf t
R1(config)# username R2 password infocomm
R1(config)# int s0/2/0
R1(config-if)# encapsulation ppp
R1(config-if)# ppp authentication pap
R1(config-if)# ppp pap sent-username R1 password infocomm
R1(config-if)# exit

R2# conf t
R2(config)# username R1 password infocomm
R2(config)# int s0/2/1
R2(config-if)# encapsulation ppp
R2(config-if)# ppp authentication pap
R2(config-if)# ppp pap sent-uesrname R2 password infocomm
R2(config-if)# exit
---------------------------------------------------
R1(config)# do show interfaces s0/2/0
확인: Encapsulation PPP, loopback not set, keepalive set(10 sec)
```

### Port-Security

![as.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c1933900-8de0-4b1a-baac-b5136a1e9af4/as.png)

```
1. Switch0에서의 설정
1) MAC 주소가 최대 1개 이상 감지되면 fa0/1 회선을 다운시켜보자.
Switch> en
Switch> conf t
Switch(config)# int fa0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport port-security
Switch(config-if)# switchport port-security maximum 1
Switch(config-if)# switchport port-security violation shutdown
Swicth(config-if)# exit

[실습]
- PC0에서 PC2로 ping 테스트 : 성공
- PC1에서 PC2로 ping 테스트 : 회선 다운
다운된 회선 복구하려면
Switch(config)# int fa0/0  // 해당 인터페이스 접속
Switch(config-if)# shut    // 비활성화
Switch(config-if)# no shut // 다시 활성화 

2) PC1의 MAC 주소를 수동으로 Switch0에 등록하고 PC0와 PC2를 통신해보자.
Switch(config)# int fa0/1
Switch(config-if)# switchport mode access
Switch(config-if)# swithcport port-security
Switch(config-if)# switchport port-security maximum 1 
Switch(config-if)# switchport port-security mac-address 000D.BDD4.6A81
Switch(config-if)# switchport port-security violation shutdown
Switch(config-if)# exit

[실습]
- PC0에서 PC2로 ping 테스트 : 바로 회선 다운
§ Port-Security 취소하려면
Switch(config)# int fa0/1   // 해당 인터페이스 접속
Switch(config-if)# no switchport port-security

§ MAC 주소 알아보려면
PC0를 클릭하고 [Desktop]의 [Command Prompt] 상에서 PC> ipconfig /all이라고 명령한다
```

### Access-List 설정하기

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7a472cdb-9eeb-45ee-a4e1-03772dfa5ad7/Untitled.png)

```
1. 첫째날 "소규모 WAN 구성하기"의 네트워크 구성에 이어서 실습한다.
1) Router1에 telnet 접속을 시도할 수 있도록 설정
Router> en
Router# conf t
Router(config)# line vty 4 0
Router(config)# password pass
Router(config)# login
Router(config)# exit

PC0에서 telnet 203.230.9.1을 시도한다.
Server0에서 telnet 203.230.9.1을 시도한다.

2) Router1에 Access-List를 접속해보자. 
   PC0를 제외하고는 telnet 접속이 되지 않도록 설정하자.
Router# conf t
**Router(config)# access-list 1 permit host 203.230.7.2
Router(config)# username master password passon
Router(config)# line vty 0 4
Router(config-line)# access-class 1 in
Router(config-line)# login local**
Router(config)# exit

PC0에서 telnet 203.230.9.1을 시도한다.
Server0에서 telnet 203.230.9.1를 시도한다.
```