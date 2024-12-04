ローリングアップデートの動作確認。

```sh
# manifestをapplyする
$ kubectl --context=minikube apply -f ./manifests/rolling-update

# ローリングアップデートの動作を視覚的に確認できるようにwatchモードで流しておく（dashboardからの方が見やすいかも）
$ kubectl get pods -w

# イメージを更新してローリングアップデートを実行（nginx:xxのxxのところを変えたら何度でも確認できる）
$ kubectl set image deployment/rolling-update-test nginx=nginx:1.21

# ローリングアップデートの進行状況を確認
$ kubectl rollout status deployment/rolling-update-test
```
