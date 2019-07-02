The passwords server survey is a collection of anonymous server data sent by the passwords app once a month.
The statistics are publicly available on [ncpw.mdns.eu](https://ncpw.mdns.eu/).


## Data privacy
All data collected by tge server survey is anonymous (and not pseudonym).
The data can not be traced back to your server and does not contain any form of id.
The data does also not allow to track servers or identify recurring reports from a server.
We do not track your individual users or their use of the app or Nextcloud.
We do not share raw data with anyone except for the publicly available statistics on the homepage.


## What is the use of the server survey?
There is absolutely no data available about the Nextcloud ecosystem.
We do not know if and how fast new versions of Nextcloud or the app are installed by users or which kind of server they run on.
We also do not know which of our many integrations or third party services really matter to users.
We also do not know how new features like the E2E are accepted or how much deprecated features like the legacy api are still in use.
In order to learn more about this we have created the server survey to collect this data each week and give us more information on the apps usage.

## What does the server survey do for me?
The server survey is your way of telling us what to focus on during development just by using that feature.
Much used services will receive more attention during development.
Much used versions of Nextcloud or PHP may receive longer support even after they are officially no longer supported.
Much used deprecated features may have a longer lifespan and a more "soft" phase out instead of a fast cancellation.
Less used services might get removed.
In future versions of the app, third party services hosted by us might be exclusive to servers who participate in the server survey.

## Server survey report modes
In the admin settings you can specify which data you want to send in the server survey.

## No participation
Will not send any data at all.
Not even that you do not participate.

## Basic
Will send the Nextcloud, PHP and app version and information about your OS, CPU architecture, cron execution and which database software is used.

This is what a basic report looks like:
```
{
    "version": {
        "server":"16.0.1.1",
        "app": "2019.7.0",
        "php": "7.3.0"
    },
    "environment": {
        "os": "Linux",
        "architecture": "x86_64",
        "bits": 64,
        "database": "mysql",
        "cron": "cron"
    }
}
```



## Full
Will send all the basic information and the services selected in the admin settings, legacy api usage, how much sharing is used, which encryption types are used, and if selected other apps are installed.

This is what a full report looks like:
```
{
    "version": {
        "server":"16.0.1.1",
        "app": "2019.7.0",
        "php": "7.3.0"
    },
    "environment": {
        "os": "Linux",
        "architecture": "x86_64",
        "bits": 64,
        "database": "mysql",
        "cron": "cron"
    },
    "legacyApi": {
        "enabled": true,
        "used": false
    },
    "services": {
        "images": "imagick",
        "favicons": "bi",
        "faviconApi": false,
        "previews": "pageres",
        "previewApi": false,
        "words": "local",
        "security": "hibp"
    },
    "settings": {
        "nigthlies": false,
        "handbook": false
    },
    "apps": {
        "passman": {
            "installed": true,
            "enabled": false
        },
        "unsplash": {
            "installed": true,
            "enabled": true
        }
    },
    "sharing": {
        "shares": 10
    },
    "encryption": {
        "sse": {
            "default": "SSEv1r2",
            "SSEv1r1": true,
            "SSEv1r2": true,
            "SSEv2r1": false,
            "none": false
        },
        "cse": {
            "default": "none",
            "CSEv1r1": false,
            "none": true
        }
    }
}
```