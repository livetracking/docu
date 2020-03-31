# Request Password Reset

## [POST] /resetting

### Parameters

Username or Email

* q

**Examples:**

```
 curl --data "q=TEST" https://your-domain.local/resetting
 curl --data "q=test@localhost.local"  https://your-domain.local/resetting
```

### Response

**OK:**

* status
  * OK

**Errors:**

* errors
  * INVALIDATE_USERNAME
  * INVALIDATE_EMAIL
  * EMAIL_NOT_VERIFIED
  * USERNAME_NOT_FOUND
  * EMAIL_NOT_FOUND