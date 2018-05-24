# Chatbot Smart Widget BFF (Node)

This is a Node.js backend service library to create a BFF service for the Chatbot Smart Widget. The widget provides a picker field to choose a person from a list of contacts. This service is matched by a [corresponding UI](https://github.com/digipolisantwerp/contact-picker_widget_angular).

There is a **demo service**, see below for instructions on running it.

## How to use

### Installing

Copy the .npmrc file from this repo to your application's folder.

Then install (you will need to be on the digipolis network):

```sh
> npm install @acpaas-ui-widgets/nodejs-contact-picker
```

### Using

Express example:

```js
const express = require('express');
const app = express()
const pickerHelper = require('@acpaas-ui-widgets/nodejs-contact-picker');
const controller = pickerHelper.mprofielAdmin.createController({
    clientId: "<oauth client id>",
    clientSecret: "<oauth client secret>",
    oauthUrl: "https://api-gw-o.antwerpen.be/astad/mprofieladmin/v1/oauth2/token",
    serviceUrl: "https://api-gw-o.antwerpen.be/astad/mprofieladmin/v1/api/mprofiel"
});
app.get('/api/medewerkers', controller);
app.listen(3000);
```

You can obtain the OAuth credentials by taking a contract on the API in the [API store](https://api-store-o.antwerpen.be).

The library provides the following interface:

- mprofielAdmin
  - *createController(config)*: create an express controller that handles the connection to the mprofiel-admin API
  - *createService(config)*: create a function that accepts a query and returns a promise of the results of the mprofiel-admin API for that query. The createController routine builds on top of this.

## Run the demo app

Create a .env file containing:

```sh
PORT=3000
OAUTH_CLIENT_ID=<client id>
OAUTH_CLIENT_SECRET=<client secret>
MPROFIEL_ADMIN_OAUTH_URL=https://api-gw-o.antwerpen.be/astad/mprofieladmin/v1/oauth2/token
MPROFIEL_ADMIN_API_URL=https://api-gw-o.antwerpen.be/astad/mprofieladmin/v1/api/mprofiel
```

Obtain the client id and client secret by creating a contract on the mprofiel-admin service on [api-store-o.antwerpen.be](https://api-store-o.antwerpen.be).

(Remove the -o extension in the URL's to use the production api.)

Run the service:

```sh
> npm install
> npm start
```

Test by browsing to [localhost:3000/api/medewerkers?search=aa](http://localhost:3000/api/medewerkers?search=aa).

The UI demo app expects the service to run on port 3000.

## Service Specification

The service implements the following protocol:

- GET /path/to/endpoint?search=...
- search = the text that the user typed on which to match
- result = JSON-encoded array of [ContactItem](src/mprofiel-admin/types.ts) objects

An [example swagger description](swagger-example.json) is included.

## Contributing

We welcome your bug reports and pull requests.

Please see our [contribution guide](CONTRIBUTING.md).

## License

This project is published under the [MIT license](LICENSE.md).
