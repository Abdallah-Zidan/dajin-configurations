# 1. Success

## Created 
### successful resource creation
    - status code: 201
    - data: created resource data

## Accepted
###    Successful resource update/patch
    - status code: 202
    - data: updated resource data

## NoContent
###   Successful resource deletion
    - status code: 204
    - data: null

## Ok
### Successful resource retreival
    - status code: 200
    - data : requested resource data

# 2. Errors

## NotFound
### Requested resource or endpoint doesn't exist
    - status code: 404
    - data : null

## Forbidden
### Logged in user can't access the requested resource
    - status code: 403
    - data: null
    - message: optional message without leaking info 

## Duplicate
### Requested action has been already executed and can't be re-excuted
    - status code: 409
    - data: null
    - message: a message describing what happened

## TooManyRequests
### Client exceeded the number of requests allowed in a period of time in general or for specific endpoint
    - status code: 429
    - data : null
    - message: optional message explaining why request was rejected

## Method Not Allowed
### Request method isn't supported for the target resource
    - status code: 405
    - data: null

## UnProcessableEntity
### The data received from the client didn't pass the validation rules
    - status code: 422
    - data : null
    - message: The given data was invalid.
    - errors : key-value pair of each invalid attribute and its validation errors as an array of strings
    example:
        "errors": {
            "email": [
                "البريد الإلكترونى مستخدم من قبل"
            ],
            "daily_loading_capacity": [
                "سعة التحميل التقريبية مطلوبة."
            ]
        }

## BadRequest
### Request is invalid 
    - status code: 400
    - data: null
    - message: a message describing why the request is considered invalid

## UnAuthenticated / UnAuthorized
### Trying to access a protected resource with unauthenticated user or with expired session/token
    - status code: 401
    - data: null
    - message: UnAuthenticated
* Note : User shouldbe redirected to login page

## CSRF Token mismatch
### invalid csrf token header (stateful origins only) 
    - status code: 419
    - data: null
    - message: CSRF token mismatch
* Note: Ensure hitting csrf-cookie endpoint and appending the header with the request 


# 3.Server errors 
### all errors with status code 50x are considered server side errors 

## Internal Server Error 
### An exception happened in the server while processing the incoming request
    - status code: 500
    - data: null


## Bad Gateway
### In case of using proxy or a gateway in front of the api server and the gateway can receive the request but the api server isn't reachable
    - status code: 502
    - data: null


## Service UnAvailable
### Server is loaded and can't handle more requests
    - status code: 503
    - data: null








