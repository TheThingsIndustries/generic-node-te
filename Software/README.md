# GNTE Software

The software uses `Make` and `arm-none-eabi-gcc` toolchain.

## Documentation

The [Generic Node documentation website](https://www.genericnode.com/docs/) provides information about the software features and how to [get started with the software development](https://www.genericnode.com/docs/getting-started/se-sw/).

## Requirements

- [MAKE](https://www.gnu.org/software/make/) or [MinGW](https://osdn.net/projects/mingw/releases/) for `Windows` environments
- [arm-none-eabi-gcc](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads)

## Set-up

1. Clone project & checkout `develop` branch
```
$ git clone --branch develop https://github.com/TheThingsIndustries/generic-node-te.git
```
2. Install [MinGW](http://mingw.org) for Windows environment and make sure `mingw32-make.exe` can be used from cmd (as a recognized command)
3. Configure which application to build [Makefile](./gcc/Makefile), by default `TRACKER_APP = 1`
4. Configure the region, by default `USE_REGION_868 = 1`
5. Configure your EUIs and Keys in [LoRaWAN](./Src/apps/LoRaWAN/Commissioning.h) and [Tracker](./Src/apps/Tracker/Commissioning_tracker.h) applications
6. Set `GCC_PATH` in [Makefile](./gcc/Makefile) and run `make` command inside the [gcc](./gcc) folder or pass it directly `make GCC_PATH=xxx`

## Applications

- [gnss_test](./Src/apps/gnss_test) is a simple GNSS example
The unix date in ASCII is set in the application, it executes a GNSS scan periodically according to the gnss settings defined in the application.

- [wifi_test](./Src/apps/wifi_test) is a simple Wi-Fi example
The modem executes a Wi-Fi scan periodically according to the Wi-Fi settings defined in the application.

- [LORAWAN](./Src/apps/LoRaWAN) is a simple LoRaWAN Class A application 868/915 MHz
The app joins automatically the LoRa Network server then sends uplinks periodically with the interval defined by APP_TX_DUTYCYCLE.

- [Tracker](./Src/apps/Tracker) is a simple Tracker example
The app joins automatically the network then periodically performs a clock sync, a Wi-Fi Scan
and a GNSS scan and stream the scan results.

> Please note that you can use the Semtech Join Server keys derivation algorithm by updating the `USE_SEMTECH_JOIN_SERVER` flag in the [LoRaWAN](./Src/apps/LoRaWAN/Commissioning.h) and [Tracker](./Src/apps/Tracker/Commissioning_tracker.h) applications.

> Also, to use the LR1110 modem production keys : update the `USE_PRODUCTION_KEYS` flag in [LoRaWAN](./Src/apps/LoRaWAN/main_lorawan.c) and [Tracker](./Src/apps/Tracker/main_tracker.c) applications.
