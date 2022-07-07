
```
kubectl describe node controlplane | grep -i taints
kubectl describe node node01 | grep -i taints
```

- node selector
```
# node에 라벨 지정
kubectl label nodes <node-name> <label-key>=<label-value>
kubectl label nodes node-1 size=Large *****************
```


```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app: nginx
    tier: frontend
spec:
  containers:
  -  name: nginx
     image: nginx
  nodeSelector:
    size: Large *************

```

- node affinity
  - Taint가 Pod가 배포되지 못하도록 하는 정책이라면, affinity는 Pod를 특정 Node에 배포되도록 하는 정책
  - affinity는 Node를 기준으로 하는 Node affinity와, 다른 Pod가 배포된 위치(node)를 기준으로 하는 Pod affinity 두 가지가 있다.
- type
  - requiredDuringSchedulingIgnoredDuringExectution 
  - preferredDuringSchedulingIgnoredDuringExecution

```
apiVersion: v1
kind: Pod
metadata:
  name: with-node-affinity
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: kubernetes.io/os
            operator: In
            values:
            - linux
      preferredDuringSchedulingIgnoredDuringExecution:
      - weight: 1
        preference:
          matchExpressions:
          - key: another-node-label-key
            operator: In
            values:
            - another-node-label-value
  containers:
  - name: with-node-affinity
    image: k8s.gcr.io/pause:2.0
```

- requiredDuringSchedulingIgnoredDuringExecution는 Hard affinity 정의
- 위의 예제는 node에 label key “kubernetes.io/e2e-az-name” 의 값이 eze-az1 이나 eze-az2 인 node를 선택하도록 하는 설정
- preferredDuringSchedulingIgnoredDuringExecution는 Soft affinity 정의
- Soft affinity는 조건에 맞는 node로 되도록이면 배포될 수 있도록 node로 배포 선호도를 주는 기능. weight 1 ~ 100, node의 soft affinity의 weight 값들을 합쳐서 그 값이 높은 node를 우선으로 고려하도록 우선 순위를 주는데 사용 가능
- IgnoreDuringExecution는 pod이 동작 하는 도중에 label을 변경해도 무시한다
- RequiredDuringExecution는 label과 같은 변경사항이 있을 경우 실행중이 pod을 모두 없앤다(선호도 규칙 x)



- --dry-run=client -o yaml > ooo.yaml 활용을 기본적으로 하는 것이 편하다
- 그리고 쿠버네티스 공식 홈페이지 활용도 잘해야한다.