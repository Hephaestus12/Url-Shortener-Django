# URL Shortener

## Problem Statement
Main purpose is to shorten and redirect URLs - Let’s call it short.ly

Build APIs for the following
* User signup and authentication
* Ability to shorten a new URL

Should return a new unique shortURL that will redirect to parent URL: e.g. short.ly/as21f

Each shortURL should also track how many hits it got and the last hit timestamp.

Provide ability for user to give their own shortURL keys : e.g. short.ly/ncg2022

Ability to list all shortened URLs for authenticated user.

Ability for user to delete their own shortURLs

BONUS - Support for password based shortURLs

For a shortening request, creator should be able to specify a password.

Should redirect to a custom page where the end user is prompted for a password and app should redirect only if it’s valid.

## Usage

### Signup
POST request to `short.ly/auth/signup`

```json
{
  "username": USERNAME,
  "password": PASSWORD
}
```

### Login
POST request to `short.ly/auth/login`

```json
{
  "username": USERNAME,
  "password": PASSWORD
}
```


### Logout
DELETE request to `short.ly/auth/logout`

```json
{
  "username": USERNAME,
  "password": PASSWORD
}
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


