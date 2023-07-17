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

![image](https://github.com/michelangelodorado/oidc-nginx-nms/assets/102953584/2d4694c0-0e20-4b5f-b3fa-473acab76682)

Go to users, add user juice-developer, click Credentials, set password to juice-developer and turn off Temporary or else
the user will have to change it on first login.

Browse to http://10.1.1.9:8080/realms/test/.well-known/openid-configuration

![image](https://github.com/michelangelodorado/oidc-nginx-nms/assets/102953584/30155368-88b4-48ed-bbae-d152e0299e02)

OIDC Configuration
On the Juice Gateway, configure the OIDC template as follows:

| OIDC Setting  | Value |
| ------------- | ------------- |
| OIDC Authorize Endpoint  | http://10.1.1.9:8080/realms/test/protocol/openid-connect/auth  |
| OIDC Token Endpoint  | http://10.1.1.9:8080/realms/test/protocol/openid-connect/token  |
| OIDC JWKS URI  | http://10.1.1.9:8080/realms/test/openid-connect/certs  |
| Client ID | juice |
| Client Secret | WoWs70m1DXKLRbBxL4CSqi2KmWpaAQ0L |

![image](https://github.com/michelangelodorado/oidc-nginx-nms/assets/102953584/e48e45ed-8222-4a5c-b1bc-a1ea14fa728e)

Configure the Juice Web Component by setting OIDC authentication to TRUE

![image](https://github.com/michelangelodorado/oidc-nginx-nms/assets/102953584/25fd0fcb-cdab-47e5-927c-e1907f15e29b)

Test OIDC
1. Reload the browser tab with https://juice.bigtechdojo.com
2. You will be re-directed to Keycloak to complete a Login authorization flow
3. Login as : juice-developer / juice-developer
4. Keycloak will re-direct you to the application
