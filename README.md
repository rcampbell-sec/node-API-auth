`> npm init`
`> npm install express` back end routing
`> npm install nodemon` restart our test server on the fly
`npm install mongoose` so that we can easily interact with out db

## server + routing set up
1. create our express app in `index.js`, then start a server listening.
2. create the `routes/` directory.
3. create `auth.js` file for handling authentication-specific requests.
    3a. in this file, import express router: `require('express').Router()`
4. import the auth route into `index.js` with `const authRoute = require('./routers/auth')`
5. add it as middleware: `app.use('/api/user', authRoute);`
    this means anything under the `api/user/` subdomain will refer to the authRoute middleware

start creating the `auth.js` routers
1. POST -> `/register` for registering a new user
2. POST -> `/login`

## database
go to `cloud.mongodb.com` to set up our test database.
    add the connection string to the environment vars file
    (security) - add user access stuff, IP whitelisting etc through the mongo website.

in `index.js`
    `const mongoose = require('mongoose');`
    `mongoose.connect(<CONN STRING>, { useNewUrlParse: true}).then(() => { console.log('connected to db') });`

## db models
create a file eg `Users.js` (note case)
inside this file import mongoose and define a `new mongoose.Schema()`
when exporting our model we use `module.exports = mongoose.Schema('User', userSchema)`.  User is the name of the model

## using the db models
in our `auth.js` routes we may make new instances of the model, eg new User.  we then build it out with JSON data.
in order to parse the POST request data properly, we need to go to `index.js` where our `app` is defined, and give it new middleware:
`app.use(express.json());` lets express know to parse requests as JSON objects

