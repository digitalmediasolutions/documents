# digitalmediasolutions/documents

The point of the project is to manage the sending of emails. See  [https://github.com/digitalmediasolutions/documents/tree/main/o2o-caas](https://github.com/digitalmediasolutions/documents/tree/main/o2o-caas)  for more information.

## Pre-requisites
Typescript and running instances of a MongoDB are required for the app to start. The **MongoDB** is used for the rest of the models in the app.

## Installation
Do the following to clone and start the project.

`
1. `$ git clone https://github.com/digitalmediasolutions/documents.git`
2. `$ cd documents`
3. `$ npm i`
4. `$ npm start``

## Models
This app has the following models:
1.  `Accounts`  - representing the accounts of the system.
2.  `EmailTemplates`  - a model to represent the email request template.
3.  `EmailDistributions`  - a model to represent the records from SendGrid after sending emails.

## Controllers

Controllers expose API endpoints for interacting with the models and more.

In this app, there are three controllers:

1.  `account`  - controller for creating account, fetching account info, updating account info and deleting account info.
2.  `email-template`  - controller for creating email templates, fetching email templates info, updating email templates info and deleting email templates info.
3.  `account-email`  - controller for sending, updating, deleting account emails.
