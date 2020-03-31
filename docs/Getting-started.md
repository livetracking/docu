# API

This describes the resources that make up the Live Tracking HTTP API.

## Schema

All API access is over HTTPS, and accessed from the `https://your-domain.local`. All data is sent as JSON.

If you installed the back end software on your own server, of course, the URL changes.

## Parameters

Many API methods take parameters. Which parameters are expected exactly will be described in detail:

New User:

* [Create User (Register)](Create-User-Register.md)
* [Email Address Verification](Email-Address-Verification.md)

User Data:

* [Get User Data](Get-User-Data.md)
* [Search Users](Search-Users.md)

Edit User:

* [Change Username](Change-Username.md)
* [Change Password](Change-Password.md)
* [Change Email](Change-Email.md)
* [Delete User](Delete-User.md)

Share:

* [Add Share to Username (Grant Read Access)](Add-Share-to-Username.md)
* [Remove Share from Username (Remove Read Permission)](Remove-Share-from-Username.md)

Live Tracking:

* [Writing Data](Writing-Data.md)
* [Querying Data](Querying-Data.md)

## Authentication

There is only one way to authenticate through livetracking.io API:

* **HTTP Basic authentication (BA)**

You can find more details in [Wikipedia](https://en.wikipedia.org/wiki/Basic_access_authentication).

Requests that require authentication will return `401 Unauthorized`. If the login failed `403 Forbidden` is returned.

Without username and password:

```
curl -i https://your-domain.local/user
HTTP/1.1 401 Unauthorized

{
  "error": "AUTHENTICATION_FAILED"
}
```

With username and password:

```
curl -i https://your-domain.local/user -u foo:bar12345
HTTP/1.1 403 Forbidden

{
  "error": "AUTHENTICATION_FAILED"
}
```

## OK

If your request received HTTP status code `200` or `204`, it was a success!

## Errors

There are three possible types of errors on API calls. Each type of error has its own HTTP status code. Depending on the type of error, further details are output.

**HTTP Status Code:**

* `400`, `404` and `405`: Client error
* `401` and `403`: Authentication error
* `500`: The system is overloaded or significantly impaired

For status code `400`, object `errors` is return with an array of error codes.

```
curl --data "username=test" https://your-domain.local/register
HTTP/1.1 400 Bad Request

{
  "errors": [
    "INVALIDATE_PASSWORD",
    "INVALIDATE_EMAIL"
  ]
}
```


**Error Codes (Detail):**

* `IP_TEMP_BLOCKED`: IP address temporarily blocked. Please try again in two hours.
* `USERNAME_DOUBLE`: The username is already used.
* `INVALIDATE_USERNAME`: The username is not valid. It must be at least 4 characters and can be up to 20 characters long. It can only contain characters (a-z) and numbers.
* `INVALIDATE_PASSWORD`: The entered password is invalid. The password must be at least 8 characters long.
* `INVALIDATE_NEW_PASSWORD`: The entered new password is invalid. The password must be at least 8 characters long.'
* `INVALIDATE_EMAIL`: The email is not valid.
* `INVALIDATE_TOKEN`: Invalid token.
* `EMAIL_NOT_VERIFIED`: Email address is not verified. No delivery to this email address possible.
* `USERNAME_NOT_FOUND`: Username could not be found.
* `EMAIL_NOT_FOUND`: Email address could not be found.
* `TOKEN_NOT_FOUND`: No token could be found.
* `SELF_TALK`: Self talk?
* `FORBIDDEN`: The entered password is not correct.

## Cross Origin Resource Sharing

The API supports Cross Origin Resource Sharing (CORS) for AJAX requests from any origin. You can read the [CORS W3C Recommendation](https://www.w3.org/TR/cors/), or this [Wikipedia article](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).

