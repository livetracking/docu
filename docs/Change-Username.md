# Change Username

If the username is changed, all granted and received permissions are deleted!

## [POST] /user/change-username

### Parameters

* username
* password

**Example:**

```
curl -u blafa:test1234 \
     --data "username=bla_fa" \
     --data "password=test1234" \
     "https://your-domain.local/user/change-username"
```

### Response

**OK:**

* status
  * OK

**Errors:**

* errors
  * USERNAME_DOUBLE
  * INVALIDATE_USERNAME
  * INVALIDATE_PASSWORD
