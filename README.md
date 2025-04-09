# ai-observability
A repository to observe AI usage and costs in OSP

# k8s

## PG

```
k apply -f ./pg.yml
```

Get secret:
```
PASS=`k -n langfuse get secret langfuse.langfuse--pg.credentials.postgresql.acid.zalan.do -o json | jq  -r '.data.password' | base64 -d`
```

Get service:
```
SVC=`k -n langfuse get svc -l spilo-role=master --no-headers -o custom-columns=NAME:.metadata.name`
```

Create connection string secret:
```
kubectl -n langfuse create secret generic langfuse-pg-connection-string  --from-literal=connection=postgresql://langfuse:${PASS}@${SVC}:5432/langfuse
```

## Flux

```
k -n langfuse apply -f ./flux-sync.yml
```

## Web

Change admin password in WebUI.


## force sync

```
flux -n langfuse reconcile source git langfuse
```
