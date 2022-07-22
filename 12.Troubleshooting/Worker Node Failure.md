```
kubectl get node 후 문제되는 노드 로그 확인

- CPU, Memory, Disk 등등확인
- kubelet 확인 (service kubelet status, sudo journalctl -u kubelet)
- 인증서 확인 (poenssl x509 -in /var/lib/kubelet/worker-1.crt -text)
- kubelet config 파일 (var/lib/kubelet)
```