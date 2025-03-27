### UART

#### Disclaimer
I am not responsible for your damaged 3D printers and single board computers, I do not give advice, this information is provided as is, you can use it only at your own risk.

#### About the factory firmware
Very weak (115200 baud) feedback and high latency do not give good prints. Eliminating the latency that occurs on USB allows octoprint to work better and print better. This printer prints better from a USB stick.

The printing problem on the factory firmware is more or less solved by the firmware "32Base_2_11_01Demo250000BOUD.Bin". Starting with "32Base_2_11_04Demo500000BOUDAndMoreSerialMods.bin" the problem is completely fixed on firmware with active "buffer buddy" (plugin on octoprint) and can be used with USB key, but 500000 baud rate may not suit everyone, and you can use simpler without special edits "32Base_2_11_01Demo250000BOUD.Bin" at 250000 baud.

#### Direct UART connection to SBC (single board computer)
<img src="../img/uart.JPG" width="21%"></img>

It is possible to connect the microcontroller and SBC directly, eliminating the influence of USB connection. The photo shows the contacts that need to be soldered to the wires to use UART of SBC and microcontroller directly, without converting to USB and back. After soldering the contacts I recommend removing the ch340g chip (but you will lose USB support)

#### Things to remember when using Raspberry Pi single board computers with direct UART connection
1. Enable uart with "enable_uart=1" in config.txt
2. Disable system services
```
sudo systemctl stop serial-getty@ttyS0.service
sudo systemctl disable serial-getty@ttyS0.service

sudo systemctl stop serial-getty@ttyAMA0.service
sudo systemctl disable serial-getty@ttyAMA0.service
```
3. Do not use mini UART (/dev/ttyS0), it is better to disable it, it will only hinder you (you will lose the ability to use bluetooth). When using this interface, connection latency is not constant, performance is variable
add to config.txt
```
dtoverlay=pi3-disable-bt
dtoverlay=disable-bt
```
Now you can specify /dev/ttyAMA0 in octoprint or klipper config.

4. <b>(Optional, may not work for everyone)</b> You can increase the UART clock speed and get a theoretical maximum of ~4 Mbps over UART
Add to config.txt:
```
init_uart_clock=64000000
```
