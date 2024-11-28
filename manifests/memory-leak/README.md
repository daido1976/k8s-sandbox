わざとメモリリークを起こさせて、`resources.limit` で pod の再起動が起こることを確認する。

```sh
# manifestをapplyする
$ kubectl --context=minikube apply -f ./manifests/memory-leak

# 以下でログを見る
$ kubectl logs -f deployment/php-memory-leak-test
# [2024-11-28 15:08:41] Memory usage: 4392648 bytes (4.19 MB)
# [2024-11-28 15:08:51] Memory usage: 8395448 bytes (8.01 MB)
# [2024-11-28 15:09:01] Memory usage: 12397264 bytes (11.82 MB)
# ...

# pod起動中なら以下でpodのメモリ使用量が見れる
$ kubectl top pods
```
