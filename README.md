# iac-flux-keycloak
Flux configuration for Keycloak

## Developer Guide
To test the changes, ensure that you are on your developer machine and that the context is set correctly to your local instance please amend the following script to use the target branch:

```bash
kubectl config use-context docker-desktop
kubectl create namespace keycloak
flux create source git keycloak --url="https://github.com/lsc-sde/iac-flux-keycloak" --branch=main --namespace=keycloak
flux create kustomization keycloak-sources --source="GitRepository/keycloak" --namespace=keycloak --path="./sources" --interval=1m --prune=true --health-check-timeout=10m --wait=false
flux create kustomization keycloak-cluster-config --source="GitRepository/keycloak" --namespace=keycloak --path="./cluster/local" --interval=1m --prune=true --health-check-timeout=10m --wait=false
```

This should in turn deploy all of the resulting resources on your local cluster.

This should in turn deploy all of the resulting resources on your local cluster. Once done you'll need to download the CA certificate for this so that you can install it onto your local machine:

```bash
kubectl get secrets/keycloak.lsc-sde.local-tls -n keycloak -o=jsonpath="{.data.ca\.crt}" | base64 --decode > ca.crt
```

this will create a ca.crt file in the directory, you will then need to install it into your trusted root authorities.

You will also need to adjust your machines hosts file to include the line:

```
127.0.0.1 keycloak.lsc-sde.local
```