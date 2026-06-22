# PortBell - Track the journey. Hear the arrival.

Low-power ESP32 desktop vessel tracker with scheduled updates, local status storage, and port approach alerts.

PortBell is a battery-powered desk device that tracks a single ship via AIS data. It is built for following a loved one who works aboard international vessels. The device sleeps most of the time to conserve battery, wakes periodically to silently update the vessel's status, shows the latest status on its screen when you press a button, and chimes on key events (such as the ship mooring at port) without even turning the screen on.

## Features

- **Scheduled silent updates:** wakes on a timer, fetches the latest AIS data, stores it locally, and goes back to sleep without lighting up the screen.
- **On-demand display:** press the button to see the last known position, speed, course, navigational status, destination, ETA, and how long ago the last signal was received.
- **Port approach alerts:** plays a chime when the vessel moors at port, and a different chime when it reappears after a long gap at sea. Quiet hours are configurable so it stays silent overnight.
- **Adaptive sleep:** checks more often near port and less often on the open ocean, backing off automatically when no data is available, to preserve battery.
- **Low power first:** designed to run for weeks on a single 18650 cell.

## Hardware

- Adafruit ESP32-S3 Feather
- 2.8" ILI9341 TFT display
- MAX98357A I2S amplifier + speaker
- 1x button
- 1500 mAh 18650 LiPo battery

## Data Source

PortBell uses [AISStream.io](https://aisstream.io) (free, WebSocket-based) to receive AIS messages filtered by the target vessel's MMSI. A free API key is required.

> **Note:** On the open sea, beyond terrestrial AIS range, a vessel can be invisible for hours or days. This is expected. PortBell shows how long ago the last signal was received and adapts its update schedule accordingly.

## Getting Started

1. Clone this repo and open it with [PlatformIO](https://platformio.org/).
2. Copy `config.example.h` to `config.h` and fill in your Wi-Fi credentials, AISStream API key, target MMSI, quiet hours, and other settings. `config.h` is gitignored so your secrets stay local.
3. Build and upload to the ESP32.

## Configuration

All user-specific and tunable values live in `config.h`, including Wi-Fi credentials, AISStream API key, target MMSI, quiet hours (on/off, start, end, UTC offset), sleep durations, timeouts, display duration, button long-press threshold, sound settings, and pin definitions.

## License

MIT License - see `LICENSE` for details.
