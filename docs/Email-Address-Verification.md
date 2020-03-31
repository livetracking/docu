# Email Address Verification

## [GET] /validateemail/{email_verification_token}

**Example:**

```
curl https://your-domain.local/validateemail/<TOKEN>
```

### Response

**OK:**

* status
  * OK

**Errors:**

* errors
  * TOKEN_NOT_FOUND
  * INVALIDATE_TOKEN