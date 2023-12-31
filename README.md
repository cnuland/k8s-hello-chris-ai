# azure-bus-python
## Provsion
1) Need OLM operator installed first
2) Generate needed secrets from the /ignored folder (Azure account)
3) Deploy Cluster-Primer
```
kubectl apply -k cluster-primer
```
## Service Bus
Secret Needed
Either create it manually as shown below
```
az servicebus queue authorization-rule create --resource-group <name> --namespace-name <name> --queue-name <nme> --name <name> --rights Listen
```
```
az servicebus queue authorization-rule keys list --resource-group <resource-group-name> --namespace-name <namespace-name> --queue-name orders --name order-consumer
```

```
oc create secret generic namespace-secret --from-literal=connection="Endpoint=sb://<endpoint>;SharedAccessKeyName=<sa-name>;SharedAccessKey=<primary-key>"
```

## Vault
If using an external secret operator you will need the initial service principal to access the Azure key vault.

```
az ad sp create-for-rbac --name myKeyVaultServicePrincipal --role reader --scopes /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>
```

## Tekton & Kaniko
Docker Secret for Kaniko
```
cat ~/.docker/config.json | base64
```
```
apiVersion: v1
kind: Secret
metadata:
  name: docker-credentials
  namespace: hello-chris
data:
  config.json: ewoJImF1d....
```

## useful commands
```
argocd app sync hello-chris
```
```
argocd app terminate-op hello-chris
```

```
kubectl debug clone-build-push-build-push-pod -n hello-chris --image=busybox:1.28 -i --target=step-build-and-push
```

```
kubectl annotate externalsecret foobar rotate=$(date +%s)
```