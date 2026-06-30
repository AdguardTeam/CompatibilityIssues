The `mac` folder contains the `processes.json` and `browsers.json` files, which configure application filtering and list the browsers supported by the AdGuard browser extension.
AdGuard for Mac loads these files from its application bundle, but for testing purposes, you can place them in the same folder as the `DevConfig.json` file (i.e. `/Library/Application Support/AdGuard Software/<APP_BUNDLE_ID>`) and AdGuard for Mac will use those copies instead.
This feature is available starting with AdGuard for Mac version 2.20.0.

# processes.json File Format

## Purpose

This file defines the list of applications whose traffic AdGuard should filter.


## Top Level

A **JSON array** of objects, each describing a single application:

```json
[ { ... }, { ... }, ... ]
```


## Object Fields

| Field                   | Type       | Required | Description                                                                                                                                       |
|-------------------------|------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| `bundleId`              | `String`   | ✓        | Bundle ID of the main application — unique identifier for the record                                                                              |
| `enabled`               | `Bool`     | ✓        | Whether filtering is enabled by default for this application                                                                                      |
| `filteringBundleIds`    | `[String]` | ✗        | Bundle IDs of **all processes** of the application to filter (main + helper, renderer, plugin, GPU, etc.)                                         |
| `filteringProcessNames` | `[String]` | ✗        | Process names to filter in the kernel extension filtering mode (it is going to be deprecated, maybe)                                              |
| `filteringHosts`        | `[String]` | ✗        | List of `"ip:port"` destination hosts, if set, only **specific hosts** are filtered for the given Bundle ID (rather than all application traffic) |


## Example Entry

```json
{
  "bundleId": "org.torproject.torbrowser",
  "enabled": false,
  "filteringBundleIds": [
    "org.torproject.torbrowser"
  ],
  "filteringHosts": [
    "127.0.0.1:9150"
  ],
  "filteringProcessNames": [
    "firefox"
  ]
}
```

# browsers.json File Format

## Purpose

This file defines the list of browsers known to AdGuard for Mac, along with the metadata needed to locate browser profiles and native messaging host directories.


## Top Level

A **JSON array** of objects, each describing a single browser:

```json
[ { ... }, { ... }, ... ]
```


## Object Fields

| Field                  | Type     | Required | Description                                                                                      |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------|
| `bundleId`             | `String` | ✓        | Browser application bundle ID                                                                    |
| `kind`                 | `String` | ✓        | Browser engine family: `chrome`, `edge`, or `gecko`                                              |
| `name`                 | `String` | ✓        | Browser application name                                                                         |
| `profilesFolder`       | `String` | ✓        | Path to the browser profile data directory relative to `~/Library/Application Support`           |
| `nativeMessaging`      | `String` | ✓        | Path to the browser native messaging hosts directory relative to `~/Library/Application Support` |
| `needsHttpsWorkaround` | `Bool`   |          | Does HTTPS support need a workaround? [1]                                                        |

[1]: For now, this flag is only relevant for Gecko-like browsers. Some of them (e.g. Tor Browser) require `security.enterprise_roots.enabled` and `security.cert_pinning.enforcement_level` to be set to allow AdGuard for Mac to handle HTTPS connections.


## Example Entry

```json
{
  "bundleId": "com.google.Chrome",
  "kind": "chrome",
  "name": "Google Chrome",
  "profilesFolder": "Google/Chrome/",
  "nativeMessaging": "Google/Chrome/NativeMessagingHosts"
}
```
