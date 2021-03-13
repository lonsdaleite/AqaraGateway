# Aqara Gateway/Hub (G2H, M1S CN, P3 CN, M2) integration for Home Assistant

Control Zigbee devices from Home Assistant with **Aqara Gateway (KTBL12LM, ZHWG15LM, ZHWG12LM, ZNSXJ12LM)**.

This integration was based on the development of <a href=https://github.com/AlexxIT/XiaomiGateway3/>@AlexxIT</a>, Thanks Alex.

**ATTENTION:** The component **only works on modified firmware (M2) or the gateway which enabled telnet . **

To flash modified firmware to M2, please use <a href="https://github.com/niceboygithub/AqaraM1SM2fw/raw/main/tools/aqaragateway.exe"> AqaraGateway.exe </a> to flash. Need to open the case of gateway and wired out the UART.

For M1S CN and AirCondition P3, you can use <a href="https://gist.github.com/zvldz/1bd6b21539f84339c218f9427e022709"> custom open telnet command </a> way 2 or way 3 to enable telnet in *Mi Home mode*, then flash modification firmwares to <a href="https://github.com/niceboygithub/AqaraM1SM2fw/tree/main/modified/M1S"> M1S </a>, <a href="https://github.com/niceboygithub/AqaraM1SM2fw/tree/main/modified/P3/3.0.7_0007.0515"> P3 </a> or copy pubic mosquitto to /data/bin. No need to open the case of gateway.

After telnet to gateway via putty, there are two ways to enable telnet and public mqtt.

## Not Flash Custom firmware method

```shell
mkdir /data/bin
cd /data/bin
wget -O /data/bin/curl "http://master.dl.sourceforge.net/project/mgl03/bin/curl?viasf=1"
chmod +x /data/bin/curl
/data/bin/curl -s -k -L -o /data/bin/mosquitto https://raw.githubusercontent.com/niceboygithub/AqaraM1SM2fw/main/binutils/mosquitto
chmod a+x /data/bin/mosquitto

mkdir /data/scripts
cd /data/scripts
/data/bin/curl -s -k -L -o /data/scripts/post_init.sh https://raw.githubusercontent.com/niceboygithub/AqaraM1SM2fw/main/binutils/post_init.sh
chmod +x /data/scritps/post_init.sh
```

## Flash M1S Custom firmware method
```shell
cd /tmp
wget -O /tmp/curl "http://master.dl.sourceforge.net/project/mgl03/bin/curl?viasf=1"
chmod a+x /tmp/curl
/tmp/curl -s -k -L -o /tmp/linux_3.1.2_0013.0519.bin https://raw.githubusercontent.com/niceboygithub/AqaraM1SM2fw/main/original/M1S/3.1.2_0013.0519/linux_3.1.2_0013.0519.bin
fw_update /tmp/linux_3.1.2_0013.0519.bin
/tmp/curl -s -k -L -o /tmp/rootfs_3.1.2_0013.0519_modified.bin https://raw.githubusercontent.com/niceboygithub/AqaraM1SM2fw/main/modified/M1S/3.1.2_0013.0519/rootfs_3.1.2_0013.0519_modified.bin
fw_update /tmp/rootfs_3.1.2_0013.0519_modified.bin
```

## Flash P3 Custom firmware method
```shell
cd /tmp
wget -O /tmp/curl "http://master.dl.sourceforge.net/project/mgl03/bin/curl?viasf=1"
chmod a+x /tmp/curl
/tmp/curl -s -k -L -o /tmp/linux_3.0.7_0007.0515.bin https://raw.githubusercontent.com/niceboygithub/AqaraM1SM2fw/main/original/P3/3.0.7_0007.0515/linux_3.0.7_0007.0515.bin
fw_update /tmp/linux_3.0.7_0007.0515.bin
/tmp/curl -s -k -L -o /tmp/rootfs_3.0.7_0007.0515_modified.bin https://raw.githubusercontent.com/niceboygithub/AqaraM1SM2fw/main/modified/P3/3.0.7_0007.0515/rootfs_3.0.7_0007.0515_modified.bin
fw_update /tmp/rootfs_3.0.7_0007.0515_modified.bin
```

For G2H, you need to wired out the UART, then login to gateway to <a href="https://github.com/niceboygithub/AqaraCameraHubfw/tree/main/binutils#aqara-camera-hub-g2g2h-znsxj12lm-related-binutils">enable telnetd</a>.

Gateway support **Zigbee 3**.

**Attention:** The component is under active development.

<a href="https://www.buymeacoffee.com/niceboygithub" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-orange.png" alt="Buy Me A Coffee" height="41" width="174"></a>
