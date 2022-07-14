1. Create CertificateSigningRequest Object
2. Review Requests
3. Approve Requests
4. Share Certs to Users


- 사용자는 먼저 키를 만든 다음 자신의 이름이 있는 키를 사용하여 인증서 서명 요청 생성
- 관리자에게 요청 보냄
- 관리자는 키를 가져와 인증서 서명 요청 object를 생성
- 인증서 서명 요청 object는 manifest를 사용하여 다른 kubernetes 객체처럼 생성됨
- yaml파일 확인해보면 kind가 CertificateSigningRequest
- request 필드에는 사용자의 csr 파일을 base64로 인코딩한 내용을 적어야함
```
kubectl get csr
kubectl certificate approve jane
kubectl get scr jane -o yaml
echo "~~~~" | base64 --decode
```
- Controller Manager에 CSR-APPROVING, CSR_SIGNING을 수행하는 것이 있음
```
cat /etc/kubernetes/manifests/kube-controller-manager.yaml
--cluster-signing-cert-file=/etc/kubernetes/pki/ca.crt
--cluster-signing-key-file=/etc/kubernetes/pki/ca.key
```