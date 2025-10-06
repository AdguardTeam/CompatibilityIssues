
# Compatibility issues

This is a repo for listing all kinds of compatibility issues that we maintain for AdGuard apps.

This repository contains lists of filtering exclusions and inclusions for applications and IP ranges. Information from this repo is automatically built into the versions of AdGuard apps.

## Why exclude apps from filtering?

Although we strive to maintain a high quality of filtering primarily through rules (see [AdguardFilters](https://github.com/AdguardTeam/AdguardFilters) repo), in specific cases, rules may not be enough. Some applications do not allow their traffic to be filtered, which leads to them malfunctioning. We carefully investigate such cases and add the identifier of the problematic app to the corresponding list.

## What AdGuard applications use these filtering lists?

Currently, they apply to AdGuard for Android.

## How do these lists get updated in the AdGuard apps?

The lists get updated automatically when a new version of the app is released. For the new version, current filtering lists from this repository are fetched and set as default.

When you update AdGuard, the applications filtering settings will be updated unless you modified them before. If you have made changes to them, you won't get any updates.

## Can I contribute to these lists?

We deeply appreciate and value community contributions. You can contribute by creating an issue or opening a pull request in this repository.

## How to know if an app should be added to lists from this repository?

An app is a good candidate for the filtering exclusions list when it experiences issues with AdGuard that cannot be resolved using standard filter lists from the [AdguardFilters](https://github.com/AdguardTeam/AdguardFilters) repo.

This primarily includes apps that use SSL pinning, a technique to verify that the server's certificate is the one expected by the app. Filtering traffic could interfere with this process, causing these apps to malfunction or detect potential security threats.

Another common reason is that the problematic app relies on QUIC traffic. Filtering QUIC traffic cannot be managed by regular filter lists and requires the use of lists from this repository.

## How to troubleshoot compatibility issues?

Here’s a simple steps to help you sort things out.

1. Make sure the traffic isn’t being blocked by one of the filters in the AdGuard app. To do this, check the blocked requests of the problematic app in the Filtering log and temporarily disable all filters listed in the request details as the blocking source. Then test again: does the issue still occur with those filters disabled? If resolved, please report by creating a new issue in the [AdguardFilters](https://github.com/AdguardTeam/AdguardFilters) repository.

2. Try temporarily disabling the Tracking Protection module and check the issue again. If that helps, you can solve it by creating an [allowing rule with the `$stealth` modifier](https://adguard.com/kb/general/ad-filtering/create-own-filters/#stealth-modifier). Then open a new issue in the [AdguardFilters](https://github.com/AdguardTeam/AdguardFilters) repository.

3. Confirm that the traffic isn’t being blocked by your filtering DNS server. Switch to `Automatic DNS` or another non-filtering DNS and see if the problem persists.

4. Check whether QUIC blocking might be the cause of the compatibility issue. A common symptom of QUIC-related problems is that images or video content won’t load. Add the app to the QUIC bypass packages list in AdGuard and see if that resolves the problem. Open a new issue or pull request in this repository if it does.

5. If you’re using the Proxy module, temporarily disable it to make sure the compatibility issue isn’t caused by the proxy.

6. If the app relies on SSL pinning, it may not function correctly when its traffic is being filtered. In that case, try disabling filtering for this app in AdGuard. If that resolves the problem, let us know by creating a new issue in this repository.

> [!TIP]
> To check whether the app is using SSL pinning, close AdGuard and route its traffic through [mitmproxy](https://www.mitmproxy.org). Try to reproduce the problem. If you see entries in the mitmproxy Event Log such as:
`Client TLS handshake failed. The client does not trust the proxy's certificate for example.com (OpenSSL Error([('SSL routines', '', 'ssl/tls alert certificate unknown')]))`
— that indicates SSL pinning is in use.

&nbsp;

## Compatibility configuration for AdGuard for Android

- [`filter_traffic_exclusions.json`](android/filter_traffic_exclusions.json) - A list of app package names where routing through AdGuard is disabled by default (App Management -> Route traffic through AdGuard).

- [`block_ads_exclusions.json`](android/block_ads_exclusions.json) - A list of app package names where traffic filtering is disabled by default (App Management -> Filter traffic).

- [`filter_https_traffic_exclusions.json`](android/filter_https_traffic_exclusions.json) - A list of app package names where HTTPS filtering is disabled by default, even on rooted devices (App Management -> Filter HTTPS traffic).

- [`filter_https_traffic_inclusions.txt`](android/filter_https_traffic_inclusions.txt) - A list of app package names where HTTPS filtering is enabled by default, including non-rooted devices (App Management -> Filter HTTPS traffic).

- [`filter_https_traffic_inclusions_problematic_devices.txt`](android/filter_https_traffic_inclusions_problematic_devices.txt) - A special list of app package names where HTTPS filtering is enabled by default, including non-rooted devices. It is applied on problematic devices instead of the standard 'filter_https_traffic_inclusions.txt' (App Management -> Filter HTTPS traffic).

- [`browsers.txt`](android/browsers.txt) - A list of browsers where traffic filtering is enabled with the free version of AdGuard.

- [`pkg_exclusions.txt`](android/pkg_exclusions.txt) - A list of apps excluded from routing completely. It supports exclusions by package names and reserved UIDs (Low-level settings -> Excluded apps).

- [`quic_pkg_exclusions.txt`](android/quic_pkg_exclusions.txt) - A list of app package names where QUIC traffic is allowed (Low-level settings -> QUIC bypass packages).

- [`ipv4_routes_exclusions.txt`](android/routes_exclusions/ipv4_routes_exclusions.txt) - A list of IPv4 ranges excluded from routing.

- [`ipv4_routes_exclusions_fujitsu.txt`](android/routes_exclusions/ipv4_routes_exclusions_fujitsu.txt) - A list of IPv4 ranges excluded from routing on problematic devices. This list applies on Fujitsu devices: F-01J, F-01K, F-01L, F-02H, F-03H, F-03K, F-04H, F-04K.

- [`ipv6_routes_exclusions.txt`](android/routes_exclusions/ipv6_routes_exclusions.txt) - A list of IPv6 ranges excluded from routing.
