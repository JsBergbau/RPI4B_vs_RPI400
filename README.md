# Raspberry PI 4B with passive Armor Case vs Raspberry Pi 400 
<img src="https://raw.githubusercontent.com/JsBergbau/RPI4B_vs_RPI400/main/images/Pi400AndPI4B.jpg" with="600" alt="Raspberry PI 400 vs Raspberry PI 4B" title="Raspberry PI 400 vs Raspberry PI 4B">
<img src="https://raw.githubusercontent.com/JsBergbau/RPI4B_vs_RPI400/main/images/Pi400AndPI4BConnections.jpg" with="600" alt="Raspberry PI 400 vs Raspberry PI 4B connectors" title="Raspberry PI 400 vs Raspberry PI 4B connectors">

## Cooling performance Raspberry PI 4B with Armor Case vs Raspberry PI 400
In this test I mainly compare the Raspberry PI 4B with 4 GB RAM and the Raspberry PI 400 with also 4 GB RAM. RPI 4B comes with 1,5 GHz whereas PI 400 is equipped with 1,8 GHz.
In this test I overclock both with 
```
arm_freq=2000
over_voltage=4
```
For maximum heat generation cpuburn-a53.S is used 
```
wget https://raw.githubusercontent.com/ssvb/cpuburn-arm/master/cpuburn-a53.S
gcc -o cpuburn-a53 cpuburn-a53.S
chmod +x cpuburn-a53
./cpuburn-a53
```
OS is Raspian Lite from 11. January 2021, filename 2021-01-11-raspios-buster-armhf-lite with updates of 3. February 2021 
```
uname -r
5.4.83-v7l+
````

## Power consumption Raspberry PI 4B and Raspberry PI 400
Clock frequency 2000 MHz, Overvoltage 4, only Gigabit Ethernet connected, no display connected, access solely with SSH, Load power consumption with cpuburn-a53s
Official Raspberry PI 4 USB-C PSU is used. For power consumption measurement the accurate "ELV Energy Master Profi-2" is used.
| | Idle | Load
|---|----|----|
Raspberry PI 4B @2GHz, 4 overvoltage | 2,6 W - 2,7 W | 8,6 W
Raspberry PI 4B @stock 1,5GHz, no overvoltage | 2,6 W | 5,8 W
Raspberry PI 400 @2GHz, 4 overvoltage| 2,5 W - 2,6 W | 7,2 W
Raspberry PI 400 @stock 1,8 GHz, no overvoltage| 2,4 W | 6,8 W

~0,1 W can be saved via ` /opt/vc/bin/tvservice -o`

Higher powerconsompution of Raspberry PI 400 @default speed is because of 20 % higher CPU speed. Please keep in mind that when connecting a USB keyboard to a Raspberry PI 4B power consumption will rise. So despite the higher CPU frequency Raspberry PI 400 is more energy efficient.

## Throttling

For this measurement ambient temperature is about 20 °C. Both, PI400 and RPI 4B have about 1 cm air under the case. For detecting throttling, throttleMonitor.sh in this repository is used.

### Raspberry PI4B
Both devices were cool. I’ve powered up and immediately began executing cpuburn.
Raspberry PI 4 with Armorcase throttled after about 19 minutes. Noticeably CPU temperature went up about 20 °C within less than a minute. This means there is a high thermal resistance between Armor Case and CPU heatspreader. Probably this is because of these light blue thermal pads between CPU and case.

<img src="https://raw.githubusercontent.com/JsBergbau/RPI4B_vs_RPI400/main/images/bluepads.jpg" with="600">

### Raspberry PI 400
Even after 30 minutes, Raspberry PI 400 didn’t throttle. Temperature was quite stable at about 60 °C. Because of the much bigger surface compared to the Raspberry PI 4B there is much more room for the heat to dissipate. Take a look at the thermal image. 

Top:

<img src="https://raw.githubusercontent.com/JsBergbau/RPI4B_vs_RPI400/main/images/thermografie.jpg" with="600" alt="Raspberry PI 400 thermal image" title="Raspberry PI 400 thermal image">

Bottom:

<img src="https://raw.githubusercontent.com/JsBergbau/RPI4B_vs_RPI400/main/images/thermografiebottom.jpg" with="600" alt="Raspberry PI 400 thermal image backside" title="Raspberry PI 400 thermal image backside">

If you want to take a look inside have a look at this video https://youtu.be/OqpylxLhw98?t=244 and the massive heatspreader inside the Raspberry PI 400. 

### Comparing Raspberry PI4B and Raspberry PI 400 regarding price
Raspberry PI 4B 4GB is about 57 €, and armor Case is about 10 €, so in total 67 €.
Raspberry PI 400 is about 71 €. You get a faster CPU and a keyboard. Only one USB port is less because the integrated keyboard is connected there. Regarding in addition the less power consumption and also no throttling of Raspberry PI 400 my favorite is clearly the Raspberry PI 400.
