# WHC2021SIC-Guide

Guide for the IEEE World Haptics Conference 2021 Student Innovation Challenge

https://2021.worldhaptics.org/sic/

## Authors

- [Christian Frisson](https://frisson.re)
- [Jun Nishida](https://junis.sakura.ne.jp/wp)
- [Heather Culbertson](https://sites.usc.edu/culbertson/)
- you?

Your contributions are welcome, here are your options to help us improve this guide:
- [review and open issues](https://github.com/WHC2021SIC/WHC2021SIC-Guide/issues)
- [create pull requests](https://github.com/WHC2021SIC/WHC2021SIC-Guide/pulls)
- contact WHC 2021 SIC chairs at [sic@2021.worldhaptics.org](mailto:sic@2021.worldhaptics.org)

## Contents

Generated with `npm run toc`, see [INSTALL.md](INSTALL.md).

Once this guide becomes very comprehensive, the main file can be split in multiple files and reference these files.

<!-- table of contents generated by running from repository root: npm run toc -->

<!-- toc -->

- [Getting Started](#getting-started)
  * [Unpack and assemble hardware](#unpack-and-assemble-hardware)
    + [Raspberry Pi 4](#raspberry-pi-4)
    + [Audio Injector Octo soundcard hat](#audio-injector-octo-soundcard-hat)
    + [Syntacts board and actuators](#syntacts-board-and-actuators)
    + [SparkFun Qwiic hat, boards and sensors](#sparkfun-qwiic-hat-boards-and-sensors)
  * [Setup software configuration](#setup-software-configuration)
    + [Raspberry Pi 4](#raspberry-pi-4-1)
      - [Change or init your password](#change-or-init-your-password)
      - [Setup WiFi and SSH](#setup-wifi-and-ssh)
      - [Setup VNC](#setup-vnc)
      - [Forward mouse and keyboard input from your laptop/desktop to your Raspberry Pi](#forward-mouse-and-keyboard-input-from-your-laptopdesktop-to-your-raspberry-pi)
    + [Audio Injector Octo soundcard hat](#audio-injector-octo-soundcard-hat-1)
    + [Syntacts board and actuators](#syntacts-board-and-actuators-1)
      - [Test and create audio signal pipelines with Pure Data](#test-and-create-audio-signal-pipelines-with-pure-data)
      - [Explore the vibrotactile design space with the Syntacts Tactor Synthesizer](#explore-the-vibrotactile-design-space-with-the-syntacts-tactor-synthesizer)
      - [Other tools for haptic and audio interaction design](#other-tools-for-haptic-and-audio-interaction-design)
    + [SparkFun Qwiic hat, boards and sensors](#sparkfun-qwiic-hat-boards-and-sensors-1)
- [License](#license)

<!-- tocstop -->

## Getting Started

This section will help you setup hardware and software components of your WHC 2021 SIC kit.

### Unpack and assemble hardware

This section will help you setup hardware components of your WHC 2021 SIC kit.

#### Raspberry Pi 4

TODO

Make sure to hold the bare RPI board from its edges to avoid touching components.

#### Audio Injector Octo soundcard hat

TODO

Stack Audio Injector Octo soundcard hat on GPIO header of RPI.

Connect at least the Output RCA breakout.

#### Syntacts board and actuators

TODO

Define ideal wiring length based on your project setup, particularly depending on constraints from  the locations of actuators and of the rest of your system (both colocated? wearable?).

Solder actuators, wires and connectors. 

Connect:
- actuators to Syntacts board
- audio cables from Syntacts board to Audio Injector Octo soundcard hat

#### SparkFun Qwiic hat, boards and sensors

TODO

Remove the black header protection from the top of the Audio Injector Octo soundcard hat.

Stack your [SparkFun Qwiic HAT](https://www.sparkfun.com/products/14459) on top of the Audio Injector Octo soundcard hat.

### Setup software configuration

This section will help you setup software components of your WHC 2021 SIC kit.

#### Raspberry Pi 4

This section will let you setup your Raspberry Pi with a SD card reader and without the need of USB keyboard and mouse. 

We tested this procedure with the Raspberry Pi OS (formerly Raspbian) distribution and this kernel (output from command `uname -a` on a terminal):
`Linux raspberrypi 5.4.51-v7l+ #1333 SMP Mon Aug 10 16:51:40 BST 2020 armv7l GNU/Linux`

This procedure is based on third-party tutorials such as: https://desertbot.io/blog/headless-raspberry-pi-4-lite-remote-desktop-upgrade

##### Change or init your password

TODO Add method by writing filesystem with SD card reader.

If you are already logged in your Raspberry Pi, in a terminal, type/paste command `sudo passwd pi` then input your new password. Choose something else than the default ~~raspberry~~ password for increased security.

##### Setup WiFi and SSH

> The Secure Shell Protocol (SSH) is a cryptographic network protocol for operating network services securely over an unsecured network.[1] Typical applications include remote command-line, login, and remote command execution, but any network service can be secured with SSH. From: https://en.wikipedia.org/wiki/Secure_Shell_Protocol

Make sure your laptop/desktop and Raspberry Pi are on the same network.

Enable WiFi and SSH by following this tutorial: https://desertbot.io/blog/headless-raspberry-pi-4-ssh-wifi-setup

Highlight: to enable SSH, put a `ssh` file with no extension on boot partition:
https://www.raspberrypi.org/documentation/remote-access/ssh/

##### Setup VNC

> In computing, Virtual Network Computing (VNC) is a graphical desktop-sharing system that uses the Remote Frame Buffer protocol (RFB) to remotely control another computer. It transmits the keyboard and mouse events from one computer to another, relaying the graphical-screen updates back in the other direction, over a network. From: https://en.wikipedia.org/wiki/Virtual_Network_Computing

This procedure is based on third-party tutorials such as: https://www.raspberrypi.org/documentation/remote-access/vnc/

- install VNC Server on Raspberry Pi
    - `sudo apt install realvnc-vnc-server realvnc-vnc-viewer
    - `sudo raspi-config`
      - `Interfacing Options > VNC / SSH`
- determine the Raspberry Pi IP address:
   - access your Wifi router admin panel and identify connected devices
   - use network scanning tools, such as `nmap` for Linux debian/ubuntu systems: http://mitchtech.net/vnc-setup-on-raspberry-pi-from-ubuntu/
      - `sudo apt install nmap`
      - `nmap -sV -p 22 192.168.2.1-255` (replace `192.168.2.1-255` with your network subnetwork and range)
- download VNC Viewer from https://www.realvnc.com/en/connect/download/viewer/
- install:
   - for Linux debian/ubuntu systems: `sudo dpkg -i VNC-Viewer-6.20.529-Linux-x64.deb`

##### Forward mouse and keyboard input from your laptop/desktop to your Raspberry Pi

There are various ways of forwarding mouse and keyboard input from your laptop/desktop to your Raspberry Pi, see: https://raspberrypi.stackexchange.com/questions/4253/forward-mouse-and-keyboard-input-to-x-session

We recommend barrier: https://github.com/debauchee/barrier

#### Audio Injector Octo soundcard hat

Perform **Manual setup** from: https://github.com/WHC2021SIC/Octo

Automated setup is outdated and valid only for older kernels.

#### Syntacts board and actuators

##### Test and create audio signal pipelines with Pure Data

> Pure Data (Pd) is a visual programming language developed by Miller Puckette in the 1990s for creating interactive computer music and multimedia works. From: https://en.wikipedia.org/wiki/Pure_Data

Pure Data has been employed in the HCI and haptics communities, here are a few examples:
- StereoHaptics by Ali Israr et al.: https://la.disneyresearch.com/publication/stereohaptics/
- libhapiness by Christian Frisson et al.: https://gitlab.inria.fr/Loki/happiness/libhappiness
- WebAudioHaptics by Christian Frisson et al.: https://github.com/webaudiohaptics

Install puredata from a terminal with: `sudo apt install puredata`.

Test all vibrotactile channels independently by sending test signals (tone or noise) with puredata and its Test Audio and MIDI utility accessible from menu `Media`. 


##### Explore the vibrotactile design space with the Syntacts Tactor Synthesizer 

Explore the vibrotactile design space with the Syntacts Tactor Synthesizer by Evan Pezent et al.: https://github.com/WHC2021SIC/Syntacts

##### Other tools for haptic and audio interaction design

- Macaron by Oliver Schneider et al.: http://hapticdesign.github.io/macaron
- VibViz by Hasti Seifi et al.: http://www.cs.ubc.ca/~seifi/VibViz/main.html


#### SparkFun Qwiic hat, boards and sensors

TODO

## License

This documentation is released under the terms of the Creative Commons Attribution Share Alike 4.0 International license (see [LICENSE.txt](LICENSE.txt)).
