# Create New User

## [POST] /register

### Parameters

* username
* email
* password

**Example:**

```
 curl --data "username=TEST" \
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
  * USERNAME_DOUBLE
  * INVALIDATE_USERNAME
  * INVALIDATE_PASSWORD

Example:

```
{
  "errors": [
    "USERNAME_DOUBLE",
    "INVALIDATE_PASSWORD"
  ]
}
```