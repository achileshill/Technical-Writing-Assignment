# Technical-Writing-Assignment

## `GET /v1/playlists/{playlist_id}`
**Retrieves detailed information about a specific playlist**

---

## Overview

This endpoint provides metadata about a playlist, including:

- Name  
- Description  
- Owner information  
- Tracks  
- Images  
- Followers  

It is commonly used to display playlist details in applications or to analyze playlist content.

---

## Request

**Method:** `GET`  
**URL:** `https://api.spotify.com/v1/playlists/{playlist_id}`

### Path Parameters

| Name          | Type     | Description                        |
|---------------|----------|------------------------------------|
| `playlist_id` | string | The Spotify ID of the playlist.    |

### Query Parameters

| Name     | Type     | Description | Example |
|----------|----------|-----------------------|---------|
| `market` | string | An ISO 3166-1 alpha-2 country code. If provided, tracks will be returned only if available in that market. If a valid user access token is specified in the request header, the country associated with the user account will take priority over this parameter. | `market=VN` |
| `fields` | string | A comma-seperated list of the fields to return. If omitted, all fields are return. | `fields=description,uri` |
| `additional_types` | string | A comma-separated list of item types that clien supports besides the default track type. Track and episode are valid types |

### Headers

| Name            | Required | Description                             |
|-----------------|:--------:|-----------------------------------------|
| `Authorization` | Yes      | Bearer token for the current user (OAuth 2.0). |
| `Content-Type`  | No       | Typically `application/json`.           |

---

## Response

**Status Code:** `200`  
**Content-Type:** `application/json`

### Example Body

```json
{
  "collaborative": false,
  "description": "A collection of my favorite tracks.",
  "external_urls": {
    "spotify": "https://open.spotify.com/playlist/3cEYpjA9oz9GiPac4AsH4n"
  },
  "followers": {
    "href": null,
    "total": 0
  },
  "href": "https://api.spotify.com/v1/playlists/3cEYpjA9oz9GiPac4AsH4n",
  "id": "3cEYpjA9oz9GiPac4AsH4n",
  "images": [
    {
      "height": null,
      "url": "https://i.scdn.co/image/ab67706f000000033e6b8e3c6f8f3f4b8b6b8e3c",
      "width": null
    }
  ],
  "name": "My Playlist",
  "owner": {
    "display_name": "Spotify",
    "external_urls": {
      "spotify": "https://open.spotify.com/user/spotify"
    },
    "href": "https://api.spotify.com/v1/users/spotify",
    "id": "spotify",
    "type": "user",
    "uri": "spotify:user:spotify"
  },
  "public": true,
  "snapshot_id": "MySnapshotId",
  "tracks": {
    "href": "https://api.spotify.com/v1/playlists/3cEYpjA9oz9GiPac4AsH4n/tracks",
    "total": 10
  },
  "type": "playlist",
  "uri": "spotify:playlist:3cEYpjA9oz9GiPac4AsH4n"
}
```
### Response Fields

| Field           | Type     | Description |
|:----------------|:--------:|------------|
| `collaborative` | boolean  | Whether the playlist is collaborative. |
| `description`   | string   | Playlist description. |
| `external_urls` | object   | External URLs for the playlist. |
| `href`          | string   | Spotify Web API endpoint URL for the playlist. |
| `id`            | string   | Spotify ID for the playlist. |
| `images`        | array    | Array of image objects representing the playlist's cover art. Array may be empty or contain up to three images in descending order of size |
| `name`          | string   | Name of the playlist. |
| `owner`         | object   | Information about the playlist's owner.  <br>• `external_urls` (object) – Public external URLs for the user <br>• `href` (string) – Link to the Web API endpoint for this user <br>• `id` (string) – Spotify user ID <br>• `type` (string) – Object type <br>• `display_name` (string) – User's name (`user`) <br>• `uri` (string) – Spotify URI ||
| `public`        | boolean  | Whether the playlist is public. |
| `snapshot_id`   | string   | A unique identifier for the current playlist state. |
| `tracks`        | object   | Information about the tracks in the playlist. <br>• `limit` (integer) – Maximum number of items in the response <br>• `href` (string) – Link to the Web API endpoint for the request <br>• `next` (string) – URL to the next page of itmes <br>• `offset` (integer) – The offset of the items returned <br>• `previous` (string) – URL to the previous page of items (`user`) <br>• `total` (integer) – Total number of items available to return|
| `type`          | string   | Type of the object (`playlist`). |
| `uri`           | string   | Spotify URI for the playlist. |

---
## Example Request (Python)

```python
playlist_id = "3cEYpjA9oz9GiPac4AsH4n"
access_token = "SPOTIFY_OAUTH_TOKEN"
headers = {
    "Authorization": f"Bearer {access_token}"
}

response = requests.get(f"https://api.spotify.com/v1/playlists/{playlist_id}", headers=headers)
```
 ---
 ## Potential response
 | Status number | Description |
 |:----:|:----:|
 | `401` | Bad or expired token. This can happen if the user revoked a token or the access token has expired. You should re-authenticate the user. |
 | `403` | Bad OAuth |
 | `429` | The app has exceeded its rate limits |
