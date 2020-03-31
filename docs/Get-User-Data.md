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
  * email _(Only for own user)_
* shares
  * to
    * _Usernames_
  * from
    * _Usernames_

**Errors:**

* errors
  * USERNAME_NOT_FOUND
  * INVALIDATE_USERNAME