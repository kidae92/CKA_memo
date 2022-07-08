- kube-api가 없이 kubelet에 pod 형성
- 서버의 디렉토리에서 yaml 파일을 읽도록 kubelet 구성 가능
- 일반적으로 /etc/kubernetes/manifest
- static pod은 해당 노드에서 docker ps 로 확인 가능
- 또한 API server는 kubelet에 의해 생성된 static pod를 인식함
- 클러스터의 일부인 경우 kube api server에 mirror object를 생성(read-only, 삭제불가)
DaemonSets vs Static PODs
- DaemonSets: created by Kube-API server(DaemonSet Controller), Deploy Monitoring Agents, Logging Agents on nodes
- Static PODs: Created by Kubelet, Deploy Control Plane components as Static Pods
공통점은 Ignored nby the Kube-Scheduler