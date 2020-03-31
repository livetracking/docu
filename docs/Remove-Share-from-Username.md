# Remove Share from Username (Remove Read Permission)

## [DELETE] /user/{username}/share

**Example:**

```
curl -u test:test1234 -X DELETE "https://your-domain.local/user/nils/share"
```

### Response

**OK:**

* status
  * OK

**Errors:**

* errors
  * SELF_TALK
  * USERNAME_NOT_FOUND
  * INVALIDATE_USERNAME