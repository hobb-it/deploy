# Deploy

Per fare il deploy dell'applicazione bisogna creare due file:

1. db-config.yml
2. user-service-secret.yml

Per creare questi file utilizzare i template forniti.

Dopo di che seguire i seguenti passi:

```bash
kubectl apply -f db-config.yml
```

```bash
kubectl apply -f user-service-secret.yml
```

E infine 

```bash
kubectl apply -f user.yml
```