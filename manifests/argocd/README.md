Argo CD を minikube にデプロイしてみる。

```sh
# argocd用のnamespace作成
$ kubectl create namespace argocd
# argocdのインストール
$ kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
# ポートフォワードしてargocdにブラウザからアクセスできるようにする
$ kubectl port-forward svc/argocd-server -n argocd 8080:443
# 以下でパスワードを取得しつつ `Username: admin/Password: {取得したパスワード}` でログインする
$ kubectl -n argocd get secret argocd-initial-admcret -o jsonpath="{.data.password}" | base64 -d; echo
```

Argo CD CLI を使う場合は以下。

```sh
$ brew install argocd
# ポードフォワードした状態で以下を実行してログイン
$ argocd login localhost:8080 --username admin --password $(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d) --insecure
# argocdのアプリケーションの作成（Web UIからでも `New App` のところから設定可能）
$ argocd app create argocd-sample-app --repo https://github.com/daido1976/k8s-sandbox --path manifests/argocd --dest-server https://kubernetes.default.svc --dest-namespace default
```

## 参考

- https://argo-cd.readthedocs.io/en/stable/getting_started/
- https://medium.com/@mehmetodabashi/installing-argocd-on-minikube-and-deploying-a-test-application-caa68ec55fbf
