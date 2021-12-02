# digitalmediasolutions/documents

The point of the project is to manage the sending of emails. See  [https://github.com/digitalmediasolutions/documents/tree/main/o2o-caas](https://github.com/digitalmediasolutions/documents/tree/main/o2o-caas)  for more information.

## Pre-requisites
Typescript and running instances of a MongoDB are required for the app to start. The **MongoDB** is used for the rest of the models in the app.

## Installation
Do the following to clone and start the project.

$ git clone https://github.com/digitalmediasolutions/documents.git
$ cd documents
$ npm i
$ npm start

## Models
This app has the following models:
1.  `Accounts`  - representing the accounts of the system.
2.  `EmailTemplates`  - a model to represent the email request template.
3.  `EmailDistributions`  - a model to represent the records from SendGrid after sending emails.

## Controllers

Controllers expose API endpoints for interacting with the models and more.

In this app, there are four controllers:
