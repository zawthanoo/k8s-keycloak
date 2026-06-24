# Keycloak on Kubernetes

This setup installs Keycloak on Kubernetes without Helm and exposes it at:

```text
http://mycluster.local.com/keycloak
```

PostgreSQL is assumed to already exist.

Default example database values:

```text
Database: keycloakdb
Username: keycloakuser
Password: keycloak123
```

Before applying, update `KC_DB_URL` in `02-configmap.yaml` if your PostgreSQL service/host is not `postgresql`:

```yaml
KC_DB_URL: jdbc:postgresql://postgresql:5432/keycloakdb
```

Apply:

```bash
cd /Users/zawthanoo/dev/devops-workshop/devops-apps/keycloak
kubectl apply -f .
```

Check:

```bash
kubectl get pods,svc,ingress -n keycloak
kubectl logs deploy/keycloak -n keycloak
```

Open:

```text
http://mycluster.local.com/keycloak
```

Login:

```text
Username: admin
Password: admin123
```

For real environments, change the admin password, do not commit real secrets, and pin the Keycloak image tag instead of using `latest`.
