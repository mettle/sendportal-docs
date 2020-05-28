# Workspaces

## Index

Retrieve a paginated list of all workspaces the API user is a member of.

### Usage

#### Endpoint

`GET /api/v1/workspaces`

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
GET /api/v1/workspaces HTTP/1.1
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
            "name": "Test Workspace",
            "created_at": "2020-03-23 13:44:09",
            "updated_at": "2020-03-23 13:44:09"
        }
    ],
    "links": {
        "first": "<https://sendportal.local/api/v1/workspaces?page=1>",
        "last": "<https://sendportal.local/api/v1/workspaces?page=1>",
        "prev": null,
        "next": null
    },
    "meta": {
        "current_page": 1,
        "from": 1,
        "last_page": 1,
        "path": "<https://sendportal.local/api/v1/workspaces>",
        "per_page": 25,
        "to": 1,
        "total": 1
    }
}
```
