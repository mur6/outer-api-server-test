# outer-api-server-test
github のページ右上の自分の写真から、
 > settings > Developer settings > Personal access tokens

を選択した上で、`read:packages, repo, write:packages` という権限を付加したアクセストークンを発行する。

```
$ kubectl create secret docker-registry regcred --docker-server=https://docker.pkg.github.com --docker-username=<アカウント名> --docker-password=<アクセストークン>
```

Dockerレジストリに対する認証のため、githubのアカウント名と発行したアクセストークンを上記のコマンドで kubernetes Secretに登録する。

```
$ skaffold run
Generating tags...
Checking cache...
Tags used in deployment:
Starting deploy...
 - service/service created
 - deployment.apps/deployment created
Waiting for deployments to stabilize...
 - deployment/deployment: waiting for rollout to finish: 0 of 1 updated replicas are available...
 - deployment/deployment is ready.
Deployments stabilized in 2.357680821s
You can also run [skaffold run --tail] to get the logs
```
で internal-api-server-test のマニフェストとコンテナをインポートした形で、サービスを起動できる。

```
$ skaffold delete
Cleaning up...
 - service "service" deleted
 - deployment.apps "deployment" deleted
```
にて停止できる。
