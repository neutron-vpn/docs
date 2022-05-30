# Endpoints

## /
### Description
/ is an root endpoints which returns API version and available endpoints.
### Arguments
It takes no arguments.
### Call example
HTTPX:
```
$ httpx https://api_address
```
### Output
```
{
    "status": "OK",
    "version": "1.0",
    "routes": [
        "/",
        "/user/register",
        "/user/getAccessToken",
        "/endpoint/test"
    ]
}
```
## /user/register
### Description
/user/register is an endpoint which is used to register new users.
### Arguments
It takes arguments `username` and `password` in JSON format.
### Call example
HTTPX:
```
$ httpx https://api_address/user/register -j '{"username": "example", "password": "example"}'
```
### Output
Success:
```
{
    "status": "OK",
    "message": "User successfuly created",
    "code": "user_created",
    "id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
```
Fail (conflict):
```
{
    "status": "ERR",
    "message": "Username already in use",
    "code": "conflict"
}
```

## /user/getAccessToken
### Description
/user/getAccesToken is an endpoint which generates and returns an access token which expires in 600s (30m)
### Arguments
It takes arguments `id` and `password` in JSON format.
### Call example
HTTPX:
```
$ httpx https://api_address/user/getAccessToken -j '{"id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "password": "example"}'
```
### Output
Success:
```
{
    "status": "OK",
    "message": "Access token sent",
    "expiresIn": 600,
    "code": "access_token_sent",
    "token": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```
Fail (wrong credentials):
```
{
    "status": "ERR",
    "message": "You specified wrong credentials",
    "code": "wrong_creds"
}
```

## /endpoint/test
### Description
/endpoint/test is an endpoint used for auth testing.
### Arguments
It takes token in headers
### Call example
HTTPX:
```
$ httpx https://api_address/endpoint/test -h Authorization 'Bearer TOKEN'
```
### Output
Success: 
```
{
    "status": "OK",
    "message": "Authorization working!",
    "code": "test_sucess"
}
```
Fail (expired token or wrong token):
```
{
    "status": "ERR",
    "message": "Wrong or expired token",
    "code": "wrong_expired_token"
}
```












