API document for common application manager system

System allow many developers can join in. Each developer have many apps
Each developer will be given 2 hash key: **api_key** and **api_secret**
**api_key** will be used as GET parameter for all API to send to server.
**api_secret** will be use to calculate api_signature which will be use as
GET parameter for all API


# User signup
/v1/users/signup

## GET params
+ `api_key`
+ `api_secret`
+ `app_id` - App id is unique for all users

## POST params
+ `device_id` - will be use to send push notification
+ `device_type` - iphone, ipad, samsung, ...
+ `os` - ios, android
+ `os_version` - 7.0, 6.0

## JSON result
+ `access_token` - will be used for next time request


# User start session
/v1/users/start

## GET params
+ `api_key`
+ `api_secret`
+ `app_id` - App id is unique for all users
+ `version` - Current version of the app
+ `access_token`

## JSON result: {}


# User end session
/v1/users/start

## GET params
+ `api_key`
+ `api_secret`
+ `app_id` - App id is unique for all users
+ `version` - Current version of the app
+ `access_token`

## JSON result: {}


# App related
/v1/apps

## GET params
+ `api_key`
+ `api_secret`

## JSON result
List of objects
+ `name`
+ `version`
+ `description`
+ `image_url`
+ `download_url`


# App version
/v1/app/:app_id/version

## GET params
+ `api_key`
+ `api_secret`

## JSON result
+ `version` - newest version of app id
+ `force_update` - true/false if true use must download the app
+ `download_url` - link to download app

# App news
/v1/app/:app_id/news

## GET params
+ `api_key`
+ `api_secret`
+ `from_time` - epoch time

## JSON result
List of objects:
+ `title`
+ `content`
+ `timestamp`
