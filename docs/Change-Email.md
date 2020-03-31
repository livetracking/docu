# Change Email

## [POST] /user/change-email

### Parameters

* email
* password

**Example:**

```
 curl -u blafa:test1234 \
     --data "password=test1234" \
     --data "email=new@localhost.local" \
     "https://your-domain.local/user/change-email"
```

### Response

**OK:**

* status
  * OK

**Errors:**

* errors
  * INVALIDATE_PASSWORD
  * INVALIDATE_EMAIL