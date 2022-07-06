- 복제셋으로 생각하면 되고, Controller가 지정된 팟의 갯수의 복제셋을 끊임 없이 관찰하고 유지한다.
- replicaset은 label을 보고 그 수를 판단하기 때문에 label이 겹치거나 임의로 변경하면 안된다. 
- replicaset 갯수를 변경할 때 명령어
```
## yaml 파일로 직접 교체
kubectl replace -f ....yml

## yaml 파일에 replicas에 대한 정보 없이 scale 명령어로 주기
kubectl scale --replicas=6 –f ...

## object의 이름을 지정하고 직접 변경
kubectl scale --replicas=6 replicaset(type) myapp-replicaset(name)
```

- ex) replicaset
```

apiVersion: apps/v1   (이거 주의해야함)
kind: ReplicaSet

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
replicas: 3
selector:
  matchLabels:
    type: front-end 
```

---------------------------------------------------------------------------
- Replicaset은 Deployment로 감싸서 배포함

- 주로 쓰이는 명령어
```
kubectl create deployment --image=nginx nginx
kubectl scale deployment nginx —replicas=5
kubectl expose deployment nginx —port 80
```

## 시험 팁 명령어
```
kubectl apply –f nginx.yaml (create & update 동일)
kubectl run —image=nginx nginx
kubectl create deployment —image=nginx nginx
kubectl expose deployment nginx —port 80
kubectl edit deployment nginx
kubectl scale deployment nginx —replicas=5
kubectl set image deployment nginx nginx=nginx:1.18

kubectl run nginx --image=nginx --dry-run=client –o yaml
kubectl create deployment --image=nginx nginx --dry-run=client –o yaml
kubectl create deployment nginx --image=nginx --dry-run=client -o yaml > nginx-deployment.yaml

특히 --dry-run=client를 옵션으로 주면 실제로 형성되지는 않고 가능한지 불가능한지만 판단
뒤에 -o yaml을 하면 커맨드라인에 작성한 명령어가 yaml 파일 형식으로 출력 해줌
> ooo.yaml을 붙이면, yaml 파일 형식으로 출력됬던 정보가 실제 yaml파일로 만들어진다.
```
