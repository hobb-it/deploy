# Deploy

Per fare il deploy dell'applicazione bisogna creare due file:

1. db-config.yml
2. user-service-secret.yml

Per creare questi file utilizzare i template forniti.

Dopo di che seguire i seguenti passi:

```bash
kubectl apply -f k8s/user-service/db-config.yml
```

```bash
kubectl apply -f k8s/user-service/user-service-secret.yml
```

E infine 

```bash
kubectl apply -f k8s/user-service/user.yml
```

## Collegamento a Google Cloud

In db-config.yml sostituisce data.db_url con:
URL: "jdbc:postgresql://34.65.114.98:5432/user-db"

In user-service-secret.yml sostituisce db-username e db-password con base64encode di User e Password