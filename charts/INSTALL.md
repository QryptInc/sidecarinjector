# Step by Step Instructions to Install and try the examples

## Assumptions
- a Kubernetes cluster is available and KUBECONFIG is correct configured
- kubectl cli is installed
- Helm v3 is installed

## Steps

### Create a namespace for cert-manager

- Create cert-manager namespace

```
kubectl create ns cert-manager
```

- Label the cert-manager namespace so that injection is disabled

```
kubectl label ns cert-manager sidecar-injection=disabled
```

### Mark if Cert-Manager should be installed

Note it is [recommended](https://cert-manager.io/docs/contributing/policy/#helm-subchart-capabilities) to only have 1 cert-manager per cluster.
- Set cert-manager enabled value to false if it should not be installed

### Install Generic Sidecar Injector

- Install Generic Sidecar injector using Helm

```
helm dependency update helm/sidecarinjector/
helm install sidecarinjector helm/sidecarinjector/ --namespace sidecarinjector
kubectl get pods -n sidecarinjector
```

- Note that there must be a few secrets in the target namespace.
  - secret qrypt-token must contain the token to get random from Qrypt BLAST servers under the key token.

- TLS enabled secure tunnel
Use the values_tls.yaml instead of the values.yaml. The yaml is set up to contain the cert and key in plain-text. It should be a small update to use secrets instead.
  - Secrets to fill in
    - secret tls-cert must contain the tls cert in pem format under the key tls_cert.
    - secret tls-key must contain the tls private key in pem format under the key tls_key.

- mTLS enabled secure tunnel
Use the values_mtls.yaml instead of the values.yaml. The yaml is set up to contain the cert and key in plain-text. It should be a small update to use secrets instead.
  - Secrets to fill in
    - secret tls-cert must contain the tls cert in pem format under the key tls_cert.
    - secret tls-key must contain the tls private key in pem format under the key tls_key.
    - secret client-cert must contain the client cert in pem format under the key client_cert.

### Verify sidecar injector functionality

- Try some examples

```
cd helm/examples
kubectl create ns demo
kubectl create secret generic qrypt-token --from-literal=token=FILL_IN -n demo
kubectl apply -f pod.yaml
kubectl get pods
```

- verify the pod has a new container injected called envoy

```
 kubectl get po -o jsonpath='{range .items[*]}{"pod: "}{.metadata.name}{"\n"}{range .spec.containers[*]}{"\tname: "}{.name}{"\n"}{end}'
```

### Cleanup
- delete the busybox pod

```
kubectl delete -f pod.yaml
```

- delete the helm release for sidecar

```
helm delete sidecarinjector
```

- delete the namespaces

```
kubectl delete ns demo
kubectl delete ns sidecarinjector
```
