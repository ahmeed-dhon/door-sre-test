# Helm Chart: nodejs-service

A Helm chart for nodejs-service.

## Usage

1. Install [Helm](https://helm.sh/).
```sh
$ brew install helm
```

2. Go to `k8s-manifests` directory.
```sh
$ cd k8s-manifests
```

3. Deploy `nodejs-service`.
```sh
$ helm install nodejs-service ./nodejs-service --namespace PROD --set image.tag=latest
```

4. Upgrade `nodejs-service`.
```sh
$ helm upgrade nodejs-service ./nodejs-service --namespace PROD --set image.tag=v0.10.7
```

5. Check release history of `nodejs-service`.
```sh
$ helm history nodejs-service --namespace PROD
```

6. Rollback `nodejs-service`.
```sh
$ helm rollback nodejs-service [REVISION] --namespace PROD
```

7. Uninstall `nodejs-service`.
```sh
$ helm uninstall nodejs-service --namespace PROD
```