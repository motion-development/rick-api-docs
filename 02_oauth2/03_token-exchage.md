
# Token Exchange

Once you have obtained a `code` from the user by [authorizing the user](authorizing-the-user), you can exchange the `code` for an access token. The access token is used to authenticate requests to our API. To exchange the `code` for an access token, you will need to make a `POST` request to the `/oauth2/token` endpoint.

:: POST /oauth2/token ::

Endpoint to exchange a code for an access token, or to refresh an access token. The payload may vary depending on the grant type used. No authorization headers are required for this endpoint since all authorization is done through the payload.

### Code Exchange

To exchange a `code` for an access token, you will need to provide the following payload:

| Field | Type | Description |
|-------|------|-------------|
| `client_id` | string | The client id of your application. |
| `client_secret` | string | The client secret of your application. |
| `code` | string | The code obtained from the user. |
| `redirect_uri` | string | The redirect uri used to obtain the code. |
| `grant_type` | string | The grant type, should be set to `authorization_code` to exchange a code |

### Refresh Token

To refresh an access token, you will need to provide the following payload:

| Field | Type | Description |
|-------|------|-------------|
| `client_id` | string | The client id of your application. |
| `client_secret` | string | The client secret of your application. |
| `refresh_token` | string | The refresh token obtained from the user. |
| `grant_type` | string | The grant type, should be set to `refresh_token` to refresh an access token |
| `scope`?\* | string | The scope of the access request, see the [scopes section](getting-started#scopes) for more information. |

\*The `scope` may contain the same scopes as the original access token, or a subset of the original scopes. If the `scope` is not provided, the original scopes will be used.

### Response

If the request is successful (a `200: Ok` response), the response will contain the following payload:

| Field | Type | Description |
|-------|------|-------------|
| `access_token` | string | The access token to authenticate requests. |
| `token_type` | string | The type of token, should be set to `Bearer`. |
| `expires_in` | integer | The number of seconds until the access token expires. |
| `refresh_token` | string | The refresh token to refresh the access token. |
| `scope` | string | The scope of the access token. |

If the request is unsuccessful, the response will contain an error payload. See the [errors section](../errors#oauth2-errors) for more information.

## Access Tokens

Access tokens are generaly valid for 14 days unless otherwise stated by the `expires_in` field in the response. Once an access token expires, you will need to refresh the access token by following the [refresh token](#refresh-token) section. Refresh tokens do not expire and can be used to obtain a new access token at any time. And refresh token may only be used **once** and will expire after use.


## Token Revocation

Users can revoke access to your application at any time and your application should handle this accordingly. If a user revokes access to your application all its access tokens and refresh tokens will be invalidated. You should prompt the user to reauthorize your application if this happens. 

The api will return `invalid_code` or `invalid_token` errors if the code or token is invalid. You should prompt the user to reauthorize your application if this happens.
