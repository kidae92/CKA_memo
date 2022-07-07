- 쿠버네티스 클러스터의 특정 노드에 taint를 지정할 수 있다. taint를 설정한 노드에는 pod들이 스케쥴링 되지 않는다
- taint가 걸린 노드에 포드들을 스케쥴링 하려면 toleration을 이용해서 지정해 줘야한다.
- 주로 노드를 지정된 역할만 하게할 때 사용. DB용 pod을 띄워서 전체의 CPU나 RAM자원을 독점해서 사용하게 할 수 있음.
- 


```
#node1에 taint 지정
kubectl taint nodes node1 app=blue:NoSchedule
#확인
kubectl describe node node1 | grep Taint
```

```
#toleration을 이용하여 taint가 걸린 노드 접근 가능
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  containers:
  - name: nginx-container
    image: nginx
    
  tolerations:
  - key: "app"
    operator: "Equal"
    value: "blue"
    effect: "NoSchedule"
```