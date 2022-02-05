# flyte-spark-op

### charts installation:
```bash
cd charts/flyte
helm dependency update
helm install -f values.yaml --create-namespace flyte .
```

### charts uninstall:
```bash
helm uninstall flyte
kubectl patch crd/flyteworkflows.flyte.lyft.com -p '{"metadata":{"finalizers":[]}}' --type=merge
```
### flyte install
```bash
curl -s https://raw.githubusercontent.com/flyteorg/flytectl/master/install.sh | bash
pip install flytekit
```

### flyte workflows/tasks build:

```bash
cd kubernetes
docker build . --tag rodrigobaron/flyte:0.0.1 -f k8s_spark/Dockerfile
docker push rodrigobaron/flyte:0.0.1

pyflyte --pkgs k8s_spark package --image rodrigobaron/flyte:0.0.1
flytectl register files --project flytesnacks --domain development --archive flyte-package.tgz --version v1
```
