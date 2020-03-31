<h1 align="center">
  <a href="https://github.com/jsheng08/hapi-pgsql"><img src="https://github.com/jsheng08/hapi-pgsql/raw/master/hapi-pgsql.png" alt="hapi-pgsql" width="200"></a>
  <br>
  hapi-pgsql
  <br>
  Hapi Postgresql Plugin
  <br>
</h1>

<p align="center">
    <a href="https://travis-ci.org/jsheng08/hapi-pgsql"><img src="https://img.shields.io/travis/jsheng08/hapi-pgsql/master.svg" alt="travis"></a>
  <a href='https://coveralls.io/github/jsheng08/hapi-pgsql?branch=master'><img src='https://coveralls.io/repos/github/jsheng08/hapi-pgsql/badge.svg?branch=master' alt='Coverage Status' /></a>
  <a href="https://standardjs.com"><img src="https://img.shields.io/badge/code_style-standard-brightgreen.svg" alt="Standard - JavaScript Style Guide"></a>
</p>

This Hapi Plugin creates a Connection to PostgreSQL when your server starts up and makes it available anywhere in your app's route handlers via request.pgsql.

When you shut down your server (e.g. the server.stop in your tests) the connection is closed for you.

### 1. *Download/Install* from NPM

```sh
npm install hapi-pgsql --save
```

### 2. *Intialise* the plugin in your Hapi Server

in your server:
```js
await server.register({
    plugin: require('hapi-pgsql'),
    options: {
        database_url: 'postgresql://username:password@hostname/database',
    }
})
```
Now *all* your route handlers have access to Postgres
via: `request.pgsql`

### 3. Using Postgres Client in your Route Handler

```js
server.route({
    method: 'GET',
    path: '/',
    handler: async (request, h) => {
        const time = await request.pgsql.query('SELECT NOW()')
        return `Hello World! Time: ${time.rows[0].now}`;
    }
});
```

