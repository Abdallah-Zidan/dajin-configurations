# Social Login Guide
*Last updated at : 17-4-2022*

## 1. Login
### This request is performed in case user decided to login using one of the available social login options

#### URL :  /api/v1/social/login
#### Method: POST
#### Headers: 
    - Content-Type: application/json
    - platform: "WEB" or "ANDROID" or "IOS",
    - accept: application/json
#### Body:
    - type: 1 (google) or 2 (facebook) or 3  (apple)
    - token: <Access token retreived from OAuth>

#### Response
    A. Created with status code 201 
        - Token is valid and user exists and linked with the target social platform
        - Response will be a normal login response exactly as normal login

    B. Ok with status code 200
        - Token is valid but user doesn't exist or not linked with the target social platform
        - Response will contain the user info retreived from social platform [name,email,sub, picture (optional)]
        - In that case user can continue registeration and provide access token again in registration request in order to link him with the target social platform


#### Errors 
    A. Validation error with status code 422

    B. Bad Request error
        - BadRequestError with status code 400 
        - Message: invalid token message or unsupported login type
---
## 2. Registration with social linking
### This request is performed when user try to login using social login and the token is valid but he doesn't have a linked account with that social platform
#### URL :  /api/v1/register
#### Method: POST
#### Headers: 
    - Content-Type: application/json
    - platform: "WEB" or "ANDROID" or "IOS",
    - accept: application/json    
#### Body:
    - <Normal registration body>
    - google_token: <Access token retreived from google> 
        or
    - facebook_token: <Access token retreived from facebook>
        or
    - apple_token: <Access token retreived from apple>

#### Response
    - Created with status code 201 
        - Token is valid and user was created and linked with the target social platform
        - Response will be a normal registration response exactly as normal registration
    * Note: if token isn't valid it will be ignored and no linking will happen
---
## 2. Link
### This request is performed when user try to link his account with one of the supported social platforms
#### URL :  /api/v1/social/link
#### Method: PUT | PATCH
#### Headers: 
    - Content-Type: application/json
    - platform: "WEB" or "ANDROID" or "IOS",
    - accept: application/json
    - Authoriation: Bearer <dajin_token>  

#### Body:
    - type: 1 (google) or 2 (facebook) or 3  (apple)
    - token: <Access token retreived from OAuth>

#### Response
    - Accepted with status code 202

#### Errors 
    A. Validation error with status code 422

    B. Bad Request error
        - BadRequestError with status code 400 
        - Message: invalid token message or unsupported login type

    C. UnAuthenticated with status code 401 when user isn't authenticated
        - Message: UnAuthenticated
---
## 3. Unlink
### This request is performed when user wants to unlink his account from a social platform
#### URL :  /api/v1/social/unlink
#### Method: DELETE

#### Body:
    - type: 1 (google) or 2 (facebook) or 3  (apple)

#### Response
    - NoContent with status code 204

#### Errors 
    A. Validation error with status code 422

    B. Bad Request error
        - BadRequestError with status code 400 
        - Message: invalid token message or unsupported login type

    C. UnAuthenticated with status code 401 when user isn't authenticated
        - Message: UnAuthenticated

---
## General Notes:
#### User data retrieved from backend will have the following parameters returned with it.

    a. google_user_id => if null means that user account isn't linked with google
    b. facebook_user_id =>  if null means that user account isn't linked with facebook
    c. apple_user_id => if null means that user account isn't linked with apple
