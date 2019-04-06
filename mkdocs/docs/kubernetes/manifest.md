KubernetesはInfrastructure as Code でのアプローチを公式でサポートしています。  
Objectsのコードはyamlで表現することが可能です。また、このコードのことをManifestと呼びます。

## nginxの起動
例のごとく"handson-4"という名前で"nginx"を起動することを例にします。  

今までは以下のように `kubectl run` を使ってコンテナをデプロイしてきました。
```console
$ kubectl run handson-4 --image=nginx --port=80
```

コードで定義すると上記のコマンドは以下のようなyamlになります。
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    run: handson-4
  name: handson-4
spec:
  selector:
    matchLabels:
      run: handson-4
  template:
    metadata:
      labels:
        run: handson-4
    spec:
      containers:
      - image: nginx
        name: handson-4
        ports:
        - containerPort: 80
```

まずは実際に上記のコードが実際に動作するか見てみましょう
```console
$ vi manifest.yaml
```

作成したコードは `kubectl apply -f <ファイル名>` で適用できます。  
早速実行してみましょう。
```console
$ kubectl apply -f manifest.yaml
deployment.apps/handson-4 created
$ kubectl get all -l run=handson-4
NAME                            READY   STATUS    RESTARTS   AGE
pod/handson-4-696c5c849-wlhdk   1/1     Running   0          9s

NAME                        DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/handson-4   1         1         1            1           9s

NAME                                  DESIRED   CURRENT   READY   AGE
replicaset.apps/handson-4-696c5c849   1         1         1       9s
```

## LoadBalancerの起動
コンテナのデプロイと同じくロードバランサもmanifestで定義可能です。
以下のコードを先程のファイルへ追記してみましょう。

```
$ vi manifest.yaml
```

```yaml
---
apiVersion: v1
kind: Service
metadata:
  labels:
    run: handson
  name: handson
spec:
  ports:
  - port: 80
    targetPort: 80
  selector:
    run: handson
  type: LoadBalancer
```

ロードバランサがセットアップされたか確認してみましょう。
```console
$ kubectl apply -f manifest.yaml
deployment.apps/handson-4 configured
service/handson-4 created
$ kubectl get all
NAME                            READY   STATUS    RESTARTS   AGE
pod/handson-4-696c5c849-wlhdk   1/1     Running   0          1h

NAME                TYPE           CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
service/handson-4   LoadBalancer   10.3.250.83   <pending>     80:32533/TCP   27s

NAME                        DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/handson-4   1         1         1            1           1h

NAME                                  DESIRED   CURRENT   READY   AGE
replicaset.apps/handson-4-696c5c849   1         1         1       1h
```

## お片付け
コマンドから起動した "handson" と命名したObjectsの削除。
```console
$ kubectl delete service handson
service "handson" deleted
$ kubectl delete deployment handson
deployment.extensions "handson" deleted
```

コードから定義した "handson-4" 命名したObjectsの削除。  
```
$ kubectl delete -f manifest.yaml
deployment.apps "handson-4" deleted
service "handson-4" deleted
```
