# Ariya Monitor (public edition)

🇯🇵 **日本語: [README.md](README.md)**

> **Support is available in Japanese only.** Release notes and the report form are in Japanese too. This English page and the English app screens are provided as-is for people who can find their way around.

An Android app that reads battery status and other data from the Nissan Ariya's OBD2 port and shows it on screen.
**This is an unofficial app made by an individual. It is not affiliated with Nissan.**

> ⚠️ **This is a trial release.** It has been tested only on the author's own car (a Japanese-market Ariya). Depending on model year, grade or market, some values may not appear or may be wrong. Ariyas sold outside Japan have not been tested at all.

## Download

👉 Open the **[latest release page (Releases)](../../releases/latest)** and download `ariyamonitor-public-x.y.z.apk`.

> 📱 A **[Lite edition](https://github.com/kojipa/ariyamonitor-lite-releases)** is also available for Android 5–7 or slower devices (Japanese screens only).

### Switching the app to English

The app starts in Japanese on a Japanese device and in English on any other device language. To change it, open **Settings → Display → Language / 言語** and choose **Match device**, **日本語** or **English** (v0.4.0 or later).

If the app is showing Japanese: tap **設定** (Settings), then the **表示** (Display) tab, then choose **English** under **Language / 言語**.

## What it does

- **Home**: Shows the SOC held by the battery management computer (BMS; "Real SOC") in large type, and the car's SOC that is close to the meter's % (shown as "METER") in small type. "METER" is not the meter display itself, so it can differ slightly (e.g. 99.28% when the meter shows 100%). Real SOC can go slightly above 100% when fully charged; the screen shows up to 100%. The flow of electricity (driving, regen, charging) is shown as light effects over the car image. Choose how strong the effects are with **Effects level** (STEALTH / CRUISE / SPORT / OVERDRIVE) in Settings → Display. It also shows tire pressure (all four), outside temp and odometer. The bottom band shows pack voltage, remaining energy, speed and battery temperature with gauges. The number font (Chakra Petch / Standard) and the scrolling background log (events and trip summary) can also be chosen in Settings → Display.
- **List**: A list of battery temperature, coolant temp, pack voltage, current, speed, BMS remaining energy and more.
- **Graph (last 15 minutes)**: Shows how a chosen item has changed, with a scaled graph.
- **Battery**: Maps the voltage of all 96 cells and the module temps (as many as the car reports; 12 on the B6). While parked, a face icon gives a rough health indication based on cell spread and other values. You can also see the estimated 12V battery voltage and a capacity estimate while charging. When it connects, it shows a rough build type (Early build / Revised build or later). Measurement history is stored only on the device. Cell voltage can be shown as a map or as a bar graph.
- **Charging (charge history)**: Records each charging session on the device and lists time, SOC change, energy charged (approximate), power and temperature. Tap one to see its charge curve (power, real SOC, battery temperature). Charging with the car switched off is recorded too, as long as the app is running.
- **Auto-connect**: The app connects to the OBD2 adapter automatically when it starts. With Bluetooth (classic) adapters it tries three ways of connecting and remembers the one that works. Wi-Fi adapters (v0.3.9 or later) and BLE adapters (v0.4.0 or later) are supported too. If it can't connect, it shows why (Bluetooth is off, the adapter's Wi-Fi isn't found, the adapter can't be reached, the car doesn't respond, and so on).
- **English screens**: Switch the screens to English with **Language** in Settings → Display (v0.4.0 or later).
- **Keep screen on**: Stops the screen from turning off while the app is shown (Off / While reading / Always; the default is While reading).

Some items (current, SOH, high-precision current, charge power), the battery screen's diagnosis and capacity estimate, and the trip summary in the log are **approximate (unofficial)**. Their accuracy hasn't been fully verified even on the author's car, so treat them as a rough guide.

## Safety

- **The app sends only read commands to the car.** It has no function to write, reset ECUs or clear trouble codes. It reads from the battery-related ECUs, the meter (tire pressure, odometer) and the climate control (outside temp). Tire pressure and similar values are read only once a minute while driving.
- If the car is parked, not charging, and almost no current flows for 10 minutes, reading stops automatically (to protect the 12V battery).
- Vehicle data is never sent anywhere. There is no account or sign-up.
- The only network access is a check, once a day, for a newer version on this page. You can turn it off in Settings.
- Location is not used, with one exception: **on Android 11 or older, when you choose a BLE adapter**, the system may require location permission to search for it. It is used only to find the adapter; your location is never recorded or sent. It is not requested on Android 12 or later, or for Bluetooth (classic) and Wi-Fi adapters.

## Requirements

| Item | Requirement |
|---|---|
| Car | Nissan Ariya |
| Android | 8.0 or later (a phone, or an Android device such as a CarPlay AI box) |
| OBD2 adapter | An **ELM327-compatible** adapter connecting over **Bluetooth (classic / SPP)**, **Bluetooth Low Energy (BLE)** or **Wi-Fi** |

- Pair a Bluetooth (classic) adapter first in Android's Settings → Bluetooth (the PIN is usually `1234` or `0000`). BLE adapters need no pairing; you choose them inside the app.
- Wi-Fi adapters without a password (the kind that creates its own Wi-Fi network) are supported. While connected, the device's Wi-Fi is used only for the adapter (on Android 10 or later, other traffic keeps using mobile data. Head units that get internet through Wi-Fi tethering lose internet while connected).

## Installing

1. Download the APK from the latest release page in your Android browser.
2. Open the downloaded file.
3. If asked "Allow apps from this source?", **allow** it, go back and install.
4. A **Google Play Protect** warning may appear, because the app isn't distributed through Google Play.
   - Choose "Install without scanning", or "More details" → "Install anyway".

## How to use

1. Turn on the car and plug in the OBD2 adapter.
2. Start the app, read the notice and press **Agree and start**.
3. In **Settings → Connection → Adapter**, press **Change** and choose the adapter you use (Bluetooth / BLE / Wi-Fi).
   - For a BLE adapter, press **Find BLE adapter** and choose the one found (e.g. `OBD BLE`). Adapters that support both Bluetooth classic and BLE connect over only one of them at a time; to use BLE, don't pair the classic side in the device's Bluetooth settings.
   - For a Wi-Fi adapter, leave SSID, address and port blank and it is found automatically. On Android 10 or later, press **Choose the adapter Wi-Fi (first time only)** in the Wi-Fi adapter settings and pick the adapter's Wi-Fi (e.g. `WiFi-OBDII`) once; from then on it connects without the "Connect to device" screen (if you skip this, or the saved adapter isn't found, that screen appears each time you connect). On Android 9 or older, connect to the adapter's Wi-Fi in the device's Wi-Fi settings first.
4. Press **Connect**. Values appear on Home within a few seconds to a few dozen seconds. From then on, it connects automatically when the app starts.

If the Home effects don't appear or stay at CRUISE, turn off "Remove animations" on the device, or set "Animator duration scale" in Developer options to 1x (the log display also doesn't appear while animations are off).

If it won't connect, try these in order: unplug and replug the adapter, turn the car off and on again, close other OBD apps (such as Car Scanner). An adapter can be used by only one app at a time. If a Wi-Fi adapter isn't found, check that it appears in the device's Wi-Fi list (some adapters use channels such as 13 that the device may not see easily).

If it still won't connect, or values look wrong, turn on **Record debug log** in Settings → Other, connect, and then send it from **Report a problem / request** (copy the debug log with **[Copy]** on the Debug log screen and paste it. It is encrypted and only the author can read it). Requests for the app go through the same form. **The form and replies are in Japanese only.**

## Updates

When a new version is released, the app shows a "new version" notice once. Open **Settings → Other → App updates** and press **View on GitHub** to open this page, then download the new APK and install it over the old one. Your settings are kept. Release notes are written in Japanese.

## Disclaimer

- This app comes with no warranty. The accuracy of the values shown is not guaranteed.
- The author is not responsible for any damage resulting from its use. Use it at your own risk.
- **Do not operate the screen while driving.**
- "ARIYA" and "Nissan" are trademarks of Nissan Motor Co., Ltd. This app is not provided or endorsed by Nissan Motor Co., Ltd.
