# Change Password

## [POST] /user/change-password

### Parameters

* password
* new_password

**Example:**

```
 curl -u blafa:test1234 \
     --data "password=test1234" \
     --data "new_password=TEST1234" \
     "https://your-domain.local/user/change-password"
```

### Response

**OK:**

* status
  * OK

**Errors:**

* errors
  * INVALIDATE_PASSWORD
  * INVALIDATE_NEW_PASSWORD