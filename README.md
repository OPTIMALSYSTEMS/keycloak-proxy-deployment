# keycloak-proxy-deployment

## Prerequisites
Helm3 - https://github.com/helm/helm/releases/tag/v3.7.2

## Deploying keycloak proxy
Keycloak instances and proxy require unique public listed DNS records.
```
*kc001.example.net*
*keycloak.proxy.example.net*
```

Proxy is managing instances via *keycloak-proxy.yaml* configuration file, located in the git repository of the *infrastructure* chart.
New keycloak instances are automatically added to the file via kubernetes job.

### Infrastructure chart
1. Set DNS, keycloak-instance/database/git credentials for default keycloak instance in *infrastructure/values.yaml*   
2. Integrate templates and values into yuuvis api *infrastructure* helm chart.
3. Install infrastructure helm chart according to yuuvis api helm chart documentation.

### Yuuvis chart
1. Set DNS and credentials for keycloak proxy in *yuuvis/values.yaml*. 
2. Set DNS and credentials for default keycloak instance, database and git, as specified in *infrastructure/values*.yaml. These are subsequently added to *keycloak-proxy.yaml* via kubernetes job. 
3. Integrate templates and values into yuuvis api *yuuvis* helm chart.
4. Install yuuvis helm chart according to yuuvis api helm chart documentation.

Keycloak proxy is now running in *yuuvis* namespace and pointing to default keycloak instance running in *infrastructure* nameespace.

## Adding new keycloak instance
Each keycloak instance can hold up to 50 tenants. Additonal tenants require a new instance.

1. Set DNS and credentials for new keycloak instance in *keycloak-instance/values.yaml*
2. Set credentials for database and git, as specified in *infrastructure/values*.yaml.
3. Install keycloak instance via helm to new namespace.
```
helm install keycloak-instance-2 ./keycloak-instance -n keycloak-instance-2
```


