```
# 다른 namespace의 service를 부를 때
http://web-server.app(namespace)
web-service.apps.svc.cluster.local 정규화된 도메인 이름
10.244.2.5라는 ip를 가진 pod은 hostname이 10-244-1-5 대시로 이어진 이름으로 저장됨

노드와 pod이 많아지면 /etc/hosts에 하나하나 지정해주는 건 옳지않다
/etc/resolv.conf의 nameserver를 coreDNS ip를 지정해준다
resolv.conf 파일을 coredns가 proxy로서 활용함
```