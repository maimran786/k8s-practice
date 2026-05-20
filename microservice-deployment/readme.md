votepod - vote-service -port -80 -image-kodekloud
redispod- redis-service - port -6379 -image-redis:alpine
workerpod- 
postgrespod- postgre-service- port -5432 -image-postgres:alpine env-name&pass
resultpod - result-service -port 80 -image -kodekloud

Postgres credentials:

Create a local `.env` file and set real values:

```env
POSTGRES_USER=your-user
POSTGRES_PASSWORD=your-password
POSTGRES_DB=your-db
```

Do not commit `.env`. Create or update the Kubernetes Secret from that file:

```powershell
kubectl create secret generic postgres-db-secret --from-env-file=.env --dry-run=client -o yaml | kubectl apply -f -
```

Then recreate the Postgres pod so it reads the updated Secret:

```powershell
kubectl delete pod postgres-db-pod
kubectl apply -f .\microservice-deployment\election-pods\postgres-db-pod.yaml
```
