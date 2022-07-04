# keycloak-proxy-deployment

## Prerequisites
Helm3 - https://github.com/helm/helm/releases/tag/v3.7.2

## Deploying keycloak proxy
Register DNS records for all keycloak instances and proxy.
```
https://auth.example.net
https://proxy.example.net
```
Instances are listed in config file *keycloak-proxy.yaml*.

### Keycloak proxy chart
Edit *changeme* credentials and DNS records in *keycloak-proxy/values.yaml*
```
helm install keycloak-proxy ./keycloak-proxy -n yuuvis
```
Keycloak proxy is now running in *yuuvis* namespace.

## Adding new keycloak instance
Edit *changeme* credentials and DNS records in *keycloak-instance/values.yaml*
```
helm install keycloak-instance-2 ./keycloak-instance -n keycloak-instance-2
```
Keycloak instances can hold up to 100 tenants.
