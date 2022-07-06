- 이름공간 또는 네임스페이스(영어: namespace)는 개체를 구분할 수 있는 범위

- 다른 namespace에 있는 db에 접근하고자 하면 아래와 같이 해야한다.
servicename.namespace.svc.cluster.local

- 주요 명령어
```
## yaml 파일로 오브젝트를 생성할 때 namespace를 지정해줄 수 있다. 안하면 default namespace에 생성
kubectl create –f ...yml —namespace=dev
## default namespace를 dev namespace로 바꾼다.
kubectl config set-context $(kubectl config current-context) --namespace=dev
```

```

apiVersion: v1
kind: Pod
metadata:
  name: nginx
  namespace: dev (이런식으로도 가능)
  labels:
    app: nginx
    tier: frontend
spec:
  containers:
  -  name: nginx
     image: nginx
```

- ResouceQuata (namespace resource allocation)
- namespce별 총 리소스 사요을 제안하는 제약 조건을 제공
```
apiVersion: v1
kind: ResouceQuata
metadata:
  name: compute-quata
  namespace: dev
spec:
  hard:
    pod: “10”
    requests.cpu: “4”
    requests.memory: 5Gi
    limits.cpu: “10”
    limits.memory: 10Gi
```