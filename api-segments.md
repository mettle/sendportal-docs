# Segments

## Index

Retrieve a paginated list of all segments.

### Usage

#### Endpoint

`GET /api/v1/workspaces/{workspaceId}/segments`

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
GET /api/v1/workspaces/1/segments HTTP/1.1
Host: sendportal.local
Authorization: Bearer 9w2fN7d4F3Banyv7gihYOWJEH6MvtYyZ
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
    ],
    "links": {
        "first": "<https://sendportal.local/api/v1/workspaces/1/segments?page=1>",
        "last": "<https://sendportal.local/api/v1/workspaces/1/segments?page=1>",
        "prev": null,
        "next": null
    },
    "meta": {
        "current_page": 1,
        "from": 1,
        "last_page": 1,
        "path": "<https://sendportal.local/api/v1/workspaces/1/segments>",
        "per_page": 25,
        "to": 1,
        "total": 1
    }
}
```

## Show

Get details of a single segment.

### Usage

#### Endpoint

`GET /api/v1/workspaces/{workspaceId}/segments/{segmentId}`

#### Expected Response Code
200

#### Response Fields

- data: `object`
    - id: `int`
    - name: `string`
    - created_at `datetime`
    - updated_at `datetime`

#### Sample Request

```
GET /api/v1/workspaces/1/segments/1 HTTP/1.1
Host: sendportal.local
Authorization: Bearer 9w2fN7d4F3Banyv7gihYOWJEH6MvtYyZ
Accept: application/json
```

#### Sample Response

```json
{
    "data": {
        "id": 1,
        "name": "Test Segment",
        "created_at": "2020-03-23 12:44:14",
        "update_at": "2020-03-23 12:44:14"
    }
}
```

## Store

Create a new segment, optionally including subscribers that should be in the segment.

### Usage

#### Endpoint

`POST /api/v1/workspaces/{workspaceId}/segments`

#### Expected Response Code
201

#### Request Fields

- name: `string`
- subscribers: `array<int>` (optional)

#### Response Fields

- data: `object`
    - id: `int`
    - name: `string`
    - subscribers: `array<object>`
        - id: `int`
        - first_name: `string`
        - last_name: `string`
        - email: `string`
        - created_at: `datetime`
        - updated_at: `datetime`
    - created_at: `datetime`
    - updated_at: `datetime`

#### Sample Request

```
POST /api/workspaces/1/segments HTTP/1.1
Host: sendportal.local
Authorization: Bearer 9w2fN7d4F3Banyv7gihYOWJEH6MvtYyZ
Accept: application/json
Content-Type: application/json

{
	"name": "Test Segment Two",
	"subscribers": [1]
}
```

#### Sample Response

```json
{
    "data": {
        "id": 2,
        "name": "Test Segment Two",
        "subscribers": [
            {
                "id": 1,
                "first_name": "Test",
                "last_name": "Subscriber",
                "email": "testsubscriber@example.com",
                "created_at": "2020-03-23 13:44:09",
                "updated_at": "2020-03-23 13:44:09"
            }
        ],
        "created_at": "2020-03-24 08:45:55",
        "update_at": "2020-03-24 08:45:55"
    }
}
```

## Update

Update the details of the given segment. If you wish to adjust the subscribers associated with the segment, see the Segment Subscribers API.

### Usage

#### Endpoint

`PUT /api/v1/workspaces/{workspaceId}/segments/{segmentId}`

#### Expected Response Code
200

#### Request Fields

- name: `string`

#### Response Fields

- data: `object`
    - id: `int`
    - name: `string`
    - created_at `datetime`
    - updated_at `datetime`

#### Sample Request

```
PUT /api/v1/workspaces/1/segments/2 HTTP/1.1
Host: sendportal.local
Authorization: Bearer 9w2fN7d4F3Banyv7gihYOWJEH6MvtYyZ
Accept: application/json
Content-Type: application/json

{
	"name": "Updated Segment"
}
```

#### Sample Response

```json
{
    "data": {
        "id": 2,
        "name": "Updated Segment",
        "created_at": "2020-03-24 08:45:55",
        "update_at": "2020-03-24 08:57:21"
    }
}
```

## Delete

Delete the given segment.

#### Endpoint

`DELETE /api/v1/workspaces/{workspaceId}/segments/{segmentId}`

#### Expected Response Code
204

#### Sample Request

```
DELETE /api/v1/workspaces/1/segments/2 HTTP/1.1
Host: sendportal.local
Authorization: Bearer 9w2fN7d4F3Banyv7gihYOWJEH6MvtYyZ
Accept: application/json
```
