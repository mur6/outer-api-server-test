# outer-api-server-test
画面右上自分の写真 > settings > Developer settings > Personal access tokens
から、read:packages, repo, write:packages という権限を選んでトークンを発行する。


```
$ cat ~/zozo_github_pkg.txt | docker login docker.pkg.github.com -u USERNAME --password-stdin
Login Succeeded
```
でgithubのdocker registryにログインしておく。

```
$ docker pull docker.pkg.github.com/mur6/internal-api-server-test/simpleapi:v0.1.1
```
でpullしておく。

```
$ skaffold run --port-forward
Generating tags...
Checking cache...
Tags used in deployment:
Starting deploy...
 - service/service created
 - deployment.apps/deployment created
Waiting for deployments to stabilize...
 - deployment/deployment: waiting for rollout to finish: 0 of 1 updated replicas are available...
 - deployment/deployment is ready.
Deployments stabilized in 1.881413879s
Press Ctrl+C to exit
Port forwarding service/service in namespace default, remote port 5000 -> address 127.0.0.1 port 5000
```
で起動。

```
$ skaffold delete
Cleaning up...
 - service "service" deleted
 - deployment.apps "deployment" deleted
```
で停止。
