```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: google-storage
provisioner: kubernetes.io/gce-pd
```

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: myclaim
spce:
  accessModes:
    - ReadWriteOnce
  storageClassName: google-storage
  resources:
    requests:
      storage: 500Mi
```

- 연결된 스토리지 클래스는 정의된 프로비저닝을 사용하여 필요한 GCP에서 크기를 지정한 다음 persistent volume을 만들고 PVC를 해당 volume에 바인딩
- 수동으로 PV를 만드는 것이 아닌 storage class에 의해 자동으로 생성