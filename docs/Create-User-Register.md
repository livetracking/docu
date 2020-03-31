# Create New User

## [POST] /register

### Parameters

* username
* email
* password

**Example:**

```
 curl --data "username=TEST" \
      --data "email=test@localhost.local" \
      --data "password=test1234" https://your-domain.local/register
```

### Response

**OK:**

* status
  * OK
* username
  * _Username_
* id
  * _User-ID_

Example:

```
{
  "status": "OK",
  "id": "9",
  "username": "test"
}
```

**Errors:**

* errors
  * IP_TEMP_BLOCKED
  * USERNAME_DOUBLE
  * INVALIDATE_USERNAME
  * INVALIDATE_PASSWORD
  * INVALIDATE_EMAIL

Example:

```
{
  "errors": [
    "USERNAME_DOUBLE",
    "INVALIDATE_PASSWORD",
    "INVALIDATE_EMAIL"
  ]
}
```