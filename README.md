# Deploy dell'Applicazione Hobb.it

Questo repository contiene i file di configurazione dell’applicazione Hobb.it e i relativi comandi per avviarla.

Per effettuare il deploy, è necessario avere un’istanza di PostgreSQL per poter creare un database per ogni microservizio. Per semplicità, suggeriamo un comando per creare un unico database per entrambi i microservizi usando Docker.
In alternativa, modificando i file di configurazione di Kubernetes, è possibile collegarsi a un’istanza su Google Cloud.

## Creazione DB con Docker

Comando per creare un database usando Docker:

```bash
docker run --name hobbit-db -e POSTGRES_DB=users -e POSTGRES_USER=admin -e POSTGRES_PASSWORD=admin -p 5432:5432 -d postgres
```

Con il seguente comando possiamo accedere al databsse appena creato su Docker:

```bash
docker exec -it hobbit-db psql -U admin -d users
```

## Connessione al DB in Cloud

Per utilizzare il database su Google Cloud modifica i file .yml dei microservizi interessati, user.yml e hobbycard.yml, aggiornando le credenziali di accesso e l’URL del database. 

```yml
env:
  - name: DB_URL
    value: "jdbc:postgresql://34.65.114.98:5432/users-db"
  - name: DB_USERNAME
    value: "username"
  - name: DB_PASSWORD
    value: "password"
```

`username` e `password` sono stati oscurati per motivi di sicurezza.

## Avvio di Kubernetes

Una volta creato il database, avviare Kubernetes tramite Minikube.

Avvio minikube

```bash
minikube start
```

Caricamento dei file di configurazione, presenti nella cartella `k8s`

```bash
kubectl apply -f k8s
```

Questo comando crea i deployment dell'applicazione, e minikube si occuperà di creare i relativi pods.

## Forwarding delle porte

Per esporre i microservizi all’esterno, utilizzare il comando seguente:

```bash
minikube tunnel
```

Per esporre il frontend e poterci collegare dal nostro browser eseguiamo il seguente comando, che collegherà la porta interna di minikube alla porta della nostra macchina

```bash
kubectl port-forward svc/hobbit-frontend 3000:3000
```

## Accedi ad Hobb.it

Seguendo questi semplici passaggi sarà possibile collegarsi all'applicazione tramite questo link [http://localhost:3000](http://localhost:3000).