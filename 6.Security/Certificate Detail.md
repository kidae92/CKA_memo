```
kubectl create serviceaccount test
```

- Auth Mechanisms
    - Static Password File: CSV파일내에 정보 돈재, 패스워드, 사용자이름. 사용자ID가 있다
      (--basic-auth-file=user-details.csv), kube-apiserver.yaml을 수정해야함. command에 csv파일 경로를 적어줘야함
    - Static Token File: 암호 대신 토큰을 지정(--token-auth-file=user-details.csv)
    - Certificates
    - Identity Services

- 보안을 위해서 암호화 형식의 데이터와 이를 해독할 수 있는 key가 필요
- 하지만 발신자와 수신자 사이에 해커가 키에 접근하여 암호를 해독할 수 있음
- Asymmetric Encryption(비대칭 암호화): Private Key, Public Key
- Public Key: *.crt, *.pem, Private Key: *.key, *-key.pem

```
openssl genrsa -out ca.key 2048

openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout
```