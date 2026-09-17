## Secrets

`11-db-secret.yaml` and `21-backend-secret.yaml` are **not committed** — they
contain real credentials. Only the `*.example.yaml` templates are in git.

To recreate them locally before applying the manifests:

```
cp 11-db-secret.example.yaml 11-db-secret.yaml
cp 21-backend-secret.example.yaml 21-backend-secret.yaml
```

Then edit `11-db-secret.yaml` / `21-backend-secret.yaml` and replace every
`CHANGE_ME` with real values (keep the password used in `21-backend-secret.yaml`'s
`DATABASE_URL` consistent with `11-db-secret.yaml`'s `POSTGRES_PASSWORD`).

Apply everything with:

```
kubectl apply -f .
```
