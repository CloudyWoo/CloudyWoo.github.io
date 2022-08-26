---
layout: single

title:  "쿠버네티스 대시보드 사용법"
excerpt: "kube proxy 또는 Nodeport로 로컬에서 대시보드를 사용해보자."

categories:
    - Kubernetes
tags: [DevOps, Kubernetes]

toc: true
author_profile: false
sidebar:
    nav: "docs"

date: 2022-08-24
last_modified_at: 2022-08-24
---

### 1. 대시보드 UI 배포
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.6.0/aio/deploy/recommended.yaml

### 2. 대시보드 UI 접근
##### 1) Proxy로 서비스하는 경우
kubectl proxy
curl http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

##### 2) NodePort로 서비스하는 경우
kubectl -n kubernetes-dashboard get svc
kubectl -n kubernetes-dashboard edit service kubernetes-dashboard

``` yaml
apiVersion: v1
kind: Service
metadata:
  ...
spec:
  clusterIP: 10.106.207.236
  clusterIPs:
  - 10.106.207.236
  internalTrafficPolicy: Cluster
  ipFamilies:
  - IPv4
  ipFamilyPolicy: SingleStack
  ports:
  - port: 443
    protocol: TCP
    targetPort: 8443
  selector:
    k8s-app: kubernetes-dashboard
  sessionAffinity: None
  type: ClusterIP # 이곳을 NodePort로 변경하자
status:
  loadBalancer: {}
```
kubectl -n kubernetes-dashboard get service kubernetes-dashboard # 노드 포트 확인
https://localhost:<확인된포트>


### 3. 
##### 1) ServiceAccount
``` yaml
// sudo vim service-account.yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kubernetes-dashboard
```

##### 2) ClusterRoleBinding
``` yaml
// cluster-role-binding.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
  - kind: ServiceAccount
    name: admin-user
    namespace: kubernetes-dashboard
```

### 대시보드 토큰 발행
kubectl -n kubernetes-dashboard create token admin-user


### 대시보드 토큰 제한 시간 변경
kubectl edit -n kubernetes-dashboard deployments.apps kubernetes-dashboard

``` yaml
# ... content before...

    spec:
      containers:
      - args:
        - --auto-generate-certificates
        - --namespace=kubernetes-dashboard
        - --token-ttl=0 # <-- 이걸 추가
      image: kubernetesui/dashboard:v2.6.0

# ... content after ..
```


