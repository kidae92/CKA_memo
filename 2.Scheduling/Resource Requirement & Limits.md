- 노드에 CPU, Memory, storage와 같은 resource가 부족하면 pending 상태가 됨.
- describe 명령어를 활용하여 확인가능
- 따로 리소스 제한을 설정 안하면 0.5 CPU, 512 Mi

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
  resources:
    requests:
      memory: "1Gi"
      cpu: 1
    limits:
      memory: "2Gi"
      cpu: 2

```
- CPU의 경우 지정된 제한을 초과하지 않도록 조절함
- 메모리의 경우 제한보다 많은 리소스를 사용할 수 있음. 그러나 지속적으로 제한보다 많은 메모리를 사용하려고 하면 pod이 종료가 됨


- 기본 default 리소스 할당 조정 가능
```
apiVersion: v1
kind: LimitRange
metadata:
  name: mem-limit-range
spec:
  limits:
  - default:
      memory: 512Mi
    defaultRequest:
      memory: 256Mi
    type: Container
```


```
apiVersion: v1
kind: LimitRange
metadata:
  name: cpu-limit-range
spec:
  limits:
  - default:
      cpu: 1
    defaultRequest:
      cpu: 0.5
    type: Container
```