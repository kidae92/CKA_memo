- cAdvisor / Container Advisor: Pod에서 성능 메트릭을 검색하고 kubelet API를 통해 노출
- Metrics Server에서 소스 다운 받고 사용 가능
```
git clone https://github.com/kodekloudhub/kubernetes-metrics-server.git
cd kubernetes-metrics-server
kubectl apply -f . (전부 실행)
# 각 오브젝트의 CPU(cores) / CPU% / MEMORY(bytes) / MEMORY% 를 확인 할 수 있음
kubectl top node
kubectl top pod

```