# dokku-dscribe

A dokku plugin for creating data apps.

## Requirements

- dokku v0.20.x+
- docker 19.03.+

## Installation

```bash
sudo dokku plugin:install https://github.com/dscribers/dokku-dscribe-data.git dscribe
```

## Usage

### Create an app

```bash
dokku dscribe:create APP_NAME
```

This runs the following code:

```bash
dokku postgres:create APP_NAME
dokku redis:create APP_NAME
```

### Destroy app

```bash
dokku dscribe:destroy APP_NAME
```

The runs the following code:

```bash
dokku postgres:destroy APP_NAME
dokku redis:destroy APP_NAME
```
