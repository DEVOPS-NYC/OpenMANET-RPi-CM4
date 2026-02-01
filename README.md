# OpenMANET-RPi-CM4
this is a custom firmware version of OpenMANET for the Raspberry Pi CM4

## Tested Hardware
### SBC
| Device            | Status    | Onboard WiFi      | Notes                        |
|-------------------|-----------|-------------------|------------------------------|
| Raspberry Pi CM4  | ✅ Tested | ✅ Working (SPI)  | Onboard Wifi Only in AP Mode |

### HaLow Hardware

| Device              | Status    | Interface  | MM Chipset | Notes                                 | Product Link |
|---------------------|-----------|------------|------------|---------------------------------------|-------------- |
| SeeedStudio WM1302 | ✅ Tested |   SPI      | 6108       | Best performing with HaLow currently  | [WM1302 Module](https://www.seeedstudio.com/WM1302-Pi-Hat-p-4897.html "SeedStudio WM1302 Raspberry Pi Hat") |
| SeeedStudio Wio-WM6108 | ✅ Tested |   SPI      | 6108       | Best performing with HaLow currently  | [Wio-WM6108 Module](https://www.seeedstudio.com/Wio-WM6108-Wi-Fi-HaLow-mini-PCIe-Module-p-6394.html "SeedStudio Wio-WM6108 Module") |

## Building OpenMANET Firmware
### Dependencies

To build the OpenMANET OpenWrt, you need a working Linux environment. This has been tested with Ubuntu 24.04 and higher.

Install build environment packages with
```
> sudo apt update
> sudo apt install build-essential clang flex g++ gawk gcc-multilib g++-multilib git gettext \
  libncurses5-dev libssl-dev python3-setuptools rsync unzip zlib1g-dev swig file wget libnl-3-dev \
  libnl-genl-3-dev libgps-dev libcap-dev pkg-config libopus-dev \
  libopusfile-dev portaudio19-dev net-tools libpcre3-dev libpcre3
```

### Usage

Run the `./scripts/openmanet_setup.sh` script to configure the build for your board of choice.

For example, Using seeedstudio's WiFi Halow Modules on Raspberry Pi4.
```
> ./scripts/openmanet_setup.sh -i -b ekh-bcm2711
```

Run this to download all dependencies before starting a build.  It will make building more reliable.
```
> make download
```

After configuration is complete, run the build with
```
> make -j$(nproc)
```

For verbose compilation, consider using
```
> make -j$(nproc) V=sc 2>&1 | tee log.txt
```

Once the build is complete a compiled image can be found in `bin/target/<platform>/<target>/`
