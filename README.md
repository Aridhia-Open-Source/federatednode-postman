# Federated Node postman collection

### Pre-requisite
- The hostname the FN is deployed on is `https://phems-federatednode.net` in the [base env](./envs/base.postman_environment.json) as `base_url` variable. Alternatively, the nginx or backend service can be `port-forward`ed  from the cluster and be accessed via `localhost`.
- In case it is run in a local cluster, add the hostname to your `hosts` file.

### Port forwards
|service|ports|
|--|--|
|service/db|5432|
|service/keycloak|8080:80|
|service/federatednode-ingress-nginx-controller|443|

They are not all mandatory, but in a combination of them. e.g. if the backend is running from outside the cluster, `db` and `keycloak` are needed.
If the goal is to emulate a prod env, `federatednode-ingress-nginx-controller` is the only one needed.


## Automation
In general, most of the endpoints have post scripts that will save some response information in variables. For instance, after a login, upon a successful response, the `.token` field will be saved into the `admin_token` variable. This will be then used as bearer token in all admin-related requests (either explicitly, or as `Inherited by parent`)
