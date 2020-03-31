# Delete User

Delete the user and all its data.

## [DELETE] /user

### Parameters

* password

**Example:**

```
curl -u test:test1234 -X DELETE \
     --data "password=test1234" \
     "https://your-domain.local/user"
```

### Response

**OK:**

* status
  * OK

**Errors:**

* errors
  * INVALIDATE_PASSWORD