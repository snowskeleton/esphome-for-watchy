# ESPHome-for-Watchy

Watchy is an open-hardware, ESP32 wrist watch with e-paper display designed by SQFMI.

https://watchy.sqfmi.com/

https://watchy.sqfmi.com/docs/hardware

This project is a minimal ESPHome configuration file for the Watchy hardware.

https://esphome.io/

It is a complete, self-contained, drop-in replacement for the original firmware.

- v2: [./watchy_v2.yaml](./watchy_v2.yaml) (Ready/Working/Functional)
- v3: [./watchy.yaml](./watchy.yaml) (Work in Progress)

## The Watch

### NEW! Watchy v3

Update: My new v3 module arrived via [Mouser Electronics](https://au.mouser.com/ProductDetail/SQFMI/SQFMI-WATCHY-10?qs=DRkmTr78QARN9VSJRzqRxw%3D%3D). It has hardware changes including ESP32-S3, RTC and rearranged pins.

<div>
<img src="doc/v3/01.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
<img src="doc/v3/02.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
<img src="doc/v3/03.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
<img src="doc/v3/04.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
<img src="doc/v3/05.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
<img src="doc/v3/06.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
<img src="doc/v3/07.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
</div>

TODO:

https://github.com/sqfmi/Watchy/compare/667d86737dd3dcedf67d83cf69553b28f4e1f38b..master

- ESP32-S3 on-board RTC - It works, but how!?
- Battery charge pin and voltage
- Step counter

### v2

Sichiray via AliExpress

<div>
<img src="doc/buttons.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
<img src="doc/02.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
<img src="doc/03.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
<img src="doc/04.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
</div>

## Multiple Faces

<div>
<img src="doc/06.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
<img src="doc/07.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
<img src="doc/08.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
<img src="doc/10.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
<img src="doc/19.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
<img src="doc/14.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
</div>

## Design Philosophy

### Low Power Usage

A low-distraction, low-interaction, unobtrusive and wearable device.

This is primarily a watch, for showing the time, with a few extra "read-only", "at-a-glance" watch-like complications such as a weather forecast.

Wifi is utilised primarily for read-only connectivity features such as updating accurate internet time, DST adjustments and a weather forecast. It is a truly "automatic" watch!

Wifi, which uses a lot of power, will only activate automatically 4 times a day.

In the future, I hope to sync with a calendar once a day.

### Interactivity

Interactive features such as the stop-watch and Home Assistant (or MQTT) controls should be used sparingly because the battery is small and the display is slow.

Multiple buttons and long-press buttons remain free for your own extensions.

### Settings

Intentionally, this project does not include any on-watch settings screens or user-configuration. The idea is that the ESPHome YAML file is simple and easy enough for it to be edited directly, and re-flashed to the ESP32 device. The YAML _is_ the settings UI.

# User Manual

## Buttons

<img src="doc/buttons.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />

### Top Left

- Press: Power On
- 2nd Press: Wifi On
- Long Press (1s): Go to sleep

### Top Right

- Press: Cycle watch faces (digital, hands, roman, info, etc)
- Long Press: Full-refresh ePaper display (this clears away ghost pixels)

### Bottom Left

- Press: Start new timer (and show timers page) (up to 5 timers)
- Long Press (1s): Cancel last active timer
- Long Press (2s): Cancel all tiemrs

### Bottom Right

- Press: Show Home Assistant page (intentionally left unused for custom features)

## Weather

The watch shows a weather forecast over the upcoming 12 hours. This is a simple, practical, human-ergonomics amount of time for planning ahead using a wrist watch.

<div>
<img src="doc/weather01.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
<img src="doc/weather02.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
</div>

## Timers Operation

Press the left-bottom button to show the timers page:

<img src="doc/11.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />

Press the left-bottom button again to start a new timer, added to the bottom (D):

<img src="doc/12.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />

Press again for another timer (E):

<img src="doc/14.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />

Press-and-hold (2s) the left-bottom button to clear all timers and start over:

<img src="doc/15.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />

When the page is full, a button press will discard the oldest timer and start a new one at the bottom. All the other timers move up one slot, maintaining their letter-codes. In this example, A, which has been restarted, moves to the bottom. Then, on another press, B.

<div>
<img src="doc/16.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
<img src="doc/17.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
<img src="doc/18.jpeg" style="width: 240px; max-width: 95vw; max-height: 95vh" />
</div>

## Install / Flash

### Install ESPHome on Mac OSX

https://esphome.io/guides/installing_esphome.html#mac

    brew install esphome
    brew install pillow
    brew unlink pillow

Download:
https://raw.githubusercontent.com/Homebrew/homebrew-core/fc831c5d76dc2eb6dbe2265ca9b6ca93d27140bc/Formula/p/pillow.rb

    brew install ./pillow.rb
    brew pin pillow

### Enter Bootloader Mode

https://watchy.sqfmi.com/docs/getting-started#uploading-new-watchfacesfirmware

To upload new firmware/watchfaces to Watchy, you will need to enter **bootloader** mode

1. Plug in the USB on Watchy
1. Press and hold the top 2 buttons for more than 4 seconds, then release the **Left button first**, before releasing the Up button
1. You should now see an ESP32S3 device enumerate a serial port i.e. COM, cu.\*

### Flash

    esphome -s ID 0 run watchy.yaml

### Reset

1. Press and hold the top 2 buttons for more than 4 seconds, then release the **Right button first**, before releasing the Back button
1. Watchy should now reset, wait a few seconds for it to boot up and refresh the screen
