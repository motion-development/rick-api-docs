# Oauth2 - Getting Started

To get started with our oauth2 service, you will need to create an application. Applications are used to authenticate users and access their data. You can create an application by visiting the [applications page](/me/developers), assuming you are an approved developer on our site.

Once you have created an application, you will be given a `client_id` and a `client_secret`. These are used to authenticate your application and access user data. You can use these credentials to authenticate your application and access user data. Your `client_secret` will only be shown once, so make sure to save it in a secure location. If you lose your `client_secret`, you will need to regenerate it which will invalidate the previous secret.

Our oauth2 service followed the [rfc6749](https://tools.ietf.org/html/rfc6749) closely. And therefore all the endpoints documented under the oauth2 section will require the `application/x-www-form-urlencoded` content type. The endpoints will also require the `client_id` and `client_secret` to be passed in the request body. The `client_id` and `client_secret` should be passed as `client_id` and `client_secret` respectively.

:::alert orange
Since we follow the [rfc6749](https://tools.ietf.org/html/rfc6749) closely, all oauth2 endpoints will require the `application/x-www-form-urlencoded` content type and do not support the `application/json` content type.
:::


## Creating an Application

To create an application, you will need to visit the [applications page](/me/developers) and click on the `Create Application` button. Your application name must reflect that of your application and must not be misleading. We reserve the right to remove any applications that may be misleading or harmful to our users. Next set the application icon to reflect your application. 

The redirect uris must be an url back to your application's website which will handle the oauth2 process. The redirect uris may contain a path, query string, and may not contain a fragment. The redirect URI must start with `http://` or `https://`, the user may be shown a warning if the redirect uri does not start with `https://`. Your application may have up to 10 redirect uris.


# Scopes

Scopes are used to limit the access your application has to a user's data. Scopes are passed in the authorization URL and are used to limit the access your application has to a user's data. Scopes are space separated and are case sensitive. Certain Applications may have access to different scopes. Refer your application's [dashboard](/me/developers) to see the scopes your application has access to.

The following scopes are available:

| Scope | Description | Documentation |
|-------|-------------| --------------|
| `identify` | Allows your application to access basic user information. | [User Information](resources#user) |
| `email` | Allows your application to access the user's email address. | [User Information](resources#user) |
| `links.view` | Read access to the user's links. | [User Links](resources#links) |
| `links.edit` | Create and edit access to the user's links. | [User Links](resources#manage-links) |
| `links.delete` | Delete access to the user's links. | [User Links](resources#manage-links) |
| `social.post` | Create posts on the users profile | [User Social](resources#social) |