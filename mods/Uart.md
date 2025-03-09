#### UART
<img src="../img/uart.JPG" width="21%"></img>

Very weak (115200boud) feedback and high latency do not produce good prints. Eliminating the latency that occurs on USB allows the octoprint to work better and print better, but the 115200 is not defeated yet.

The photo shows the contacts that need to be soldered to use the UART of the single board computer and the microcontroller directly without converting to USB and back.
After soldering the contacts I recommend removing the ch340g chip, but I want to note that you will lose USB support.

<b>These actions are relevant only for the factory firmware</b>, when using firmware at a higher speed (different from 115200) this problem is more or less eliminated by the firmware "32Base_2_11_01Demo250000BOUD.Bin". The problem is completely eliminated on the firmware "32Base_2_11_04Demo500000BOUDAndMoreSerialMods.bin" with an active "buffer buddy" (plugin on octoprint) and can be used with a usb dongle, but 500000 baud may not suit everyone and you can use a simpler one without special corrections "32Base_2_11_01Demo250000BOUD.Bin" at 250000 baud.
