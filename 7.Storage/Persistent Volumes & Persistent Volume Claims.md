- Docker Storage Driver & File System
- volume mount는 볼륨 디렉토리에서 볼륨을 마운트하고
- bind mount는 임의의 위치에서 디렉토리를 마운트
```
docker run \
--mount type=bind,source=/data/mysql,target=/var/lib/mysql mysql
```
```
docker run -it \
    --name mysql
    --volume-driver rexray/ebs
    --mount src=ebs-vol, target=/var/lib/mysql
    mysql
```

```
spec:
  containers:
  
  volumes:
  - name: data-volume
    hostPath:
      path: /data
      type: Directory
      
      
  volumes:
  - name: data-volume
    awdElasticBlockStore:
      volumeID: <volume-id>
      fsType: ext.4
```

```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-voli
spce:
  accessModes:
     - ReadWriteOnce
  capacity:
    storage: 1Gi
  hostPath:
    path: /tmp/data
  
```
- PVC가 생성되면 kubernetes는 PV를 PVC에 바인딩 1:1
```
#PV
labels:
  name: my-pv
  
#PVC
selector:
  mathLabels:
    name: my-pv
```
- PV가 없는 경우 PVC는 pending 됨
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: myclaim
spce:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 500Mi
```
- PV가 PVC보다 커도 다른 PVC가 볼륨을 사용할 수 없음. 1:1이기 때문
- persistentVolumeReclaimPolicy 설정으로 다양한 옵션 가능
```
# pod 생성하면서 PVC 할때
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
    - name: myfrontend
      image: nginx
      volumeMounts:
      - mountPath: "/var/www/html"
        name: mypd
  volumes:
    - name: mypd
      persistentVolumeClaim:
        claimName: myclaim
```

- (PV가 꼭 노드 안에 있지 않고 외장 스토리지를 사용하는 경우도 많음)   PVC를 통하여 PV가 생성되며 PVC는 Storage Class에서 할당할 수 있음