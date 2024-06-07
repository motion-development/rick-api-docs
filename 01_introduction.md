
# Rick Roll Link Generator API

Welcome to the Rick Roll Link Generator API! This API allows you to generate custom rick roll pages on our site. Or retrive information about certain links. Our API is currently private and requires developers to apply for access. If you are interested in using our API you can apply in the [developer portal](/me/developers) and optain your API keys there.


# About the API

All API access is over HTTPS, using various http methods to access / manipulate data. Our API only supports the `application/json` format for all its requests and responses, unless otherwise stated for the specific endpoints. You may encounter `415` errors if you do not set the `Content-Type` header to `application/json` in your requests. 

All requests must be authenticated with an API key. You can obtain an API key by applying for access in the [developer portal](/me/developers). More about authentication can be found in the [authentication section](#authentication).

Our api is located at `https://r.mtdv.me/api/v{version}` where `{version}` is the version of the API you are using. See the table below for the current version of the API and their respective status.

| API Version | Status | Should Use |
|-------------|--------|------------|
| v1          | Discontinued | No |
| v2          | Discontinued | No |
| v3          | Discontinued | No |
| v4          | Discontinued | No |
| v5          | Current | Yes |

## Errors

Our API uses conventional HTTP response codes to indicate the success or failure of an API request. In general, codes in the `2xx` range indicate success, codes in the `4xx` range indicate an error that failed given the information provided (e.g., a required parameter was omitted), and codes in the `5xx` range indicate an error with our servers. For more information on the errors you may encounter, see the [errors section](errors).



# Authentication

All endpoints documented in this documentation require authentication. Some endpoints may require different kinds of authentication, such as user authentication or application authentication depending on the permission level required for the endpoint. The access level may be documented in the endpoint's documentation, by default assume that the endpoint requires application authentication.


### Application Authentication

Application authentication is done by providing an API key in the `Authorization` header of the request. The API key should not have any prefix, and should be the only value in the header. Here is an example of how to authenticate with an API key:

```
Authorization: kA0YF5W2EahAL4Ru1qj8qP2rC7WrC6CCFSaWHAF77GMW612BGN
```

### User Authentication

User authentication is optained through our [ouath2](oauth2/getting-started) service. This allows you to authenticate users and access their data. More information about user authentication can be found in the [ouath2](oauth2/getting-started) section.

Once an access token is optained, you can use it to authenticate requests by providing it in the `Authorization` header of the request. The access token should have the `Bearer` prefix, and should be the only value in the header. Here is an example of how to authenticate with an access token:

```
Authorization: Bearer VdXX9pkfxXGPhCzKT8k6j01D10M59vg1eAC0upiw
```


# Understanding the documentation

The documentation is divided into sections, each section contains a group of endpoints that are related to each other. Each endpoint will have two tables, one labeled payload which contains the request body expected by the endpoint, and one labeled response which contains the response body returned by the endpoint. Some fields are nullable and may not be present in the response. Consider the following table:

| Field | Type | Description |
|-------|------|-------------|
| option? | string | The option field is optional in this request. If present it is of type string |
| option2 | string | The option2 field is required in this request. It is of type string |
| option3 | string? | Option3 may (or may not) be present in the response. The application should not rely on this value to be always present. |


# Image Formatting

Some endpoints or objects may contain images. These images are represented as a hash key in the response object. The hash key is a string that represents the image. Currently we only support the `png` format for images and the following sizes: 16, 32, 64, 128, 256, 512. Consider the following table for the uris for different images.

| URI | Description |
|-----|-------------|
| /profiles/[{user.id}](oauth2/resources#user-object)/[{user.avatar}](oauth2/resources#user-object).png | The avatar of the user.  |
| /banners/[{user.id}](oauth2/resources#user-object)/[{user.banner}](oauth2/resources#user-object).png\* | The banner of the user.  |
| /applications/[{application.id}](oauth2/resources#application-object)/[{application.icon}](oauth2/resources#application-object).png | The icon of the application.  |

\*The banner sizes are limited to: 500, 1000, 1500.

The assets are served from `https://r.mtdv.me/assets` and the full uri for an image would be `https://r.mtdv.me/assets/{uri}`.
To request a specific size of an image, you can add the `?size={size}` query parameter to the uri. The server may respond with a `400: Bad Request` if the requested size is not supported, or `404: Not Found` if the image does not exist.

## CDN

Some of our assets are hosted on a seperate CDN, such as our videos. The CDN is located at `https://cdn.mtdv.me` and the full uri for an asset would be `https://cdn.mtdv.me/{uri}`. The CDN is used to reduce load times and improve performance for our users.

# Bitfields

We store flags in bitfields as an easy way to store multiple boolean values in a single integer. Bit fields are integers where each bit represents a boolean value for a different "flag" or permission. Flags can be checked by using bitwise operations:

```python
flag = 65
if flag & 1<<0: 
    # Integer has the first bit set (In this example true.)

if flag & 1<<1:
    # Integer has the second bit set (In this example false.)
```