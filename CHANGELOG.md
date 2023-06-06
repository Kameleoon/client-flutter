# Changelog
All notable changes to this project will be documented in this file.

## 2.0.0 - 2023-06-06
* Upgraded Flutter SDK library to use [`iOS SDK 3.0.2`](https://github.com/Kameleoon/client-swift/blob/main/CHANGELOG.md) / [`Android SDK 3.1.0`](https://github.com/Kameleoon/client-android/blob/main/CHANGELOG.md) / [`JS/TS SDK 1.4.4`](https://github.com/Kameleoon/client-js/blob/main/CHANGELOG.md)
* To enhance security, we have made it mandatory to include the **client_id** and **client_secret** fields in the Kameleoon configuration file. Alternatively, you can set these fields using the internal [`KameleoonConfiguration`](https://developers.kameleoon.com/flutter-sdk.html#create) instance. By requiring these fields, we aim to ensure that only authorized parties have access to Kameleoon and its associated resources.
* Real-Time Updates:
    - Added update campaigns and feature flag configurations instantaneously with Real-Time Streaming Architecture: [`Documentation`](https://developers.kameleoon.com/flutter-sdk.html#streaming) or [`Product Updates`](https://www.kameleoon.com/en/blog/real-time-streaming)
    - Added a new method [`updateConfigurationHandler`](https://developers.kameleoon.com/flutter-sdk.html#updateconfigurationhandler) to handle events when configuration has updated data in real time.
* Adding new methods for working with feature flags:
    - [`isFeatureActive`](https://developers.kameleoon.com/flutter-sdk.html#isFeatureActive)
    - [`getFeatureVariationKey`](https://developers.kameleoon.com/flutter-sdk.html#getFeatureVariable)
    - [`getFeatureVariable`](https://developers.kameleoon.com/flutter-sdk.html#getFeatureVariable)
    - [`getFeatureAllVariables`](https://developers.kameleoon.com/flutter-sdk.html#getFeatureAllVariables)
* Adding new methods for working with data configuration:
    - [`getExperimentList`](https://developers.kameleoon.com/flutter-sdk.html#getExperimentList)
    - [`getFeatureList`](https://developers.kameleoon.com/android-sdk.html#getFeatureList)
    - [`getFeatureListActive`](https://developers.kameleoon.com/android-sdk.html#getFeatureList)html#getFeatureListActive)
* Renaming of methods:
    - `obtainFeatureVariable` -> [`getFeatureVariable`](https://developers.kameleoon.com/flutter-sdk.html#getFeatureVariable)
    - `activateFeature` -> [`isFeatureActive`](https://developers.kameleoon.com/flutter-sdk.html#isFeatureActive)
    - `obtainVisitorCode` -> [`getVisitorCode`](https://developers.kameleoon.com/flutter-sdk.html#getVisitorCode)
    - `retrieveDataFromRemoteSource` -> [`getRemoteData`](https://developers.kameleoon.com/flutter-sdk.html#getRemoteData)
    - `obtainVariationAssociatedData` -> [`getVariationAssociatedData`](https://developers.kameleoon.com/flutter-sdk.html#getVariationAssociatedData)
* Added support for **Experiment** & **Exclusive Campaign** conditions. Related to [`triggerExperiment`](https://developers.kameleoon.com/flutter-sdk.html#triggerexperiment) / [`isFeatureActive`](https://developers.kameleoon.com/flutter-sdk.html#isFeatureActive)
* Adding / renaming of exceptions:
    - `CredentialsNotFound`. Related to [`KameleoonClientFactory.create`](https://developers.kameleoon.com/flutter-sdk.html#create)
    - `NotActivated` -> `NotAllocated`. Related to [`triggerExperiment`](https://developers.kameleoon.com/flutter-sdk.html#triggerexperiment)
    - `ExperimentConfigurationNotFound` -> `ExperimentNotFound`. Related to [`triggerExperiment`](https://developers.kameleoon.com/flutter-sdk.html#triggerexperiment)
    - `FeatureConfigurationNotFound` -> `FeatureNotFound`. Related to [`isFeatureActive`](https://developers.kameleoon.com/flutter-sdk.html#isFeatureActive)
* Changes in `KameleoonData`:
    - [`CustomData`](https://developers.kameleoon.com/flutter-sdk.html#customData) accepts a list of values (previously it appected only one value)
    - Added support of `is among the values` operator for CustomData
    - Added KameleoonData [`Device`](https://developers.kameleoon.com/android-sdk.html#device) data. Possible values are: **PHONE**, **TABLET**, **DESKTOP**.
    - Removed KameleoonData `Interest`

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
