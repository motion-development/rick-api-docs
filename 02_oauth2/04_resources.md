# Resources

Once you have obtained an access token, you can use it to access user data. This page will document the resources available to you and how to access them.

:: GET /users/@me ::

Endpoint to access the current user's information. The user's information will be returned in the response payload.

| Field           | Type     | Required Scope   | Description                                                |
|-----------------|----------|------------------|------------------------------------------------------------|
| `id`            | string   | `identify`       | The user's ID                                              |
| `username`      | string   | `identify`       | The user's username                                        |
| `display_name`  | string   | `identify`       | The user's display name                                    |
| `flags`         | integer  | `identify`       | [User flags](#user-flags)                                  |
| `created_at`    | integer  | `identify`       | Unix timestamp indicating the creation time of the account |
| `avatar`        | string   | `identify`       | The user's avatar (May be "default" if none set)           |
| `banner`        | string   | `identify`       | The user's banner (May be "default" if none set)           |
| `bio`           | string   | `identify`       | The user's bio                                             |
| `email`         | string   | `email`          | The user's email address                                   |

### User Flags

User flags will contain some information about the user. We use a [bitfield](../introduction#bitfields) to store the user flags. The following flags are available:

| Flag Value | Name         | Description                                                       |
|------------|--------------|-------------------------------------------------------------------|
| 1<<0       | `unverified` | The user has not verified their email address                     |
| 1<<1       | `developer`  | The user has access to create applications                        |
| 1<<2       | `admin`      | The user is a website admin and has the red "website admin" badge |
| 1<<3       | `banned`     | The user is banned from the website                               |
| 1<<4       | `verified`   | The user is verified and has the blue "verified" badge            |
| 1<<5       | `tester`     | The user has access to beta features and a "beta tester" badge    |
| 1<<6       | `moderator`  | The user is a website moderator                                   |

# User Links

Manage the user's links.

:: GET /users/@me/links ::

Endpoint to access the current user's links. Will return a list of [link objects](#link-object) in the response payload.
This endpoint will require the `links.view` scope.

:: POST /users/@me/links ::

Endpoint to create a new link for the current user. The payload should contain a [link object](#link-object) with the required fields.
This endpoint will require the `links.edit` scope.

:: PATCH /users/@me/links/{link.id} ::

Endpoint to update an existing link for the current user. The payload should contain a [link object](#link-object) with the fields to update.
This endpoint will require the `links.edit` scope.

:: DELETE /users/@me/links/{link.id} ::

Endpoint to delete an existing link for the current user.
This endpoint will require the `links.delete` scope.

### Link Object

Link objects contain information about the user's links.

| Field             | Type                             | Description                                               |
|-------------------|----------------------------------|-----------------------------------------------------------|
| `link_id`         | string                           | The link ID used in the URL                               |
| `embed`           | [embed-object](#embed-object)    | The embed object containing the link's embed information  |
| `page`            | [page-object](#page-object)      | The page object containing the link's page information    |
| `created_at`\*    | integer                          | Unix timestamp indicating the creation time of the link   |
| `expires_at`\*    | integer                          | Unix timestamp indicating the expiration time of the link |
| `expires_in`\*\*  | integer                          | The number of days until the link expires                 |
| `visits`\*        | integer                          | The total number of visits to the link                    |
| `unique_visits`\* | integer                          | The total number of unique visits to the link             |
| `id`              | integer                          | The link's ID (Used for editing / deleting links)         |
| `page_url`        | string                           | The [page URL](#link-meta-data) of the link               |
| `url`\*           | string                           | The full URL of the link                                  |

\*These fields cannot be modified

\*\*These fields are only required when creating or modifying a link and are not present in the response.

### Embed Object

The embed object contains the information used to display the link's embed.

| Field          | Type    | Description                  |
|----------------|---------|------------------------------|
| `author`?      | string  | The author of the link       |
| `title`?       | string  | The title of the link        |
| `description`? | string  | The description of the link  |
| `image`?       | string  | The image URL of the link    |
| `color`?       | string  | The color of the embed       |

These items are nullable and are not required. If not present, the server will return an empty string.

### Page Object

The page object contains the information used to display the link's page.

| Field           | Type    | Description                                   |
|-----------------|---------|-----------------------------------------------|
| `title`?        | string  | The title of the page                         |
| `description`?  | string  | The description of the page                   |
| `page_style`    | string  | The [page style](#link-meta-data) of the page |
| `video`         | string  | The [video](#page-meta-data) of the page      |

Some items are nullable and are not required. If not present, the server will return an empty string.

### Link Meta Data

Some of the fields of a link object contain meta data which can change frequently, such as the `page_style` and `video` fields. Your application should try to update these fields at least once per day to ensure the data is up to date. You may use the following endpoint to update the meta data of a link.

:: GET /links-metadata ::

Will return a [metadata](#metadata-object) object containing the latest meta data for the link.

### Metadata Object

| Field          | Type                                     | Description                         |
|----------------|------------------------------------------|-------------------------------------|
| `page-styles`  | List of [page-style](#page-style-object) | A list of page styles available     |
| `videos`       | List of [video](#video-object)           | A list of videos available          |
| `uris`         | List of strings                          | A list of URIs that can be used     |
| `domains`      | List of strings                          | A list of domains our site runs on  |

### Page Style Object

| Field  | Type    | Description                                                |
|--------|---------|------------------------------------------------------------|
| `id`   | string  | The ID of the page style (Should be used in your requests) |
| `name` | string  | The name of the page style                                 |

### Video Object

| Field      | Type     | Description                                               |
|------------|----------|-----------------------------------------------------------|
| `id`       | string   | The ID of the video (Should be used in your requests)     |
| `name`     | string   | The name of the video                                     |
| `message`  | string   | The message displayed as soon as the video is shown       |
| `special`  | boolean  | If the video is a special video (Used for special events) |
| `visible`  | boolean  | Whether the video is selectable by users on the home page |
| `link`     | string   | A [CDN link](../introduction#cdn) to the video            |

:: POST /users/@me/social/posts ::

Endpoint to create a new post on the user's profile. The payload should contain a [post object](#post-object) with the required fields.

:::alert orange
This endpoint is still in development and will return a `501: Not Implemented` response.
:::

### Post Object

:::alert orange
To be implemented
:::
