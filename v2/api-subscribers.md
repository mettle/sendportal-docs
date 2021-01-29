# Subscribers

## Index

Retrieve a paginated list of all subscribers.

### Usage

#### Endpoint

`GET /api/v1/workspaces/{workspaceId}/subscribers`

#### Expected Response Code
200

#### Response Fields

- data: `array<object>`
    - id: `int`
    - first_name: `string`
    - last_name: `string`
    - email: `string`
    - unsubscribed_at: `datetime`
    - created_at: `datetime`
    - updated_at: `datetime`

#### Sample Request

```
GET /api/v1/workspaces/1/subscribers HTTP/1.1
Host: sendportal.local
Authorization: Bearer GbvZ6u0UJU7EE2thKTgj1mMH7yaCm23JKRomIpkiIuZ7kfWLlVBqraAldz7Fxezw3B2M45NFL2OUm5ev
Accept: application/json
```

#### Sample Response

```json
{
    "data": [
        {
            "id": 1,
            "first_name": "Test",
            "last_name": "Subscriber",
            "email": "testsubscriber@example.com",
            "unsubscribed_at": null,
            "created_at": "2020-03-23 13:44:09",
            "updated_at": "2020-03-23 13:44:09"
        },
        {
            "id": 2,
            "first_name": "Test",
            "last_name": "Subscriber Two",
            "email": "testsubscriber2@example.com",
            "unsubscribed_at": "2020-08-02 08:07:08",
            "created_at": "2020-03-23 13:50:39",
            "updated_at": "2020-03-23 13:50:39"
        }
    ],
    "links": {
        "first": "<https://sendportal.local/api/v1/workspaces/1/subscribers?page=1>",
        "last": "<https://sendportal.local/api/v1/workspaces/1/subscribers?page=1>",
        "prev": null,
        "next": null
    },
    "meta": {
        "current_page": 1,
        "from": 1,
        "last_page": 1,
        "path": "<https://sendportal.local/api/v1/workspaces/1/subscribers>",
        "per_page": 25,
        "to": 2,
        "total": 2
    }
}
```

## Show

Retrieve the details of a single subscriber, including the segments.

### Usage

#### Endpoint

`GET /api/v1/workspaces/{workspaceId}/subscribers/{subscriberId}`

#### Expected Response Code
200

#### Response Fields

- data: `object`
    - id: `int`
    - first_name: `string`
    - last_name: `string`
    - email: `string`
    - segments: `array<object>`
        - id: `int`
        - string: `string`
        - created_at: `datetime`
        - updated_at: `datetime`
    - unsubscribed_at: `datetime`
    - created_at: `datetime`
    - updated_at: `datetime`

#### Sample Request

```
GET /api/v1/workspaces/1/subscribers/1 HTTP/1.1
Host: sendportal.local
Authorization: Bearer GbvZ6u0UJU7EE2thKTgj1mMH7yaCm23JKRomIpkiIuZ7kfWLlVBqraAldz7Fxezw3B2M45NFL2OUm5ev
Accept: application/json
```

#### Sample Response

```json
{
    "data": {
        "id": 1,
        "first_name": "Test",
        "last_name": "Subscriber",
        "email": "testsubscriber@example.com",
        "segments": [
            {
                "id": 1,
                "name": "Test Segment",
                "created_at": "2020-03-23 12:44:14",
                "update_at": "2020-03-23 12:44:14"
            }
        ],
        "unsubscribed_at": null,
        "created_at": "2020-03-23 13:44:09",
        "updated_at": "2020-03-23 13:44:09"
    }
}
```

## Store

Create a new subscriber, optionally including segments the subscriber should be included in.

### Usage

#### Endpoint

`POST /api/v1/workspaces/{workspaceId}/subscribers`

#### Expected Response Code
201

#### Request Fields

- first_name: `string` (optional)
- last_name: `string` (optional)
- email: `string`
- unsubscribed_at: `datetime` (optional)
- segments: `array<int>` (optional)

#### Response Fields

- data: `object`
    - id: `int`
    - first_name: `string`
    - last_name: `string`
    - email: `string`
    - segments: `array<object>`
        - id: `int`
        - name: `int`
        - created_at: `datetime`
        - updated_at: `datetime`
    - unsubscribed_at: `datetime`
    - created_at: `datetime`
    - updated_at: `datetime`

#### Sample Request

```
POST /api/v1/workspaces/1/subscribers HTTP/1.1
Host: sendportal.local
Authorization: Bearer GbvZ6u0UJU7EE2thKTgj1mMH7yaCm23JKRomIpkiIuZ7kfWLlVBqraAldz7Fxezw3B2M45NFL2OUm5ev
Accept: application/json
Content-Type: application/json

{
	"first_name": "Test",
	"last_name": "Subscriber Two",
	"email": "testsubscriber2@example.com",
	"segments": [1]
}
```

#### Sample Response

```json
{
    "data": {
        "id": 2,
        "first_name": "Test",
        "last_name": "Subscriber two",
        "email": "testsubscriber2@example.com",
        "segments": [
            {
                "id": 1,
                "name": "Test Segment",
                "created_at": "2020-03-23 12:44:14",
                "update_at": "2020-03-23 12:44:14"
            }
        ],
        "unsubscribed_at": null,
        "created_at": "2020-03-24 10:43:08",
        "updated_at": "2020-03-24 10:43:08"
    }
}
```

## Update

#### Endpoint

`PUT /api/v1/workspaces/{workspaceId}/subscribers/{subscriberId}`

#### Expected Response Code
200

#### Description
Update the details of the given subscriber.

#### Request Fields

- first_name: `string` (optional)
- last_name: `string` (optional)
- email: `string`
- unsubscribed_at: `datetime` (optional)

#### Response Fields

- data: `object`
    - id: `int`
    - first_name: `string`
    - last_name: `string`
    - email: `string`
    - unsubscribed_at: `datetime`
    - created_at: `datetime`
    - updated_at: `datetime`

#### Sample Request

```
PUT /api/v1/workspaces/1/subscribers/2 HTTP/1.1
Host: sendportal.local
Authorization: Bearer GbvZ6u0UJU7EE2thKTgj1mMH7yaCm23JKRomIpkiIuZ7kfWLlVBqraAldz7Fxezw3B2M45NFL2OUm5ev
Accept: application/json
Content-Type: application/json

{
	"first_name": "Test",
	"last_name": "Subscriber Two Updated",
	"email": "testsubscriber2@example.com",
	"segments": [1]
}
```

#### Sample Response

```json
{
    "data": {
        "id": 2,
        "first_name": "Test",
        "last_name": "Subscriber Two Updated",
        "email": "testsubscriber2@example.com",
        "unsubscribed_at": null,
        "created_at": "2020-03-24 10:43:08",
        "updated_at": "2020-03-24 10:50:20"
    }
}
```

## Delete

Delete the given subscriber.

### Usage

#### Endpoint

`DELETE /api/v1/workspaces/{workspaceId}/subscribers/{subscriberId}`

#### Expected Response Code
204

#### Sample Request

```
DELETE /api/v1/workspaces/1/subscribers/2 HTTP/1.1
Host: sendportal.local
Authorization: Bearer GbvZ6u0UJU7EE2thKTgj1mMH7yaCm23JKRomIpkiIuZ7kfWLlVBqraAldz7Fxezw3B2M45NFL2OUm5ev
Accept: application/json
```
