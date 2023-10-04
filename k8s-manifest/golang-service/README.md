# Helm Chart: golang-service

A Helm chart for golang-service.

## Usage

1. Install [Helm](https://helm.sh/).
```sh
$ brew install helm
```

2. Go to `k8s-manifests` directory.
```sh
$ cd k8s-manifests
```

3. Deploy `golang-service`.
```sh
$ helm install golang-service ./golang-service --namespace PROD --set image.tag=latest
```

4. Upgrade `golang-service`.
```sh
$ helm upgrade golang-service ./golang-service --namespace PROD --set image.tag=v0.10.7
```

5. Check release history of `golang-service`.
```sh
$ helm history golang-service --namespace PROD
```

6. Rollback `golang-service`.
```sh
$ helm rollback golang-service [REVISION] --namespace PROD
```

7. Uninstall `golang-service`.
```sh
$ helm uninstall golang-service --namespace PROD
```