Drain と PDB の動作確認用。

TODO: PDB の object 作って動作確認もする。

```sh
# drain動作確認のために複数ノード立ち上げる
$ minikube start --nodes 2
# もしくは起動済みの場合は以下を実行
$ minikube node add

# manifestをapplyする
$ kubectl --context=minikube apply -f ./manifests/drain-pdb

# drainを実行する
$ kubectl drain minikube --ignore-daemonsets --force

# drain後のノードを再びスケジュール可能にする
$ kubectl uncordon minikube
```
