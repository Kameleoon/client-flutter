# Changelog
All notable changes to this project will be documented in this file.

## 2.0.0 - 2023-06-06
The Flutter 2.0.0 release contains the following changes:
* Upgraded Flutter SDK library to use [`iOS SDK 3.0.2`](https://github.com/Kameleoon/client-swift/blob/main/CHANGELOG.md) / [`Android SDK 3.1.0`](https://github.com/Kameleoon/client-android/blob/main/CHANGELOG.md) / [`JS/TS SDK 1.4.4`](https://github.com/Kameleoon/client-js/blob/main/CHANGELOG.md)
* To enhance security, we have made it mandatory to include the `client_id` and `client_secret` fields in the Kameleoon configuration file. Please make sure you have set these fields as soon as possible. Alternatively, you can set these fields using the internal [`KameleoonConfiguration`](https://developers.kameleoon.com/flutter-sdk.html#create) instance. This change helps ensure that only authorized parties have access to Kameleoon and its associated resources.
* Real-time updates:
    - Added the ability to update your campaigns and feature flag configurations instantaneously with the Real-Time Streaming Architecture. For details see the: [`Documentation`](https://developers.kameleoon.com/flutter-sdk.html#streaming) and [`Product Updates`](https://www.kameleoon.com/en/blog/real-time-streaming).
    - Added a new method [`updateConfigurationHandler`](https://developers.kameleoon.com/flutter-sdk.html#updateconfigurationhandler) to handle events when configuration has updated data in real time.
* Added new methods for working with feature flags:
    - [`isFeatureActive`](https://developers.kameleoon.com/flutter-sdk.html#isfeatureactive)
    - [`getFeatureVariationKey`](https://developers.kameleoon.com/flutter-sdk.html#getfeaturevariable)
    - [`getFeatureVariable`](https://developers.kameleoon.com/flutter-sdk.html#getfeaturevariable)
    - [`getFeatureAllVariables`](https://developers.kameleoon.com/flutter-sdk.html#getfeatureallvariables)
* Added new methods for working with data configuration:
    - [`getExperimentList`](https://developers.kameleoon.com/flutter-sdk.html#getexperimentlist)
    - [`getFeatureList`](https://developers.kameleoon.com/android-sdk.html#getfeaturelist)
    - [`getFeatureListActive`](https://developers.kameleoon.com/android-sdk.html#getfeaturelistactive)
* Renamed the following methods:
    - `obtainFeatureVariable` is now [`getFeatureVariable`](https://developers.kameleoon.com/flutter-sdk.html#getfeaturevariable)
    - `activateFeature` is now [`isFeatureActive`](https://developers.kameleoon.com/flutter-sdk.html#isfeatureactive)
    - `obtainVisitorCode` is now [`getVisitorCode`](https://developers.kameleoon.com/flutter-sdk.html#getvisitorcode)
    - `retrieveDataFromRemoteSource` is now [`getRemoteData`](https://developers.kameleoon.com/flutter-sdk.html#getremotedata)
    - `obtainVariationAssociatedData` is now [`getVariationAssociatedData`](https://developers.kameleoon.com/flutter-sdk.html#getvariationassociatedata)
* Added support for **Experiment** & **Exclusive Campaign** conditions. Related to [`triggerExperiment`](https://developers.kameleoon.com/flutter-sdk.html#triggerexperiment) and [`isFeatureActive`](https://developers.kameleoon.com/flutter-sdk.html#isfeatureactive).
* Added new exceptions:
    - `CredentialsNotFound`. Related to [`KameleoonClientFactory.create`](https://developers.kameleoon.com/flutter-sdk.html#create).
* Renamed exceptions:
    - `NotActivated` is now `NotAllocated`. Related to [`triggerExperiment`](https://developers.kameleoon.com/flutter-sdk.html#triggerexperiment).
    - `ExperimentConfigurationNotFound` is now `ExperimentNotFound`. Related to [`triggerExperiment`](https://developers.kameleoon.com/flutter-sdk.html#triggerexperiment).
    - `FeatureConfigurationNotFound` is now `FeatureNotFound`. Related to [`isFeatureActive`](https://developers.kameleoon.com/flutter-sdk.html#isfeatureactive).
* Changes in `KameleoonData`:
    - [`CustomData`](https://developers.kameleoon.com/flutter-sdk.html#customData) accepts a list of values (previously, it accepted only one value)
    - Added support for the `is among the values` operator for CustomData
    - Added KameleoonData [`Device`](https://developers.kameleoon.com/android-sdk.html#device) class. Possible values are: **PHONE**, **TABLET**, **DESKTOP**.
    - Removed the KameleoonData `Interest` class.

## 1.0.3 - 2022-05-31
* Added method for retrieving data from remote source: [`retrieveDataFromRemoteSource`](https://developers.kameleoon.com/flutter-sdk.html#retrievedatafromremotesource)
* Added support of multi-environment for feature flags, Related to [`activateFeature`](https://developers.kameleoon.com/flutter-sdk.html#activatefeature), [`obtainFeatureVariable`](https://developers.kameleoon.com/flutter-sdk.html#obtainfeaturevariable)
* Updated Flutter SDK library to iOS 2.0.15 / Android 2.0.13 / JS 1.0.7

## 1.0.2 - 2021-11-03
* Added scheduling feature
* Refactoring structure of library
* Updated Flutter SDK library to [`iOS 2.0.12`](https://github.com/Kameleoon/client-swift/blob/master/CHANGELOG.md#2012---2021-10-26) / [`Android 2.0.10`](https://github.com/Kameleoon/client-android/blob/master/CHANGELOG.md#2010---2021-10-25) / [`JS 1.0.5`](https://github.com/Kameleoon/client-javascript/blob/master/CHANGELOG.md#105---2021-11-03)
## 1.0.1
* Add Web platform
* Update Flutter SDK library to [`iOS 2.0.11`](https://github.com/Kameleoon/client-swift/blob/master/CHANGELOG.md#2011---2021-08-31) / [`Android 2.0.9`](https://github.com/Kameleoon/client-android/blob/master/CHANGELOG.md#209)

# Deprecated versions
All of the versions listed below are no longer supported and we strongly advise to upgrade to the latest version.

## 1.0.0
* Release

## 0.0.3
* Implement null-safety

## 0.0.2
* Implement iOS bridge

## 0.0.1
* Implement Android bridge
