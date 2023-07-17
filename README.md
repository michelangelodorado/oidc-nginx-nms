# oidc-nginx-nms
test files



## KeyCloak Setup

KeyCloak is configured at http://10.1.1.9:8080 and admin/admin. This is run easily as a docker container:
```sh
docker run -d --restart unless-stopped -p 8080:8080 -e KEYCLOAK_ADMIN=admin -e
KEYCLOAK_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:22.0.0 start-dev
```
Create a new realm named Test. Create a new client and configure the Client ID to be: juice, set Client authentication to
On, and set the valid redirect URL to https://juice.bigtechdojo.com:443/_codexch
