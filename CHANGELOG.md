[customdata]: https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#customdata

# Changelog
## 3.7.0 - 2026-02-17
### Features
* Upgraded Flutter SDK to use [`iOS SDK 4.25.0`](https://github.com/Kameleoon/client-swift/blob/main/CHANGELOG.md#4250---2026-02-17) / [`Android SDK 4.24.0`](https://github.com/Kameleoon/client-android/blob/main/CHANGELOG.md#4240---2026-02-17) / [`JS/TS SDK 4.18.0`](https://github.com/Kameleoon/client-js/blob/main/CHANGELOG.md#4180-2026-02-13)
* Added support for version strings containing pre-release and build metadata, in accordance with [Semantic Versioning](https://semver.org/#semantic-versioning-200). Pre-release and build metadata components are currently ignored, and the version is normalized to `major.minor.patch`. Full support for **Semantic Versioning**, including pre-release, will be introduced in future releases.
* Updated the allowed range for the [`trackingIntervalMilliseconds`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#initialize-the-kameleoon-client). The new range is from **`1000` ms** (default) to **`5000` ms**, allowing a reduction in the number of tracking requests.
* Introduced a new `track` parameter for [`addData`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#adddata). When set to `false`, the data is stored locally and used only for targeting evaluation; it is not sent to the Data API, helping to prevent duplicate data from being recorded. The default value is `true`. This behavior is consistent with the `track` parameter used in evaluation methods such as [`getVariation`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#getvariation).
* Introduced the [`activityTrackingIntervalMilliseconds`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#initialize-the-kameleoon-client) parameter, which defines the interval at which activity events are sent. This helps reduce network usage and battery consumption. The minimum and default value is `15 000` ms. Setting this value to `0` disables periodic activity tracking; in this case, only a single activity event is sent at application startup. (Only iOS / Android)
### Bug fixes
* Fixed an issue where the `isUniqueIdentifier` parameter passed to `KameleoonClientConfig` was not applied when initializing [`KameleoonClient`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#initialize-the-kameleoon-client).


## 3.6.0 - 2025-12-25
### Features
* Upgraded Flutter SDK to use [`iOS SDK 4.22.2`](https://github.com/Kameleoon/client-swift/blob/main/CHANGELOG.md#4222---2025-12-24) / [`Android SDK 4.21.1`](https://github.com/Kameleoon/client-android/blob/main/CHANGELOG.md#4211---2025-12-24) / [`JS/TS SDK 4.17.0`](https://github.com/Kameleoon/client-js/blob/main/CHANGELOG.md#4171-2025-12-24)
* Updated evaluation and tracking logic to comply with GDPR requirements when consent is not given:
    - If behavior is **partially blocked**, the default variation will be returned.
    - If behavior is **completely blocked**, an exception will be thrown.

## 3.5.1 - 2025-11-27
### Bug fixes
* Resolved an issue where the `com.kameleoon.flutter` platform channel sent messages from a non-platform thread when emitting SDK log events. All logging-related native-to-Flutter messages are now properly dispatched on the platform thread.

## 3.5.0 - 2025-10-30
### Features
* Upgraded Flutter SDK to use [`iOS SDK 4.21.1`](https://github.com/Kameleoon/client-swift/blob/main/CHANGELOG.md#4211---2025-10-23) / [`Android SDK 4.20.2`](https://github.com/Kameleoon/client-android/blob/main/CHANGELOG.md#4202---2025-10-24) / [`JS/TS SDK 4.9.0`](https://github.com/Kameleoon/client-js/blob/main/CHANGELOG.md)
* * In the Web integration, the [`KameleoonClient`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#initialize-the-kameleoon-client) now starts initializing immediately upon creation. Previously, initialization only began after calling the [`runWhenReady`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#runwhenready) method.
initializes only after [`runWhenReady`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#runwhenready) method.
* Added support for a **New**/**Returning** visitor breakdown filter in reports.
* Refactored targeting condition logic (remote data requests are now optional) for:
  - Time elapsed since first/last visit
  - New or returning visitors
  - Total number of visits
  - Number of visits today
* Added support for **304 (Not Modified)** responses from the SDK config service to avoid redundant updates and reduce traffic when the configuration hasn't changed.
* Added support for using a Custom Data value for traffic bucketing instead of the default visitor code. [Learn More](https://help.kameleoon.com/create-feature-flag/#Advanced_Flag_Settings).
* Introducing a fallback configuration mechanism via the [`defaultDataFile`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#initialize-the-kameleoon-client) parameter. If no cached configuration is available, the SDK immediately uses the provided default. For version control, the SDK prioritizes the default configuration if its `dateModified` timestamp is more recent than the cached version.
* Added the [`evaluateAudiences`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#evaluateaudiences) method. This method iterates over all Audiences Explorer segments, evaluates each one, and tracks the segments for which the visitor is targeted using the [`TARGETINGSEGMENT`](https://developers.kameleoon.com/apis/data-api-rest/all-endpoints/post-visit-events/) event.
* Introduced the new [`getDataFile`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk#getdatafile) method. This method returns the current SDK configuration (also known as the **data file**) used for evaluation and targeting. It is **not** intended for production use to fetch variations for every feature flag in the returned list, as it is not optimized for performance. For that purpose, use [`getVariations`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#getvariations) instead. `getDataFile` is mainly useful for debugging or QA, for example to let internal users manually select a variant for a specific feature flag in production.
* Added a new property **`name`** to [`Variation`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#variation), representing the name of the variation.
* Added an `overwrite` flag to [`CustomData`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk#customdata), used as the `overwrite` parameter during tracking.
* [`CustomData`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk#customdata) can now be created using a `name`, in addition to the existing method of using an `index`.
### Bug fixes
* Changed the order in which **conversion** and **experiment** events are sent. This may lead to more accurate **visit**-level experiment reporting.

## 3.4.0 - 2025-04-02
### Features
* Upgraded Flutter SDK to use [`iOS SDK 4.13.2`](https://github.com/Kameleoon/client-swift/blob/main/CHANGELOG.md) / [`Android SDK 4.12.0`](https://github.com/Kameleoon/client-android/blob/main/CHANGELOG.md)
* Added support for new conditions:
    - Exclusive Campaign
    - Experiment
    - Personalization

All notable changes to this project will be documented in this file.

## 3.3.0 - 2025-03-28
### Features
* Upgraded Flutter SDK to use [`iOS SDK 4.13.1`](https://github.com/Kameleoon/client-swift/blob/main/CHANGELOG.md) / [`Android SDK 4.11.1`](https://github.com/Kameleoon/client-android/blob/main/CHANGELOG.md) / [`JS/TS SDK 4.9.0`](https://github.com/Kameleoon/client-js/blob/main/CHANGELOG.md)
* Added new optional parameters `negative` and `metadata` to the [`trackConversion`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk#trackconversion) method.
* Added new optional parameter `metadata` to the [`Conversion`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk#conversion) data constructor.
* Added support for Contextual Bandit evaluations. Calling [`getRemoteVisitorData`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk#getremotevisitordata) with the `cbs=true` flag is required for this feature to function correctly.
* Added new configuration parameter `networkDomain` to [`KameleoonClientConfig`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#initialize-the-kameleoon-client). This parameter allows specifying a custom domain for all outgoing network requests.
* Added SDK support for **Mutually Exclusive Groups**. When feature flags are grouped into a **Mutually Exclusive Group**, only one flag in the group will be evaluated at a time. All other flags in the group will automatically return their default variation.
* Added SDK support for **holdout experiments**. Visitors assigned to a holdout experiment are excluded from all other rollouts and experiments, and consistently receive the default variation. For visitors not in a holdout experiment, the standard evaluation process applies, allowing them to be evaluated for all feature flags as usual.
* Added the [`setForcedVariation()`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk#setforcedvariation) method. This method allows explicitly setting a forced variation for a visitor, which will be applied during experiment evaluation.
* Added support for **simulated** variations. The feature is available only on Web.
*  Compression has been added to the [Conversions](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#conversion) list. This enhancement prevents unchecked growth and improves the speed of visitor synchronization with local storage. The feature is available only on iOS and Android.
### Bug fixes
* Resolved an issue where [CustomData][customdata] values were not applied correctly for targeting.

## 3.2.1 - 2025-02-03
### Bug fixes
* Resolved an issue where the SDK could crash during prolonged application initialization on Android devices.

## 3.2.0 - 2025-01-07
### Features
* Upgraded Flutter SDK to use [`iOS SDK 4.7.0`](https://github.com/Kameleoon/client-swift/blob/main/CHANGELOG.md) / [`Android SDK 4.5.0`](https://github.com/Kameleoon/client-android/blob/main/CHANGELOG.md) / [`JS/TS SDK 4.2.3`](https://github.com/Kameleoon/client-js/blob/main/CHANGELOG.md)
* Introduced new evaluation methods for clarity and improved efficiency when working with the SDK:
  - [`getVariation`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#getvariation)
  - [`getVariations`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#getvariations)
* These methods replace the deprecated ones:
  - [`getFeatureVariationKey`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk#getfeaturevariationkey)
  - [`getFeatureVariable`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk#getfeaturevariable)
  - [`getActiveFeatures`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk#getactivefeatures)
  - [`getFeatureVariationVariables`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk#getfeaturevariationvariables)
* Introduced a new `visitorCode` parameter to [`RemoteVisitorDataFilter`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#using-parameters-in-getremotevisitordata). This parameter determines whether to use the `visitorCode` from the most recent previous visit instead of the current `visitorCode`. When enabled, this feature allows visitor exposure to be based on the retrieved `visitorCode`, facilitating [cross-device reconciliation](https://developers.kameleoon.com/core-concepts/cross-device-experimentation/). Default value of the parameter is `true`.
* Mapping identifier is now persistent, enabling the assigned variation for a visitor to be retained when [merging sessions](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#using-custom-data-for-session-merging) between anonymous and registered users.
* A new version of the [`isFeatureActive`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#isfeatureactive) method now includes an optional `track` parameter, which controls whether the assigned variation is tracked (default: `true`).
* Enhanced [logging](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#logging):
    - Introduced [log levels](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#log-levels):
        - `none`
        - `error`
        - `warning`
        - `info`
        - `debug`
    - Added support for [custom logger](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#custom-handling-of-logs) implementations.
* Enhanced tracking to consolidate multiple requests into a single one, combining visitor information and sending it once per interval.
* Added a new variation of the [`flush`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#flush) with `instant` parameter. If the parameter's value is `true` the visitor's data is tracked instantly. Otherwise, the visitor's data will be tracked with the next tracking interval. Default value of the parameter is `false`.
* Added new configuration parameter `trackingIntervalMilliseconds` to [`KameleoonClientConfig`](https://developers.kameleoon.com/flutter-sdk.html#initialize-the-kameleoon-client), which is used to set interval for tracking requests. Default value is `1000` milliseconds.
* Added the [`getVisitorCode`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#getvisitorcode) method, which returns the unique visitor code used within [`KameleoonClient`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#initialize-the-kameleoon-client).

## 3.1.1 - 2024-10-30
### Bug fixes
* Addressed an issue preventing the SDK from compiling when building the project with JDK 17.

## 3.1.0 - 2024-10-09
### Features
* The minimum supported Android version for the SDK has been designated as API level 21. This implies that the SDK is compatible with devices running Android 5.0 (Lollipop) and above. By setting the minimum supported version to API level 21, the SDK ensures compatibility with a wide range of Android devices, allowing developers to target a significant portion of the Android user base.

## 3.0.0 - 2024-07-23
### Breaking changes
* Removed the `visitorCode` parameter from all methods that accepted it. You must now specify the visitor code during initialization. As a result, a `KameleoonClient` instance only works for a single visitor:
  - [`addData`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#adddata)
  - [`flush`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#flush)
  - [`isFeatureActive`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#isfeatureactive)
  - [`getFeatureVariationKey`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#getfeaturevariationkey)
  - [`getFeatureVariable`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#getfeaturevariable)
  - [`trackConversion`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#trackconversion)
  - [`getFeatureListActive`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#getFeatureListActive)
* Removed all deprecated methods and exceptions related to **experiments**:
  - `triggerExperiment`
  - `getVariationAssociatedData` (`obtainVariationAssociatedData`)
  - `getExperimentList` (`obtainExperimentList`)
  - `getExperimentListForVisitor` (`obtainExperimentListForVisitor`)
  - `ExperimentConfigurationNotFound`
  - `NotTargeted`
  - `NotAllocated`
  - `SiteCodeDisabled`
* Changed the following classes, methods, fields and exceptions:
  * Classes:
    - Renamed `KameleoonConfiguraton` to [`KameleoonClientConfig`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#initialize-the-kameleoon-client).
    - Renamed enum values of `Devices` class:
        - `Devices.PHONE` renamed to `Devices.phone`
        - `Devices.TABLET` renamed to `Devices.tablet`
        - `Devices.DESKTOP` renamed to `Devices.desktop`
    - Renamed enum values of `Browsers` class:
        - `Browsers.CHROME` renamed to `Browsers.chrome`
        - `Browsers.INTERNET_EXPLORER` renamed to `Browsers.internetExplorer`
        - `Browsers.FIREFOX` renamed to `Browsers.firefox`
        - `Browsers.SAFARI` renamed to `Browsers.safari`
        - `Browsers.OPERA` renamed to `Browsers.opera`
        - `Browsers.OTHER` renamed to `Browsers.other`
    - `CustomData` now accepts a list of strings, instead of a single string, for enhanced flexibility and usability.
  * Methods:
    - Removed `obtainFeatureVariable`.
    - Removed `retrieveDataFromRemoteSource`.
    - Removed `getVisitorCode`.
    - Renamed `getFeatureAllVariables` to [`getFeatureVariationVariables`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#getfeaturevariationvariables).
    - Renamed `getActiveFeatureListForVisitorCode` to [`getActiveFeatures`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#getactivefeatures).
    - Renamed `updateConfigurationHandler` to [`onUpdateConfiguration`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#onupdateconfiguration).
    - Changed `revenue` argument to optional in the [`trackConversion`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#trackconversion) method. Also, the type of `revenue` was changed to `float`.
    - For the [`runWhenReady`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#runwhenready) method, the `readyCallback` and `failCallback` combined into the single `Function(bool)` callback.
    - For the [`onUpdateConfiguration`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#onupdateconfiguration) method, the `Function` callback changed to `Function(int)` where parameter represents the value of Unix time (number of seconds that have elapsed since January 1, 1970) when configuration was updated
  * Exceptions:
    - Removed `CredentialsNotFound` (the `clientId` and `clientSecret` credentials are now optional).
    - Renamed `VisitorCodeNotValid` to `VisitorCodeInvalid`.
    - Renamed `VariationNotFound` to `FeatureVariationNotFound`.
    - Renamed `VariableNotFound` to `FeatureVariableNotFound`.
  * Added new exception [`SiteCodeIsEmpty`] for the method [`KameleoonClientFactory.create`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#create) that indicates the provided `siteCode` is empty.
  * Added new exception `FeatureEnvironmentDisabled` indicating that the feature flag is disabled for certain environments. The following methods can throw the new exception:
      - [`getFeatureVariationKey`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#getfeaturevariationkey)
      - [`getFeatureVariable`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#getfeaturevariable)
      - [`getFeatureVariationVariables`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#getfeaturevariationvariables)

### Features
* Upgraded Flutter SDK library to use [`iOS SDK 4.4.2`](https://github.com/Kameleoon/client-swift/blob/main/CHANGELOG.md) / [`Android SDK 4.2.1`](https://github.com/Kameleoon/client-android/blob/main/CHANGELOG.md) / [`JS/TS SDK 3.4.2`](https://github.com/Kameleoon/client-js/blob/main/CHANGELOG.md)
* Added the [`setLegalConsent`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#setlegalconsent) method to determine the types data that Kameleoon includes in tracking requests. This helps you adhere to legal and regulatory requirements while responsibly managing visitor data. You can find more information in the [Consent management policy](https://help.kameleoon.com/consent-management-policy/).
* [`KameleoonClientFactory.create`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#create) method accepts `visitorCode` as a parameter to use for all SDK methods. If you omit the `visitorCode`, the SDK generates a new visitor code value that it uses until you overwrite it. To overwrite a `visitorCode`, provide it as a parameter explicitly to the method. The method throws `VisitorCodeInvalid` if the provided `visitorCode` is invalid (empty or longer than 255 characters).
* Added new configuration fields to [`KameleoonClientConfig`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#initialize-the-kameleoon-client) and external [configuration](https://developers.kameleoon.com/flutter-sdk.html#additional-configuration) file:
    - `defaultTimeoutMilliseconds` which specifies the time interval, in milliseconds, that it takes for network requests from the SDK to time out. If not provided, the default value is `10_000` ms.
    - `dataExpirationIntervalMinutes` specifies the time (in minutes) that the SDK retains the visitor's data on the device. By default, the TTL (time to live) is `Integer.MAX_VALUE`.
    - `isUniqueIdentifier` that provides additional capabilities with [cross-device experimentation](https://developers.kameleoon.com/core-concepts/cross-device-experimentation) for the [`KameleoonClientConfig`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#create).
* Changed the `key` parameter in the [`getRemoteData`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#getremotedata) method from required to optional. If you don't provide a `key` parameter, the SDK uses the `visitorCode` specified during initialization.
* Added new targeting conditions (some conditions require you to pre-load data with [`getRemoteVisitorData`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk#getremotevisitordata))
  - Operating System
  - IP Geolocation
  - Kameleoon Segment
  - Target Feature Flag
  - Time since First Visit
  - Time since Last Visit
  - Number of Visits Today
  - Total Number of Visits
  - New or Returning Visitor
  - Likelihood to convert
* Added new Kameleoon Data type:
  - [`Geolocation`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk#geolocation)
* Added the [`getActiveFeatures`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#getactivefeatures) method, which retrieves information about the active feature flags that are available for a specific visitor code. This method replaces the deprecated `getActiveFeatureListForVisitorCode` method.
* Added methods for obtaining remote visitor data:
    - [`getVisitorWarehouseAudience`](https://developers.kameleoon.com/flutter-sdk.html#getvisitorwarehouseaudience) method to retrieve all data associated with a visitor's warehouse audiences and adds it to the visitor.
    - [`getRemoteVisitorData`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#getremotevisitordata) fetches the remote visitor's data (with an optional capability to add the data for the visitor).

### Bug Fixes
* Stability and performance improvements.

## 2.0.2 - 2023-09-06
### Features
* Changed the `KameleoonClientConfig` parameters `clientId` and `clientSecret` and the external configuration file parameters, `client_id` and `client_secret` from required to optional. This means you can now successfully initialize a configuration without providing credentials. Previously, you would receive a `credentialsNotFound` exception.
* Added new conditions for targeting:
    - Visitor Code
    - SDK Language
    - [Device](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#device)
    - [Conversion](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#trackconversion)
    - [`Page Title & Page Url`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#pageview) [Available only for web]
    - [`Browser`](https://developers.kameleoon.com/feature-management-and-experimentation/mobile-sdks/flutter-sdk/#browser) [Available only for web]
* Upgraded Flutter SDK library to use [`iOS SDK 3.0.6`](https://github.com/Kameleoon/client-swift/blob/main/CHANGELOG.md) / [`Android SDK 3.2.1`](https://github.com/Kameleoon/client-android/blob/main/CHANGELOG.md) / [`JS/TS SDK 1.7.2`](https://github.com/Kameleoon/client-js/blob/main/CHANGELOG.md)

## 2.0.1 - 2023-06-08
* Upgraded Flutter SDK library to use [`iOS SDK 3.0.3`](https://github.com/Kameleoon/client-swift/blob/main/CHANGELOG.md)

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
    - [`getFeatureList`](https://developers.kameleoon.com/flutter-sdk.html#getfeaturelist)
    - [`getFeatureListActive`](https://developers.kameleoon.com/flutter-sdk.html#getfeaturelistactive)
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
    - Added KameleoonData [`Device`](https://developers.kameleoon.com/flutter-sdk.html#device) class. Possible values are: **PHONE**, **TABLET**, **DESKTOP**.
    - Removed the KameleoonData `Interest` class.

# Unsupported versions:

## 1.0.3 - 2022-05-31 `[Deprecated]`
* Added method for retrieving data from remote source: [`retrieveDataFromRemoteSource`](https://developers.kameleoon.com/flutter-sdk.html#retrievedatafromremotesource)
* Added support of multi-environment for feature flags, Related to [`activateFeature`](https://developers.kameleoon.com/flutter-sdk.html#activatefeature), [`obtainFeatureVariable`](https://developers.kameleoon.com/flutter-sdk.html#obtainfeaturevariable)
* Updated Flutter SDK library to iOS 2.0.15 / Android 2.0.13 / JS 1.0.7

## 1.0.2 - 2021-11-03 `[Deprecated]`
* Added scheduling feature
* Refactoring structure of library
* Updated Flutter SDK library to iOS 2.0.12 / Android 2.0.10 / JS 1.0.5

## 1.0.1 `[Deprecated]`
* Add Web platform
* Update Flutter SDK library to iOS 2.0.11 / Android 2.0.9

## 1.0.0 `[Deprecated]`
* Release

## 0.0.3 `[Deprecated]`
* Implement null-safety

## 0.0.2 `[Deprecated]`
* Implement iOS bridge

## 0.0.1 `[Deprecated]`
* Implement Android bridge
