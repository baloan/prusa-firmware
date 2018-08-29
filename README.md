# Custom Prusa i3 MK2/S PINDA V2 Firmware

## About this Firmware

This custom firmware is forked from the Original Prusa i3 Firmware. The firmware supports temperature calibration with a PINDA V2 with a hybrid extruder on a Prusa i3 Mk2/S frame . See thingiverse at [https://www.thingiverse.com/thing:3062641](https://www.thingiverse.com/thing:3062641 "Prusa i3 Mk2S upgrade with hybrid Mk2.5 R3 extruder") for details.

### example calibration
This is the first successful calibration I achieved with the  v3.1.0-pindav2-r1 firmware. The calibration matrix can be queried with a terminal with the G Code `M861 ?`.

<table style="border-collapse: collapse; width: 136pt;" border="0"
cellpadding="0" cellspacing="0" width="180">
<col style="width: 34pt;" span="4" width="45"> <tbody>
<tr style="height: 15pt;" height="20">
<td class="xl63"
style="height: 15pt; width: 34pt; text-align: right;" height="20"
width="45">index</td>
<td class="xl63" style="width: 34pt; text-align: right;"
width="45"><span style="">&nbsp;</span>temp</td>
<td class="xl63" style="width: 34pt; text-align: right;"
width="45"><span style="">&nbsp;</span>ustep</td>
<td class="xl63" style="width: 34pt; text-align: right;"
width="45"><span style="">&nbsp;</span>um</td>
</tr>
<tr style="height: 15pt;" height="20">
<td class="xl63" style="height: 15pt; text-align: right;"
height="20">n/a</td>
<td style="text-align: right;" class="xl63">35</td>
<td style="text-align: right;" class="xl63">0</td>
<td style="text-align: right;" class="xl63">0</td>
</tr>
<tr style="height: 15pt;" height="20">
<td style="height: 15pt;" align="right" height="20">0</td>
<td align="right">40</td>
<td align="right">36</td>
<td align="right">90</td>
</tr>
<tr style="height: 15pt;" height="20">
<td style="height: 15pt;" align="right" height="20">1</td>
<td align="right">45</td>
<td align="right">58</td>
<td align="right">145</td>
</tr>
<tr style="height: 15pt;" height="20">
<td style="height: 15pt;" align="right" height="20">2</td>
<td align="right">50</td>
<td align="right">82</td>
<td align="right">205</td>
</tr>
<tr style="height: 15pt;" height="20">
<td style="height: 15pt;" align="right" height="20">3</td>
<td align="right">55</td>
<td align="right">109</td>
<td align="right">272</td>
</tr>
<tr style="height: 15pt;" height="20">
<td style="height: 15pt;" align="right" height="20">4</td>
<td align="right">60</td>
<td align="right">119</td>
<td align="right">297</td>
</tr>
</tbody>
</table>

## Build instructions

### Step 1 - Download and Install/Unpack Arduino

Download and install the Arduino IDE. The most recent version 1.8.6 is available here:
<a href="https://www.arduino.cc/en/Main/Software" target="_blank">https://www.arduino.cc/en/Main/Software</a>

If you already use a different Arduino IDE version for other projects and don't want to upgrade to the latest release, you may want to install a stand-alone (ZIP file) version rather than using the "Windows Installer".

### Step 2 - Prepare the Arduino toolchain

1. Open the IDE
2. Choose _File -> Preferences_ and set "Additional Boards Manager URLs" to the RAMBo repository:<br/> <a href="https:// raw.githubusercontent.com/ultimachine/ArduinoAddons/master/package_ultimachine_index.json" target="_blank">https:// raw.githubusercontent.com/ultimachine/ArduinoAddons/master/package_ultimachine_index.json</a>
3. Select _Tools -> Boards -> Boards Manager_ and install the RAMBo board:<br/>"<small>**RepRap Arduino-compatible Mother Board (RAMBo)** by **UltiMachine**</small>"
4. Close the IDE.
5. Open the IDE and select **RAMBo** as target board from the _Tools -> Boards_ submenu.
6. Close the IDE

### Step 3 - Download PRUSA i3 MK2 Firmware

You can either clone the baloan/Prusa-Firmware repository to a local directory or download the ZIP file from <a href="https://github.com/baloan/Prusa-Firmware/tree/MK2-PindaV2-r1" target="_blank">https://github.com/baloan/Prusa-Firmware/tree/MK2-PindaV2-r1</a> and unpack it in a local directory.

Specific released versions of source code in either **.zip** or **.tar.gz** packages can be found here:
<a href="https://github.com/prusa3d/Prusa-Firmware/releases" target="_blank">https://github.com/baloan/Prusa-Firmware/releases</a>

### Step 4 - Configure the Printer Firmware - select variant

The following configurations are available in the __Prusa-Firmware/Firmware/variants__ directory.
(See **How-to-choose-firmware.pdf** for help choosing configuration.)

* 1_75mm_MK1-RAMBo10a-E3Dv6full.h
* 1_75mm_MK1-RAMBo13a-E3Dv6full.h
* 1_75mm_MK2-MultiMaterial-RAMBo10a-E3Dv6full.h
* 1_75mm_MK2-MultiMaterial-RAMBo13a-E3Dv6full.h
* 1_75mm_MK2-RAMBo10a-E3Dv6full.h
* 1_75mm_MK2-RAMBo13a-E3Dv6full.h
* 1_75mm_MK2-RAMBo13a-E3Dv6full-PINDAV2.h

Copy and rename the file representing your configuration to the ``Firmware`` directory as ``Configuration_prusa.h`` Example:
> $ cp Firmware/variants/1_75mm_MK1-RAMBo13a-E3Dv6full-PINDAV2.h Firmware/Configuration_prusa.h

### Step 5 - Build the Firmware

1. Open the IDE
2. Load the firmware project with _File -> Open..._ Navigate to and open:<br/>
 ``Prusa-Firmware/Firmware/Firmware.ino``
3. Compile the firmware with _Sketch -> Verify/Compile (CTRL-R)_ --or--
4. Export the compiled binary with _Sketch -> Export compiled Binary (CTRL-ALT-S)_.<br/>
You will find the exported binary in ``Prusa-Firmware/Firmware/Firmware.ino.rambo.hex``


### Step 6 - Upload the Firmware

You can upload the new firmare to the printer by using either:

* The Prusa3D Firmware Updater (download from <a href="https://www.prusa3d.com/drivers/" target="_blank">https://www.prusa3d.com/drivers/</a>)

* Directly via the Arduino IDE...<br/>
    Select _Tools -> Port_ and select the serial USB connection to the printer.<br/>
    Select _Sketch -> Upload_ to build and flash the firmware.

* Obtain the free utility: **avrdude** for your platform. Firmware may be uploaded either directly via command-line or using OctoPrint. Example command-line:
>$ avrdude -v -p m2560 -c wiring -P /dev/ttyUSB0 -b 115200 -U "flash:w:**Firmware.ino.rambo.hex**:i" -D

Happy printing!

