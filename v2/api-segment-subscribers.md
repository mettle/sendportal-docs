# Segment Subscribers

## Index

Retrieve a list of the subscribers in the segment.

### Usage

#### Endpoint

`GET /api/v1/workspaces/{workspaceId}/segments/{segmentId}/subscribers`

#### Expected Response Code
200

#### Response Fields

- data: `array<object>`
    - id: `int`
    - first_name: `string`
    - last_name: `string`
    - email: `string`
    - created_at: `datetime`
    - updated_at: `datetime`

#### Sample Request

```
GET /api/v1/workspaces/1/segments/1/subscribers HTTP/1.1
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
            "created_at": "2020-03-23 13:44:09",
            "updated_at": "2020-03-23 13:44:09"
        }
    ]
}
```

## Store

Adds a list of subscribers to the given segment. Returns a list of the subscribers that are in the segment.

This endpoint is idempotent, meaning that subscribers already added to the segment will not be continuously added to the segment on repeated requests to this endpoint. However, if the intention is to supply a full list of subscribers that should be in the segment, the Update endpoint should be used instead.

#### Endpoint

`POST /api/v1/workspaces/{workspaceId}/segments/{segmentId}/subscribers`

#### Expected Response Code
200

#### Request Fields

- subscribers: `array<int>`

#### Response Fields

- data: `array<object>`
    - id: `int`
    - first_name: `string`
    - last_name: `string`
    - email: `string`
    - created_at: `datetime`
    - updated_at: `datetime`

#### Sample Request

```
POST /api/v1/workspaces/1/segments/1/subscribers HTTP/1.1
Host: sendportal.local
Authorization: Bearer GbvZ6u0UJU7EE2thKTgj1mMH7yaCm23JKRomIpkiIuZ7kfWLlVBqraAldz7Fxezw3B2M45NFL2OUm5ev
Accept: application/json
Content-Type: application/json

{
	"subscribers": [1, 2]
}
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
            "created_at": "2020-03-23 13:44:09",
            "updated_at": "2020-03-23 13:44:09"
        },
        {
            "id": 2,
            "first_name": "Test",
            "last_name": "Subscriber Two",
            "email": "testsubscriber2@example.com",
            "created_at": "2020-03-23 13:50:39",
            "updated_at": "2020-03-23 13:50:39"
        }
    ]
}
```

## Update

Replaces the list of subscribers in a given segment with the one supplied in the request.

If you want to add additional subscribers to the segment without removing existing ones, you should use the Store endpoint. If you want to remove specific subscribers from the segment, you should use the Delete endpoint.

#### Endpoint

`PUT /api/v1/workspaces/{workspaceId}/segments/{segmentId}/subscribers`

#### Expected Response Code
200

#### Request Fields

- subscribers: `array<int>`

#### Response Fields

- data: `array<object>`
    - id: `int`
    - first_name: `string`
    - last_name: `string`
    - email: `string`
    - created_at: `datetime`
    - updated_at: `datetime`

#### Sample Request

```
PUT /api/v1/workspaces/1/segments/1/subscribers HTTP/1.1
Host: sendportal.local
Authorization: Bearer GbvZ6u0UJU7EE2thKTgj1mMH7yaCm23JKRomIpkiIuZ7kfWLlVBqraAldz7Fxezw3B2M45NFL2OUm5ev
Accept: application/json
Content-Type: application/json

{
	"subscribers": [1, 2]
}
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
            "created_at": "2020-03-23 13:44:09",
            "updated_at": "2020-03-23 13:44:09"
        },
        {
            "id": 2,
            "first_name": "Test",
            "last_name": "Subscriber Two",
            "email": "testsubscriber2@example.com",
            "created_at": "2020-03-23 13:50:39",
            "updated_at": "2020-03-23 13:50:39"
        }
    ]
}
```

## Delete

Removes the provided subscribers from the segment.

#### Endpoint

`DELETE /api/v1/workspaces/{workspaceId}/segments/{segmentId}/subscribers`

#### Expected Response Code
200

#### Request Fields

- subscribers: `array<int>`

#### Response Fields

- data: `array<object>`
    - id: `int`
    - first_name: `string`
    - last_name: `string`
    - email: `string`
    - created_at: `datetime`
    - updated_at: `datetime`

#### Sample Request

```
DELETE /api/v1/workspaces/1/segments/1/subscribers HTTP/1.1
Host: sendportal.local
Authorization: Bearer GbvZ6u0UJU7EE2thKTgj1mMH7yaCm23JKRomIpkiIuZ7kfWLlVBqraAldz7Fxezw3B2M45NFL2OUm5ev
Accept: application/json
Content-Type: application/json

{
	"subscribers": [2]
}
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
            "created_at": "2020-03-23 13:44:09",
            "updated_at": "2020-03-23 13:44:09"
        }
    ]
}
```
