### Create Secret

```
kubectl create secret generic db-connection-secret \
--from-literal=username=service \
--from-literal=password=P@ssw0rd \
--from-literal=host=db-server-staging \
--from-literal=database=breyzweather
```
or

```
apiVersion: v1
kind: Secret
metadata:
  name: db-connection-secret
type: Opaque
data:
  username: c2VydmljZQ== # service
  password: UEBzc3cwcmQ= # P@ssw0rd
  host: ZGItc2VydmVyLXN0YWdpbmc= # db-server-staging
  database: YnJlenl3ZWF0aGVy # brezyweather
```


```
apiVersion: v1
kind: Secret
metadata:
  name: api-keys-secret
  namespace: staging
type: Opaque
data:
  openweather-key: c3RhZ2luZy1rZXktZm9yLXRlc3Rpbmc= # staging-key-for-testing
```

### Create Pod in staging namespace

```echo -n 'staging-key-for-testing' | base64 ```


```
kubectl create namespace staging
```

```
apiVersion: v1
kind: Pod
metadata:
  name: brezyweather-pod
spec:
  containers:
  - image: codewithpraveen/labs-k8s-brezyweather:1.0
    name: brezyweather-pod
    ports:
    - containerPort: 80
    resources:
      limits:
        cpu: 100m
        memory: 128Mi
    env:
    - name: openweather-key
      valueFrom:
        secretKeyRef:
          name: api-keys-secret
          key: openweather-key
    volumeMounts:
    - name: db-connection-volume
      mountPath: /etc/config
  volumes:
  - name: db-connection-volume
    secret:
      secretName: db-connection-secret

```
