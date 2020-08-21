# Introduction

## Request Requirements

When making a request, the following requirements must be met.

### Headers

The following headers are required. Failure to supply these headers may lead to the API behaving in unexpected ways.

#### Accept
An `Accept` header should be provided, with the value `application/json`.

#### Content-Type
A `Content-Type` header should be supplied with the value `application/json`.

## Authentication

Authentication for the API is performed on a per-user basis by supplying a token with the API request.

### Bearer Token

The preferred way to authenticate with the API during a request is to use the user’s token as a Bearer token. This is done by supplying an `Authorization` header with the request, where the value is `Bearer {api_token}`.

The token is available from the logged in user's profile.

#### Example

```
Authorization: Bearer GbvZ6u0UJU7EE2thKTgj1mMH7yaCm23JKRomIpkiIuZ7kfWLlVBqraAldz7Fxezw3B2M45NFL2OUm5ev
```

### API Token Parameter

Alternatively, you can authenticate by providing the token as a parameter when making the request. The token parameter should be keyed as `api_token` where the value is `{api_token}`.

#### GET Example

```
/api/v1/ping?api_token=GbvZ6u0UJU7EE2thKTgj1mMH7yaCm23JKRomIpkiIuZ7kfWLlVBqraAldz7Fxezw3B2M45NFL2OUm5ev
```

#### POST Example

```
{
    "api_token": "GbvZ6u0UJU7EE2thKTgj1mMH7yaCm23JKRomIpkiIuZ7kfWLlVBqraAldz7Fxezw3B2M45NFL2OUm5ev"
}
```

## Throttling

By default, the API is configured to limit requests to 60 per minute. When this limit is exceeded a `429 Too Many Requests` response will be returned.

The limit can be configured by editing the `SENDPORTAL_THROTTLE_MIDDLEWARE` key in the`.env` file. The value needs to be in the format `{number_of_requests},{every_X_minutes}`.

For example, this would limit the API to 1000 requests every 5 minutes:

```markdown
SENDPORTAL_THROTTLE_MIDDLEWARE=1000,5
```

For more information on rate limiting see the official Laravel documentation [here](https://laravel.com/docs/master/routing#rate-limiting).

## Testing the API

You can easily and quickly test your API by performing a `GET` request against the `/ping` endpoint:

`GET /api/v1/ping`

If your API is working correctly, then this will return a `200` response with the string `ok` in the body content. Note that this endpoint does not require any authentication.

## Errors

### Authentication Error

An authentication error can occur when no token is provided, or the token is invalid.

#### Response Fields

- message: `string`

#### Sample Missing Token Response

```
{
    "message": "Unauthenticated."
}
```

#### Sample Invalid Token Response

```
{
    "message": "Unauthenticated."
}
```

## Validation Errors

When data provided in a request is invalid or missing you will receive an error response explaining what is wrong with the request.

#### Response Fields

- message: `string`
- errors: `object`

#### Sample Response

```
{
    "message": "The given data was invalid.",
    "errors": {
        "email": [
            "The email field is required."
        ]
    }
}
```

## Pagination

Paginated responses follow this format:

- data: `array<object>`
    - id: `int`
    - name: `string`
    - created_at: `datetime`
    - updated_at: `datetime`
- links: `object`
    - first: `string`
    - last: `string`
    - prev: `string|null`
    - next: `string|null`
- meta: `object`
    - current_page: `int`
    - from: `int`
    - last_page: `int`
    - path: `string`
    - per_page: `int`
    - to: `int`
    - total: `int`
