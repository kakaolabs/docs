API document for common application manager system

System allow many developers can join in. Each developer have many apps.

Each developer will be given 2 hash key: **api_key** and **api_secret**.

+ **api_key** will be used as GET parameter for all API to send to server.

+ **api_secret** will be use to calculate api_signature which will be use as
    GET parameter for all API


# User signup
/v1/devices/signup

#### GET params
+ `api_key`
+ `api_secret`
+ `app_secret` - App secret is unique for each application

#### POST params
+ `device_id` - will be use to send push notification
+ `device_type` - iphone, ipad, samsung, ...
+ `os` - 0 - iOS, 1 - android
+ `os_version` - 7.0, 6.0

#### JSON result
+ `access_token` - will be used for next time request


# App related
/v1/apps/related

#### GET params
+ `api_key`
+ `api_secret`
+ `os` - OS type. 0 - iOS, 1 - android

#### JSON result
List of objects
+ `name`
+ `version`
+ `description`
+ `image_url`
+ `download_url`


# App version
/v1/app/:app_id/version

#### GET params
+ `api_key`
+ `api_secret`

#### JSON result
+ `version` - newest version of app id
+ `subversion` - newest version of app id
+ `force_update` - true/false if true use must download the app
+ `download_url` - link to download app
