- 처음에 deployment가 생성되면 Rollout이 트리거됨
```
kubectl rollout status deployment/ㅇㅇㅇ
kubectl rollout history deployment/ㅇㅇㅇ

kubectl apply -f deployment-definition.yml 로 새로운 Rollout이 트리거
kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1

recreate는 pod의 숫자가 0까지 가기 때문에 서비스 끊김
Rolling Update는 replicaet이 하나씩 줄어들고 생김

# RollBack
kubectl rollout undo deployment/myapp-deployment
```