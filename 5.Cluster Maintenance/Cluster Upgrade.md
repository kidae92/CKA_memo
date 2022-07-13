- Kube API 서버가 기본 구성 요소이기 때문에 다른 구성 요소는 다른 릴리스 버전에 있을 수 있음
- 다른 구성 요소가 Kube API버전 높은 버전이면 안됨
- kube-apiserver X
- Controller-manager, kube-scheduler X-1
- kubelet, kube-proxy X-2
- kubectl X+1 ~ X-1

- 마스터가 잠시 다운된다고 해서 워커 노드의 애플리케이션이 영향을 받진 않음
- 워커 노드를 한번에 업데이트하면 서비스 사용 불가
- 하나씩 하되 워크로드가 다른 노드로 이용
```
 kubeadm upgrage plan
 apt-get upgrade -y kubeadm=1.12.0-00
 kubeadm upgrage apply v1.12.0
 -------
 # Master
 apt-get upgrade -y kubelet=1.12.0-00
 systemctl restart kubelet
 kubectl get nodes(master는 버전 업그레이드 반영됨)
 # Worker
 kubectl drain node-01
 apt-get upgrade -y kubeadm=1.12.0-00
 apt-get upgrade -y kubelet=1.12.0-00
 kubeadm upgrade node config --kubelet-version v1.12.0
 systemctl restart kubelet
 kubectl uncordon node-01
 
```
- 공식문서 잘 따라하면 된다!