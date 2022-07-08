- Daemonset은 replicaset이랑 비슷하지만 클러스터의 각 노드에 하나의 복사본
- 클러스터가 추가될 때마다 해당 노드에 자동으로 추가됨
- 모니터링 에이전트 또는 로그 수집기를 각 노드에 배포하려 한다면 Daemonset은 pod 형태로 완벽함
- kube-proxy, network(wav)
```
apiVersion: apps/v1   
kind: DaemonSet (리플리카셋이랑 여기만 다름)

metadata:
  name: myapp-replicaset
  labels:
    app: myapp
    type: front-end

spec:
  template:
    metadata:
      name: nginx
      labels:
        app: nginx
        tier: frontend
    spec:
      containers:
      -  name: nginx
         image: nginx

```