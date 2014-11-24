Janus VR Presence Server
========================

Installation
------------

1. Download and install node from [nodejs.org](http://nodejs.org)

2. `cd` into the root of the repository where `server.js` is located and run `sudo npm install` to install all module
dependencies listed in `package.json`.

3. The modules will be placed into the `node_modules` folder and are required for the server to start.

4. Run the following script in the root of the repository: `./generate_key` to generate a SSL certificate for the server.

5. When asked to provide a Common Name for the server enter the domain name the server will be running on. I.e.
`yourdomain.com`. If running a development version of the server on OSX you can also use your Bonjour name i.e.
`yourcomputer.local`. On OSX you can see your computer's Bonjour name by going to System Preferences -> Sharing and
looking under the Computer Name field.

6. When asked to provide a challenge password while generating the SSL certificate press enter to skip setting a password.

7. From the root of the repository `cd` to `node_modules/sequelize-cli/bin`. Run `./sequelize init` to initialize the
ORM library for connecting to the database. Adjust the generated config file at
`node_modules/sequelize-cli/bin/config/config.json` with your desired configuration. Note that the `development`
environment is the default environment if not specified otherwise. You may need to set the `port` and `dialectOptions`
as follows to get the config to work with MAMP on OSX as the path to the MySQL socket is in a non-standard location
when running MAMP:

```
"development": {
        "username": "janusvr",
        "password": "PASSWORD_HERE",
        "database": "janusvr_development",
        "host": "127.0.0.1",
        "dialect": "mysql",
        "port": 3306,
        "dialectOptions": {
            "socketPath": "/Applications/MAMP/tmp/mysql/mysql.sock",
            "supportBigNumbers": true,
            "bigNumberStrings": true
        }
    },
```

8. Run `./sequelize db:migrate` to run the initial database migration.

9. `cd` to the `src/database/seeds` folder and run `node DatabaseSeeder.js` to run the initial database seed.


Adding Database Migrations
--------------------------

1. `cd` to the `node_modules/sequelize-cli/bin` folder and run `sequelize migration:create --name MIGRATION_NAME`
where `MIGRATION_NAME` is the name of the migration you wish to create. A new JS file will be created in the migrations
folder which you can edit to change the database structure.