# Permissions overview

## Permission approval

### Request prompts for dangerous permissions

#### Runtime requests (Android 6.0 and higher)

Your app must ask the user to grant the dangerous permissions at runtime

#### Install-time requests (Android 5.1.1 and below)

the system automatically asks the user to grant all dangerous permissions for your app at install-time

## Permissions for optional hardware features

## Automatic permission adjustments

## Protection levels

+ Normal permissions
  + If an app declares in its manifest that it needs a normal permission, the system automatically grants the app that permission at install time. The system doesn't prompt the user to grant normal permissions, and users cannot revoke these permissions
+ Signature permissions
  + The system grants these app permissions at install time, but only when the app that attempts to use a permission is signed by the same certificate as the app that defines the permission

+ Dangerous permissions

## Permission groups

All dangerous Android permissions belong to permission groups. Any permission can belong to a permission group regardless of protection level. However, a permission's group only affects the user experience if the permission is dangerous

Your app still needs to explicitly request every permission it needs, even if the user has already granted another permission in the same group

## Viewing an app's permissions

`adb shell pm list permissions -s` 乱码