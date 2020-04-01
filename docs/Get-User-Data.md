# Get User Data

## [GET] /user[/{username}]

**Examples:**

Current user (own user):

```
curl -u test:test1234 "https://your-domain.local/user"
```

Other user:

```
curl -u test:test1234 "https://your-domain.local/user/nils"
```

### Response

**OK:**

* user
  * id
  * username

**Errors:**

* errors
  * USERNAME_NOT_FOUND
  * INVALIDATE_USERNAME