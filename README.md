SNESDev-RPi-Wiring-Pi
=====================

SNESDev is a user-space driver for the RetroPie GPIO Adapter for the Raspberry Pi. It implements two (S)NES game controllers and a virtual keyboard for up to two (S)NES controllers and a button that are connected to the GPIO pins of the Raspberry Pi via the RetroPie GPIO Adapter (http://blog.petrockblock.com/2012/10/21/the-retropie-gpio-adapter/) or the MonsterJoysticks Arcade Controller GPIO Interface (https://monsterjoysticks.com/arcade-controller-gpio-interface-for-raspberry-pi).

This Version of the driver has been adapted from the original (https://github.com/petrockblog/SNESDev-RPi) version and modified to use the Wiring Pi (https://github.com/petrockblog/SNESDev-RPi) GPIO library.

Installation
------------

Manual installation:

First of all, make sure that Git is installed:

```shell
sudo apt-get update
sudo apt-get install -y git
```

Install the following dependencies:

```shell
sudo apt-get install -y libconfuse-dev
cd
git clone https://github.com/WiringPi/WiringPi.git
cd WiringPi
sudo ./build
```

SNESDev is downloaded and installed with

```shell
cd
git clone https://github.com/MonsterJoysticks/SNESDev-RPi-Wiring-Pi
cd SNESDev-RPi-Wiring-Pi
sudo make
sudo make install
```

The lines above build and install two needed libraries and SNESDev-Rpi. The sudo-command is needed for the installation of the two libraries. It is recommend to run SNESDev as a service, which is described [below](https://github.com/MonsterJoysticks/SNESDev-RPi-Wiring-Pi#running-snesdev-as-a-service).

Alternatively, you can use the RetroPie Setup Script (https://github.com/petrockblog/RetroPie-Setup) for installing and configuring SNESDev.

Running
-------

In order to run SNESDev mae sure that the uinput module is loaded. You can check this with

```shell
lsmod
```

The module is loaded with

```shell
sudo modprobe uinput
```

If you want to have the uinput module automatically loaded, you can add "uinput" to the file 
/etc/modules.

SNESDev has to be run as background process with

```shell
sudo ~/SNESDev-RPi/bin/SNESDev &
```

In order to access the uinput device SNESDev has to be run as root. This is (obviously) not so nice and is currently an issue. If you have a solution or suggestion for that, feel free to submit a pull request or send me a mail!

Configuring SNESDev-Rpi
-----------------------

SNESDev-Rpi is configured with the help of the configuration file ```/etc/snesdev.cfg```. It is a lightweighted configuration file and well commented. You can also use the RetroPie Setup Script (https://github.com/petrockblog/RetroPie-Setup) for configuring SNESDev.

__IMPORTANT:__ You might need to configure the correct version of the RetroPie GPIO Adapter. The default version is 2.X. If you find a revision number 1.X on your RetroPie GPIO Adapter you need to set the configiration parameter "adapter_version" to "1x".


Running SNESDev as a service
----------------------------

SNESDev-RPi comes with a script that allows SNESDev to be run as a service. The installation command for that is

```shell
sudo make installservice
```

Uninstalling SNESDev service
----------------------------

You can uninstall the SNESSDev-Rpi service with the following command:

```shell
sudo make uninstallservice
```


Button Polling
--------------

If you use the functionality for polling a button (on GPIOin P1-11), a three-state automaton is implemented:
 
- press and hold: send "r" key (for rewind function of RetroArch)
- press and release three times: send "ESC"
- press and release five times: shutdown

For comments, corrections, and suggestions visit https://github.com/petrockblog/SNESDev-RPi.

Have fun!


Raspberry Pi is a trademark of the Raspberry Pi Foundation.
