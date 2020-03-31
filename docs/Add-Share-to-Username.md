# Add Share to Username (Grant Read Access)

## [PUT] /user/{username}/share

**Example:**

```
curl -u test:test1234 -X PUT "https://your-domain.local/user/nils/share"
```

### Response

**OK:**

* status
  * OK

**Errors:**

* errors
  * SELF_TALK
  * INVALIDATE_USERNAME
  * USERNAME_NOT_FOUND