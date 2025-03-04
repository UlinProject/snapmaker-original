
## Disclaimer
The firmware presented here is provided as is, I am not responsible for your damaged devices. All information described here is solely my experience and can be both useful and harmful to the end user. You can reflash your printers only at your own risk. Damage to your device can occur at any stage of the end user's actions. All images and firmware presented here are the property of their authors.

Snapmaker is a registered trademark, to which I have no relation, you can always contact the official contacts listed on the website snapmaker.com. All rights reserved.

## Firmware

| name | value | mod_list | stable |
| ---- | ----- | ----- | ----- |
| 32Base-2_11Original.Bin | The latest current firmware from the manufacturer in 2019, downloaded from open sources. | | + |
| 32Base_2_11_01Demo250000BOUD.Bin | The first experiment on modifying this firmware, testing the reflashing method. | +uart 115200BOUD -> 250000BOUD; | +(only tests) |
| 32Base_2_11_02Demo500000BOUDAndAdvancedOK | Second experiment, 500000BOUD and ADVANCED_OK tests. | +uart 115200BOUD -> 500000BOUD; +uart advanced_ok; | +(only tests) |
| 32Base_2_11_04Demo500000BOUDAndMoreSerialMods | Experimenting with using the recommended settings for OctoPrint. | +uart 115200BOUD -> 500000BOUD; +uart advanced_ok; +fix: BLOCK_BUFFER_SIZE(8->64); +fix: BUFSIZE(8->32); +fix: RX_BUFFER_SIZE(512->2048); | +(only tests) |

## How to reflash?
1. Copy any file and rename it to Update.Bin to a USB disk formatted in Fat32.
2. Turn off the printer and insert the USB disk into the USB port.
3. Turn on the printer. If the LED changes as below, the update is successful.
- The blue LED blinks slowly for about 5 seconds.
- Then the LED turns off for about 2 seconds.
- The LED starts blinking quickly.
4. The flashing process is complete.
