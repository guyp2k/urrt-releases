# urrt

An Android remote for Unraid servers: server health at a glance (a green, amber or red card that takes you to whatever needs attention), live network speeds, Docker containers and VMs you can start and stop, storage, drive temperatures and parity checks, a UPS card, the server's logs, and notifications. It uses your own server's official Unraid API: no account, no cloud relay, no tracking.

This repository holds signed release builds only.

<p>
<img src="screenshots/home.png" width="220" alt="Home: a green Healthy server card, icon stats, CPU and RAM gauges, storage, apps, network speeds and UPS">
<img src="screenshots/health.png" width="220" alt="Home: an amber Warning card listing its reasons, each one opening the screen that deals with it">
<img src="screenshots/docker.png" width="220" alt="Docker: containers with live CPU and memory">
<img src="screenshots/vms.png" width="220" alt="VMs: actions valid for each VM's state">
<img src="screenshots/storage.png" width="220" alt="Storage: pools with their drives and temperatures, and the parity check">
<img src="screenshots/network.png" width="220" alt="Network: every interface with live speeds, totals and drops">
<img src="screenshots/logs.png" width="220" alt="Server logs: syslog followed live">
</p>

Screenshots show a demo server.

## Install

1. On your Android phone, open the latest release: **https://github.com/guyp2k/urrt-releases/releases/latest** and download `urrt-<version>.apk`.
2. Open the file. Android asks you to allow installs from your browser or file manager the first time. Allow it, then install.
3. Open urrt, tap **Add server**, and enter your Unraid server's address. Use **Sign in with Unraid**, or paste an API key from the webGUI (Settings > Management Access > API Keys).

Requirements: Android 7.0 or newer; Unraid 7.2 or newer (the API is built in).

## Check the download (optional)

Every release is signed with the same key. Its certificate's SHA-256 fingerprint is:

```
A4:5F:81:A9:9E:85:14:A4:14:EE:91:7B:AD:19:CC:64:A7:22:D1:89:8A:2F:5B:5B:55:3A:CB:A1:B8:D4:7A:19
```

With the Android SDK: `apksigner verify --print-certs urrt-<version>.apk`. The `SHA-256 digest` line must match. Each release also lists the APK's SHA-256 checksum.

## Privacy

- urrt connects to the Unraid servers you add and to the hosts that container icons point to. It has no account, cloud relay, analytics, crash reporting or ads.
- Each server's API key, address and pinned certificate are kept in Android's encrypted storage on your phone and sent only to that server.
- Container icons load from wherever each container's template points (usually GitHub). Those hosts see your phone's IP address and which icons it asks for.
- With app lock on, urrt hides its screen from the recent-apps view.

## Good to know

- **Health card:** the server card on Home is green when all is well, amber for warnings (stale data, a stopped or rebuilding array, disk errors, hot drives, unread warnings, UPS on battery) and red for problems (array fault, disabled or missing disk, a drive at its limit, unread alerts, UPS low battery). It has no colour when urrt cannot read enough to judge. Tap it to go where the reason is handled: Notifications for unread alerts and warnings (archive them there), Storage for disks and drive temperatures.

- **UPS card:** shown only when the UPS is set up in Unraid's UPS Settings (apcupsd). The Unraid API does not report a UPS monitored through the NUT plugin (requested upstream: https://github.com/unraid/api/issues/2115).
- **Parity controls:** Check, Check and Correct, Pause, Resume and Cancel appear only on arrays with a parity disk. They have been tested against the API's replies but not yet on a real array, so use them with care.
- **VM Shut down:** Unraid asks the guest to shut down, waits about 10 seconds, then cuts power. Shut down slow guests (Windows, Home Assistant OS mid-update) from inside the VM.
