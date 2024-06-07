# Errors

Our API uses conventional HTTP response codes to indicate the success or failure of an API request. In general, codes in the `2xx` range indicate success, codes in the `4xx` range indicate an error that failed given the information provided (e.g., a required parameter was omitted), and codes in the `5xx` range indicate an error with our servers.

We may also return errors in the json responses which will follow the `message` and `description` format. Message usually just contains the `http` error code and the description contains a more detailed description of the error.

For some endpoint such as the **oauth2** we follow the payload formats errors in the `error` and `error_description` format where `error` is an error key and `error_description` is a description of the error.

## HTTP Error Codes

| Code | Name        | Description |
|------|-------------|-------------|
| 200  | Ok          | Everything went as expected |
| 201  | Created     | The resource was created successfully |
| 204  | No Content  | The request was successful but there is no content to return |
| 400  | Bad Request | The request was malformed or missing required parameters |
| 401  | Unauthorized| The request was missing a valid API key or access token |
| 403  | Forbidden   | The request was valid but the server is refusing action |
| 404  | Not Found   | The requested resource was not found |
| 405  | Method Not Allowed | The request method is not allowed for the endpoint |
| 415  | Unsupported Media Type | The request was made with an unsupported media type |
| 429  | Too Many Requests | The request was rate limited |
| 500  | Internal Server Error | The server encountered an error while processing the request. If you encounter these please report them! |
| 502  | Bad Gateway | The server was acting as a gateway or proxy and received an invalid response from the upstream server |
| 503  | Service Unavailable | The server is currently unavailable (overloaded or down) |
| 504  | Gateway Timeout | The server was acting as a gateway or proxy and did not receive a timely response from the upstream server |

## Oauth2 Errors

When using the oauth2 service you may encounter the following errors when the user is redirected back to your application:

| Error           | Description |
|-----------------|-------------|
| `invalid_request`| The oauth url was malformed and the `error_description` will contain more information |
|`unsupported_response_type`| The response type is not supported by the server |
|`invalid_scope`| The scope requested is invalid or not supported by the server |
|`forbidden_scope`| Your application is not allowed to use this scope |
|`access_denied` | The resource owner or authorization server denied the request |

The following errors may be returned when exchanging a code for an access token. For most of them the `error_description` will contain more information about the error.

| Error           | Description |
|-----------------|-------------|
|`unsupported_grant_type`| The grant type is not supported by the server |
|`invalid_request`| The request was malformed and the `error_description` will contain more information |
|`invalid_client`| The client id or client secret is invalid |
|`server_error`| The server encountered an error while processing the request |

