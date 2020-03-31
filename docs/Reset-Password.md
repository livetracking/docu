# Reset Password

## [GET] /resetting/{password_reset_token}

**Example:**

```
 curl https://your-domain.local/resetting/<TOKEN>
```

### Response

**OK:**

* status
  * OK

**Errors:**

* errors
  * TOKEN_NOT_FOUND
  * INVALIDATE_TOKEN