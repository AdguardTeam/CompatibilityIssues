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

| Field             | Type     | Required | Description                                                                                    |
|-------------------|----------|----------|------------------------------------------------------------------------------------------------|
| `bundleId`        | `String` | ✓        | Browser application bundle ID                                                                  |
| `kind`            | `String` | ✓        | Browser engine family: `chrome`, `edge`, or `gecko`                                            |
| `profilesFolder`  | `String` | ✓        | Path to the browser profile data directory relative to ~/Library/Application Support           |
| `nativeMessaging` | `String` | ✓        | Path to the browser native messaging hosts directory relative to ~/Library/Application Support |



## Example Entry

```json
{
  "bundleId": "com.google.Chrome",
  "kind": "chrome",
  "profilesFolder": "Google/Chrome/",
  "nativeMessaging": "Google/Chrome/NativeMessagingHosts"
}
```
