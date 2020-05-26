# dokku-dscribe

A dokku plugin to reduce app creation commands to just one.

## Requirements

- dokku v0.20.x+
- docker 19.03.+

## Installation

```bash
sudo dokku plugin:install https://github.com/dscribers/dokku-dscribe.git dscribe
```

## Usage

### Create .env file before build

```bash
dokku dscribe:packenv APP_NAME # Packs all env vars into .env file before building the app.
```

> **Note**: All apps created with `dscribe:create`, `dscribe:frontend`, `dscribe:api`
> and `dscribe:fullstack` have this enabled for them by default.

### Slack urls

```bash
dokku dscribe:slack # Shows notification urls for all types
dokku dscribe:slack TYPE # Shows the notification url for the given type
dokku dscribe:slack TYPE URL # Sets the notification url for the given type
```

> **Note**: `TYPE` can only be one of `prod`, `staging` and `sprint`.

### Create an app

```bash
dokku dscribe:create APP_NAME
```

This runs the following code:

```bash
dokku apps:create APP_NAME # creates production app
dokku apps:create APP_NAME-staging # creates staging app
dokku apps:create APP_NAME-sprint # creates sprint app

dokku slack:set APP_NAME prod_url # Sets the slack notification url for production, if available
dokku slack:set APP_NAME-staging staging_url # Sets the slack notification url for staging, if available
dokku slack:set APP_NAME-sprint sprint_url # Sets the slack notification url for sprint, if available
```

### Create a frontend app

```bash
dokku dscribe:frontend APP_NAME
```

This runs the following code:

```bash
dokku dscribe:create APP_NAME
dokku dscribe:packenv APP_NAME
```

### Create an API app

```bash
dokku dscribe:api APP_NAME
```

This runs the following code:

```bash
dokku apps:create APP_NAMEapi # creates production api app
dokku postgres:create APP_NAMEdb # creates postgres production database
dokku postgres:link APP_NAMEdb APP_NAMEapi # connects production api app and database

dokku apps:create APP_NAMEapi-staging # creates staging api app
dokku postgres:create APP_NAMEdb-staging # creates postgres staging database
dokku postgres:link APP_NAMEdb-staging APP_NAMEapi-staging # connects staging api app and database

dokku apps:create APP_NAMEapi-sprint # creates sprint api app
dokku postgres:create APP_NAMEdb-sprint # creates postgres sprint database
dokku postgres:link APP_NAMEdb-sprint APP_NAMEapi-sprint # connects sprint api app and database

dokku slack:set APP_NAMEapi prod_url # Sets the slack notification url for production, if available
dokku slack:set APP_NAMEapi-staging sprint_url # Sets the slack notification url for staging, if available
dokku slack:set APP_NAMEapi-sprint sprint_url # Sets the slack notification url for sprint, if available
```

### Create a fullstack app

```bash
dokku dscribe:fullstack APP_NAME
```

> This runs commands in `dscribe:frontend` and `dscribe:api`.

### Destroy app

```bash
dokku dscribe:destroy APP_NAME # Destroys production, staging and sprint apps
```

The runs the following code:

```bash
dokku apps:destroy APP_NAME
dokku apps:destroy APP_NAME-staging
dokku apps:destroy APP_NAME-sprint
```

## Letsencrypt

This plugin checks that the application has https enabled at each release.
If not, it enables https for it.
