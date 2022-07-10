```
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu-sleeper-pod
spec:
  containers:
  -  name: ubuntu-sleeper
     image: ubuntu-sleeper
     command: ["sleep2.0]
     args: ["10"]

# docker file에 정의된 entrypoint(command) cmd(args)가 overrideing 됨
```