

---

## Kubernetes Cheat Sheet


#### namespace 예시
$ kubectl create deploy ui --image=nginx --namespcae=blue
$ kubectl create deploy ui --image=nginx --namespace=orange
$ kubectl create deploy ui --image=nginx --namespace=green

#### namespace 사용하기
1) CLI
$ kubectl create namespace blue
$ kubectl get namespace
2) YAML
$ kubectl create namespace green --dry-run -o yaml > green-ns.yaml
$ vim green-ns.yaml
$ kubectl create -f green-ns.yaml

#### namespace 관리하기
$ kubectl get namespace
$ kubectl delete namespace
