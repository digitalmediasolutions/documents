# digitalmediasolutions/documents
## Introduction
The point of the project is to manage the sending of emails. See  [https://github.com/digitalmediasolutions/documents/tree/main/o2o-caas](https://github.com/digitalmediasolutions/documents/tree/main/o2o-caas)  for more information.

## Pre-requisites
Node.j v14+ and running instances of a MongoDB and Redis server are required for the app to start. The **MongoDB** is used for the rest of the models in the app.

## Installation
Do the following to clone and start the project.
```
>$ git clone https://github.com/digitalmediasolutions/documents.git``
>$ cd documents``
>$ npm i``
>$ npm start``
```
## Models
This app has the following models:
```
1.  `Users`  - representing the users of the system.
2.  `EmailTemplates`  - a model to represent the email request template.
3.  `EmailDistributions`  - a model to represent the records from SendGrid after sending emails.
```

## Controllers

Controllers expose API endpoints for interacting with the models and more.

In this app, there are three controllers:
```
1.  `user`  - controller for creating user, fetching user info, updating user info and deleting user info.
2.  `template`  - controller for creating email templates, fetching email templates info, updating email templates info and deleting email templates info.
3.  `app`  - controller for sending, updating, deleting account emails.
```
## Services

### Authentication

Endpoint authorization is done using **@loopback/express**.

This package adds middleware support for LoopBack 4 and allows Express middleware to be plugged into LoopBack seamlessly. It's used by @loopback/rest to support Express middleware with InvokeMiddleware action within the REST sequence.

Some controller methods without the authorization will be accessible to everyone.

To use this package, you'll need to install `@loopback/express`.
>``npm i @loopback/express``

### Adding JSON Web Tokens

In this section, we will demonstrate how `jwt` was added to the application using the [JSON Web Tokens](https://tools.ietf.org/html/rfc7519) approach.

### Installing @loopback/authentication-jwt
The application  **already**  has the`@loopback/authentication-jwt`  dependency set up in its  **package.json**

It was installed as a project dependency by performing:

>1.  `npm install jsonwebtoken`

### Endpoints with refresh token

This application has refresh token mechanism.

1.  `To generate refresh token`  : to generate the refresh token and access token when user logins to app with provided credentials.

2.  `To refresh the token`: to generate the access token by the refresh token obtained from the the last login endpoint.

## Endpoints
### Account

| Parameter | Type| Required | Description| 
|----------|------|-------|--------|
| email | string | required | The email will supply you that identifies your account.|
| type | string | Required | Description| 

In the `AccountController` class in the application , a user can print out their user profile by performing a `GET` request on the`/accounts` endpoint.

The response will be displayed as follows:
``` 
{
  "type": "success",
  "message": "Account has been fetched successfully",
  "data": [
    {
      "email_service": "sendgrid",
      "_id": {{id}},
      "email": {{email}},
      "type": {{type}},
      "created_at": {{created_at}},
      "refresh_token": {{refresh_token}},
    }
  ]
}
 ```
a user can create their user profile by performing a `POST` request on the`/accounts` endpoint.
``` 
POST /api/v1/accounts HTTP/1.1
Host: http://o2o-caas-env-v1.eba-mbacrg8k.ap-southeast-1.elasticbeanstalk.com
Content-Type: application/x-www-form-urlencoded
Accept: application/json
Accept-Charset: utf-8

{
	"email" : {{email}},
	"type" : {{type}}
}
```
If successful, you will receive back an access token response:
```
HTTP/1.1 201 OK
Content-Type: application/json; charset=utf-8

{
  "type": "success",
  "message": "You have been logged in successfully",
  "data": {
  "accessToken": {{access_token}},
  "refreshToken": {{refresh_token}},
}
```
a user can update their user profile by performing a `PUT` request on the`/accounts/{id}` endpoint.

a user can delete their user profile by performing a `DELETE` request on the`/accounts/{id}` endpoint.

To acquire a new access token using a refresh token, make the following form-encoded request:
```
POST /api/v1/accounts HTTP/1.1
Host: http://o2o-caas-env-v1.eba-mbacrg8k.ap-southeast-1.elasticbeanstalk.com
Content-Type: application/x-www-form-urlencoded
Accept: application/json
Accept-Charset: utf-8

refresh_token={{refresh_token}}
```
### Email Template
| Parameter | Type| Required | Description| 
|----------|------|-------|--------|
| template| string | required | The email will supply you that identifies your account.|
| type | string | Required | Description| 
| subject| object| Required | The first text recipients see after your sender name when an email reaches their inbox | 
| content| object| Required | Any message sent to a person| 
| variables| array| Required | Description| 

In the `templateController` class in the application , a user can print out the email template by using  a `GET` request on the`/email-templates` endpoint.

The response will be displayed as follows:
```
{
	"subject": {{subject}},
	"content": {{content}},
	"variables": [],
	"_id": {{id}},
	"template": {{template}},
	"type": {{type}},
	"created_at": {{created_at}},
}
```

a user can create email template by performing a `POST` request on the`/email-templates` endpoint.
``` 
POST /api/v1/accounts HTTP/1.1
Host: http://o2o-caas-env-v1.eba-mbacrg8k.ap-southeast-1.elasticbeanstalk.com
Content-Type: application/x-www-form-urlencoded
Accept: application/json
Accept-Charset: utf-8

{
	"template": {{template}},
	"type": {{type}},
	"subject": {{subject}},
	"content": {{content}},
	"variables": []
}
```
a user can update email template by performing a `PUT` request on the`/email-templates/{id}` endpoint.
``` 
{
	"subject": {{subject}},
	"content": {{content}},
	"variables": [],
	"template": {{template}},
	"type": {{type}},
}
```
a user can delete email template by performing a `DELETE` request on the`/email-templates/{id}` endpoint.

## Resources

The API is RESTful and arranged around resources. Some requests must be made with an integration token.

Typically, the first request you make should be to acquire user details. This will confirm that your access token is valid, and give you a user id that you will need for subsequent requests.

Possible errors:

| Error code| Description|
|----------|------|
| 400 Bad Request | the request the client made is incorrect or corrupt|
| 401 Unauthorized| the request could not be authenticated|
| 403 Forbidden| the server understands the request but refuses to authorize it|

### Users

#### Getting the authenticated user’s details

Returns details of the user who has granted permission to the application.

``` 
GET http://o2o-caas-env-v1.eba-mbacrg8k.ap-southeast-1.elasticbeanstalk.com/api/v1/me
```

Example request:

``` 
GET /api/v1 HTTP/1.1
Host: http://o2o-caas-env-v1.eba-mbacrg8k.ap-southeast-1.elasticbeanstalk.com
Authorization: Bearer
Content-Type: application/json
Accept: application/json
Accept-Charset: utf-8
```

The response is a User object within a data envelope.
``` 
{
   "type":"success",
   "message":"Account details has been fetched successfully",
   "data":{
      "account":{
         "email_service":"sendgrid",
         "email": {{email}},
         "type": {{type}},
         "created_at": {{created_at}},
         "refresh_token": {{refresh_token}},
         "smtp":null
      }
   }  
}
```

Possible errors:

| Error code| Description|
|----------|------|
| 400 Bad Request | the request the client made is incorrect or corrupt|
| 401 Unauthorized| the request could not be authenticated|
| 403 Forbidden| the server understands the request but refuses to authorize it|

### Deliverability Insights
Fetch deliverability-insights data on the authenticated user’s profile.

``` 
GET http://o2o-caas-env-v1.eba-mbacrg8k.ap-southeast-1.elasticbeanstalk.com/me/deliverability-insights
```
The response is a Get object within a data envelope. Example response:
``` 
{
	"_id": {{id}},
	"account_id": {{account_id}},
	"recipient": {{recipient}},
	"status": {{status}},
	"created_at": {{created_at}},
}
```
Possible errors:

| Error code| Description|
|----------|------|
| 400 Bad Request | the request the client made is incorrect or corrupt|
| 401 Unauthorized| the request could not be authenticated|
| 403 Forbidden| the server understands the request but refuses to authorize it|

These endpoints will perform actions on production data on `http://o2o-caas-env-v1.eba-mbacrg8k.ap-southeast-1.elasticbeanstalk.com`.
