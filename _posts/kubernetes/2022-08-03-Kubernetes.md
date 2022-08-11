---
layout: single

title:  "Kubernetes란"
excerpt: "Kubernetes의 기능을 학습하고, 이를 기반으로 정의해보자"

categories:
    - Kubernetes
tags: [DevOps, Kubernetes]

toc: true
author_profile: false
sidebar:
    nav: "docs"

date: 2022-08-03
last_modified_at: 2022-08-03
---

## 쿠버네티스 클러스터 구성 방법
1. 로컬 쿠버네티스 - 물리 머신 한 대 -> 클러스터 구축
    - 네트워크 연결되지 않아도 바로 눈으로 확인할 수 있음 => 개발/테스트 적합
    - 이중화 X => 서비스 환경 적합 X 
2. 쿠버네티스 구축 도구-> 온프레미스/클라우드에 클러스터 구축

3. 관리형 쿠버네티스 서비스 -> 퍼블릭 클라우드의 관리형 서비스로 제공하는 클러스터 사용

개발 부서와 공유하여 사용하는 스테이징 및 서비스 환경을 클러스터는 
쿠버네티스 구축 도구나 관리형 쿠버네티스 서비스를 사용하는 것이 좋다.

가능한 관리형 k8s 서비스를 사용하고, 
k8s 구축 도구는 온프레미스에 배포하는 경우나 세밀한 커스터마이즈가 필요한 경우 사용한다.

k8s의 제공 기능 중 환경에 따라 제한 가능한 기능들
1. 외부 로드 밸런서와의 연계
2. 동적 연구 볼륨 프로비저닝

쿠버네티스 적합성 인증 프로그램(Certified Kubernetes Conformance Program)
- by CNCF
- 클러스터 기능 동작의 일관성과 이식성을 보장하려고 만들어진 곳
- 각 환경의 k8s 개발자는 먼저 이 내용을 준수하고 각 플랫폼 ㅌ특징을 살려 기능을 확장해 나간다.


1. 로컬 쿠버네티스
    - by Minikube
    - Docker Desktop for Mac/Windows
    - kind(Kubernetes in Docker)
2. k8s 구축 도구
    - kubeadm
    - Rancher
3. 퍼블릭 클라우드 관리형 k8s 서비스
    - Google Kubernetes Engine(GKE) 
    - Azure Kubernetes Service(AKS)
    - Elastic Kubernetes Service(EKS)

위의 방법들로 구축된 환경은 모두 쿠버네티스 적합성 인증 프로그램에서 인증된 
Certified Kubernetes Distribution/Platform이다.


#### 미니큐브
- 물리 머신에 로컬 쿠버네티스를 쉽게 구축하고 실행할 수 있는 도구
- SIG-Cluster-Lifecycle에서 만듦
- 단일 노드 구성 -> 여러 대의 구성이 필요한 k8s 기능 구현 제한
- 로컬 가상 머신에 k8s 설치 위해선 hypervisor 필요
    - Windows : Docker/VirtualBox/Hyper-V
    - Linux : Docker/VirtualBox/Podman/KVM/Bare Metal
    - MacOs

#### Docker Desktop for Mac/Windows
``` bash
# 컨텍스트 변경
$ kubectl config use-context docker-desktop
Switched to context "docker-desktop"
```

kubectl에서는 로컬 머신에 기동 중인 도커 호스트를 k8s 노드로 인식한다.
``` bash
# 노드 확인
$ kubectl get nodes
NAME            STATUS  ROLES   AGE     VERSION
docker-desktop  Ready   master  2m44s   v16.6-beta.0
```

k8s 클러스터 기능을 담당하는 component 그룹도 컨테이너로 기동된다.
k8s 활성화 시 Show system containers(advance)로 활성화하면 
docker contianer ls 명령어로 구성 요소를 확인할 수 있다.
``` bash
# 기동 중인 쿠버네티스 관련 구성 요소 확인
$ docker container ls --format 'table \{\{.Image}}\t\{\{.Command}}' | grep -v pause
```

#### kind, kubernetes in docker
- k8s 자체 개발을 위한 도구
- k8s의 SIG-Testing에서 제작
- 도커 컨테이너 여러 개를 기동하고 그 컨테이너를 쿠버네티스 노드로 사용하는 것 => 쿠버네티스 클러스터 구축
- 로컬 환경에서 멀티 노드 클러스터를 구축하려면 kind를 이용하는 것이 가장 효과적(Why?)


