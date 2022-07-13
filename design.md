## Design

### Signup
POST request to `short.ly/auth/signup`

```json
{
  "username": USERNAME,
  "password": PASSWORD
}
```
#### Logic
```
If user exists in db:
    return Error message: User already exists
If user doesn't exist in db:
    generate a new auth token
    store user, password, auth token, auth token timestamp in db
    return auth token and time till auth token is valid
```
### Login
POST request to `short.ly/auth/login`

```json
{
  "username": USERNAME,
  "password": PASSWORD
}
```
#### Logic
```
If user exists in db:
    generate a new auth token
    store auth_token, auth_token_valid_timestamp in db
    return auth_token and time till auth token is valid
If user doesn't exist in db:
    Return error: User doesn't exist
```

### Logout
DELETE request to `short.ly/auth/logout`

```json
{
  "username": USERNAME,
  "password": PASSWORD
}
```
#### Logic
```
If user exists in db:
    change auth_token_valid_timestamp to current time
If user doesn't exist in db:
    Return error: User doesn't exist
```
### Shorten new URL
POST request to `short.ly/url/shorten/`

pass AUTH_TOKEN in Authorization header

```json
{
  "url": URL_TO_SHORTEN,
  "key": CUSTOM_KEY,
  "passowrd": PASSWORD
}
```
#### Logic
```
if URL_TO_SHORTEN exists in db:
    return error
if URL_TO_SHORTEN doesn't exist in db:
    if CUSTOM_KEY is already taken:
        return error
    if CUSTOM_KEY isn't taken or key isn't specified:
        make new db entry with url, key(random if not specified) and password

Make new route, set url to short.ly/CUSTOM_KEY
    if PASSWORD is None
        redirect user to URL_TO_SHORTEN
    if PASSWORD is set
        return index.html which sends post request to validate password endpoint.
        ask them to enter password
        If correct password:
            redirect to URL_TO_SHORTEN
        if incorrect password:
            Empty password field and ask again
            
```