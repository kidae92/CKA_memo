- 노드가 5분 동안 오프라인이 되면 마스터 노드는 노드를 죽은 것으로 간주
- replicaset이 설정되어 있는 pod은 다른 곳에 복제본을 만들지만, 그렇지 않은 pod 그냥 사라짐
- 워크로드가 다른 노드로 이동되도록 모든 워크로드의 노드를 의도적으로 drain할 수 있음
```
kubectl drain node-1
kubectl unrcordon node-1
kubectl cordon node-2
```
- cordon: 지정된 노드에 더이상 포드들이 스케쥴링되서 실행되지 않도록 함(기존 Pod은 유지됨)
- drain: 노드 관리를 위해서 지정된 노드에 있는 포드들을 다른 곳으로 이동시키는 명령
- 이때 노드에 데몬셋으로 실행된 포드들이 있으면  drain이 실패함(--ignore-daemonsets=true 옵션을 주면 가능)