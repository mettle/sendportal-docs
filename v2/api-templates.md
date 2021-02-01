# Templates

## Index

Retrieve a paginated list of all templates.

### Usage

#### Endpoint

`GET /api/v1/workspaces/{workspaceId}/templates`

#### Expected Response Code
200

#### Response Fields

- data: `array<object>`
  - id: `int`
  - name: `string`
  - content: `string`
  - created_at: `datetime`
  - updated_at: `datetime`

#### Sample Request

```
GET /api/v1/workspaces/1/templates HTTP/1.1
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
            "name": "Template Name",
            "content": "Template Content",
            "created_at": "2020-07-17 09:48:07",
            "updated_at": "2020-07-17 09:48:07"
        }
    ],
    "links": {
        "first": "http://sendportal.test/api/v1/workspaces/1/templates?page=1",
        "last": "http://sendportal.test/api/v1/workspaces/1/templates?page=1",
        "prev": null,
        "next": null
    },
    "meta": {
        "current_page": 1,
        "from": 1,
        "last_page": 1,
        "path": "http://sendportal.test/api/v1/workspaces/1/templates",
        "per_page": 25,
        "to": 1,
        "total": 1
    }
}
```

## Show

Retrieve the details of a single template.

### Usage

#### Endpoint

`GET /api/v1/workspaces/{workspaceId}/templates/{templateId}`

#### Expected Response Code
200

#### Response Fields

- data: `object`
  - id: `int`
  - name: `string`
  - content: `string`
  - created_at: `datetime`
  - updated_at: `datetime`

#### Sample Request

```
GET /api/v1/workspaces/1/templates/1 HTTP/1.1
Host: sendportal.local
Authorization: Bearer 9w2fN7d4F3Banyv7gihYOWJEH6MvtYyZ
Accept: application/json
```

#### Sample Response

```json
{
    "data": {
        "id": 1,
        "name": "Template Name",
        "content": "Template Content",
        "created_at": "2020-07-17 09:48:07",
        "updated_at": "2020-07-17 09:48:07"
    }
}
```

## Store

Create a new template.

### Usage

#### Endpoint

`POST /api/v1/workspaces/{workspaceId}/templates`

#### Expected Response Code
201

#### Request Fields

- name: `string`
- content: `string`

#### Response Fields

- data: `object`
  - id: `int`
  - name: `string`
  - content: `string`
  - created_at: `datetime`
  - updated_at: `datetime`

#### Sample Request

```
POST /api/v1/workspaces/1/templates HTTP/1.1
Host: sendportal.local
Authorization: Bearer 9w2fN7d4F3Banyv7gihYOWJEH6MvtYyZ
Accept: application/json
Content-Type: application/json

{
	"name": "Test Template",
	"content": "Test Content"
}
```

#### Sample Response

```json
{
    "data": {
        "id": 3,
        "name": "Test Template",
        "content": "Test Content",
        "created_at": "2020-07-17 09:55:10",
        "updated_at": "2020-07-17 09:55:10"
    }
}
```

## Update

#### Endpoint

`PUT /api/v1/workspaces/{workspaceId}/templates/{templateId}`

#### Expected Response Code
200

#### Description
Update the details of the given template.

#### Request Fields

- name: `string`
- content: `string`

#### Response Fields

- data: `object`
  - id: `int`
  - name: `string`
  - content: `string`
  - created_at: `datetime`
  - updated_at: `datetime`

#### Sample Request

```
PUT /api/v1/workspaces/1/templates/3 HTTP/1.1
Host: sendportal.local
Authorization: Bearer 9w2fN7d4F3Banyv7gihYOWJEH6MvtYyZ
Accept: application/json
Content-Type: application/json

{
	"name": "Test Template",
	"content": "Content"
}
```

#### Sample Response

```json
{
    "data": {
        "id": 3,
        "name": "Test Template",
        "content": "Content",
        "created_at": "2020-07-17 09:55:10",
        "updated_at": "2020-07-17 09:57:07"
    }
}
```

## Delete

Delete the given template.

### Usage

#### Endpoint

`DELETE /api/v1/workspaces/{workspaceId}/templates/{templateId}`

#### Expected Response Code
204

#### Sample Request

```
DELETE /api/v1/workspaces/1/templates/3 HTTP/1.1
Host: sendportal.local
Authorization: Bearer 9w2fN7d4F3Banyv7gihYOWJEH6MvtYyZ
Accept: application/json
```
