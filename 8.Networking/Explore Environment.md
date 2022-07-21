- arp: 주소 결정 프로토콜
![img_11.png](images/img_11.png)
```
arp node01
```

![img_12.png](images/img_12.png)
```
ip route show default
```

![img_13.png](images/img_13.png)
```
netstat -anp | grep etcd | grep <port> | wc -l
```