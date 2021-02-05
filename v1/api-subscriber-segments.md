# Subscriber Segments

## Index

Retrieve a list of the segments a subscriber is in.

### Usage

#### Endpoint

`GET /api/v1/workspaces/{workspaceId}/subscribers/{subscriberId}/segments`

#### Expected Response Code
200

#### Response Fields

- data: `array<object>`
    - id: `int`
    - name: `string`
    - created_at: `datetime`
    - updated_at: `datetime`

#### Sample Request

```
GET /api/v1/workspaces/1/subscribers/1/segments HTTP/1.1
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
            "name": "Test Segment",
            "created_at": "2020-03-23 12:44:14",
            "update_at": "2020-03-23 12:44:14"
        }
    ]
}
```

## Store

Adds a list of segments to the given subscriber. Returns a list of the segments that the subscriber is in.

This endpoint is idempotent, meaning that segments already added to the subscriber will not be continuously added on repeated requests to this endpoint. However, if the intention is to supply a full list of segments that the subscriber should be in, the Update endpoint should be used instead.

#### Endpoint

`POST /api/v1/workspaces/{workspaceId}/subscribers/{subscriberId}/segments`

#### Expected Response Code
200

#### Request Fields

- segments: `array<int>`

#### Response Fields

- data: `array<object>`
    - id: `int`
    - name: `string`
    - created_at: `datetime`
    - updated_at: `datetime`

#### Sample Request

```
POST /api/v1/workspaces/1/subscribers/1/segments HTTP/1.1
Host: sendportal.local
Authorization: Bearer GbvZ6u0UJU7EE2thKTgj1mMH7yaCm23JKRomIpkiIuZ7kfWLlVBqraAldz7Fxezw3B2M45NFL2OUm5ev
Accept: application/json
Content-Type: application/json

{
	"segments": [1, 2]
}
```

#### Sample Response

```json
{
    "data": [
        {
            "id": 1,
            "name": "Test Segment",
            "created_at": "2020-03-23 12:44:14",
            "update_at": "2020-03-23 12:44:14"
        },
        {
            "id": 2,
            "name": "Test Segment Two",
            "created_at": "2020-03-24 08:45:55",
            "update_at": "2020-03-24 08:57:21"
        }
    ]
}
```

## Update

Replaces the list of segments in a given subscriber with the one supplied in the request.

If you want to add additional segments to the subscriber without removing existing ones, you should use the Store endpoint. If you want to remove specific segments from the subscriber, you should use the Delete endpoint.

#### Endpoint

`PUT /api/v1/workspaces/{workspaceId}/subscribers/{subscriberId}/segments`

#### Expected Response Code
200

#### Request Fields

- segments: `array<int>`

#### Response Fields

- data: `array<object>`
    - id: `int`
    - name: `string`
    - created_at: `datetime`
    - updated_at: `datetime`

#### Sample Request

```
PUT /api/v1/workspaces/1/subscribers/1/segments HTTP/1.1
Host: sendportal.local
Authorization: Bearer GbvZ6u0UJU7EE2thKTgj1mMH7yaCm23JKRomIpkiIuZ7kfWLlVBqraAldz7Fxezw3B2M45NFL2OUm5ev
Accept: application/json
Content-Type: application/json

{
	"segments": [1, 2]
}
```

#### Sample Response

```json
{
    "data": [
        {
            "id": 1,
            "name": "Test Segment",
            "created_at": "2020-03-23 12:44:14",
            "update_at": "2020-03-23 12:44:14"
        },
        {
            "id": 2,
            "name": "Test Segment Two",
            "created_at": "2020-03-24 08:45:55",
            "update_at": "2020-03-24 08:57:21"
        }
    ]
}
```

## Delete

### Usage

Removes the provided segments from the subscriber.

#### Endpoint

`DELETE /api/v1/workspaces/{workspaceId}/subscribers/{subscriberId}/segments`

#### Expected Response Code
200

#### Request Fields

- segments: `array<int>`

#### Response Fields

- data: `array<object>`
    - id: `int`
    - name: `string`
    - created_at: `datetime`
    - updated_at: `datetime`

#### Sample Request

```
DELETE /api/v1/workspaces/1/subscribers/1/segments HTTP/1.1
Host: sendportal.local
Authorization: Bearer GbvZ6u0UJU7EE2thKTgj1mMH7yaCm23JKRomIpkiIuZ7kfWLlVBqraAldz7Fxezw3B2M45NFL2OUm5ev
Accept: application/json
Content-Type: application/json

{
	"segments": [2]
}
```

#### Sample Response

```json
{
    "data": [
        {
            "id": 1,
            "name": "Test Segment",
            "created_at": "2020-03-23 12:44:14",
            "update_at": "2020-03-23 12:44:14"
        }
    ]
}
```
