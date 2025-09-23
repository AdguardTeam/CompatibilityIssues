&nbsp;

# Compatibility issues

This is a repo for listing all kinds of compatibility issues that we maintain for AdGuard apps. 

This repository contains lists of exclusions and inclusions with entries for package names, UIDs, and IP ranges. Information from this repo is automatically built into the versions of AdGuard apps. 

## Why exclude apps from filtering?

Although we strive to maintain a high quality of filtering primarily through rules (see https://github.com/AdguardTeam/AdguardFilters), in specific cases, rules may not be enough. Some applications do not allow their traffic to be filtered, which leads to them malfunctioning. We carefully investigate such cases and add the identifier of the problematic app to the corresponding list. 

## What AdGuard applications use these filtering lists?

Currently, they apply to AdGuard for Android.

## How do these lists get updated in the AdGuard apps?

The lists get updated automatically when a new version of the app is released. For the new version, current filtering lists from this repository are fetched and set as default.

When you update AdGuard, the applications filtering settings will be updated unless you modified them before. If you have made changes to them, you won't get any updates.

## Can I contribute to these lists?

We deeply appreciate and value community contributions. You can contribute by creating an issue or opening a pull request in this repository.

### Filtering lists for Android  

#### App Management tab

`filter_traffic_exclusions.json` - A list of app package names where routing through AdGuard is disabled by default (App Management -> Route traffic through AdGuard).

`block_ads_exclusions.json` - A list of app package names where traffic filtering is disabled by default (App Management -> Filter traffic).

`filter_https_traffic_exclusions.json` - A list of app package names where HTTPS filtering is disabled by default, even on rooted devices (App Management -> Filter HTTPS traffic).

`filter_https_traffic_inclusions.txt` - A list of app package names where HTTPS filtering is enabled by default, including non-rooted devices (App Management -> Filter HTTPS traffic).

`filter_https_traffic_inclusions_problematic_devices.txt` - A special list of app package names where HTTPS filtering is enabled by default, including non-rooted devices. It is applied on problematic devices instead of the standard 'filter_https_traffic_inclusions.txt' (App Management -> Filter HTTPS traffic).

`browsers.txt` - A list of browsers where traffic filtering is enabled with the free version of AdGuard.

#### Low-level settings

`pkg_exclusions.txt` - A list of apps excluded from routing completely. It supports exclusions by package names and reserved UIDs (Low-level settings -> Excluded apps).

`quic_pkg_exclusions.txt` - A list of app package names where QUIC traffic is allowed (Low-level settings -> QUIC bypass packages).

`ipv4_routes_exclusions.txt` - A list of IPv4 ranges excluded from routing. 

`ipv4_routes_exclusions_fujitsu.txt` - A list of IPv4 ranges excluded from routing on problematic devices. This list applies on Fujitsu devices: F-01J, F-01K, F-01L, F-02H, F-03H, F-03K, F-04H, F-04K. 

`ipv6_routes_exclusions.txt` - A list of IPv6 ranges excluded from routing. 

