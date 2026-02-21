### Klipper Machine Tweaks

#### # UART Interface
Use the built-in UART interface for direct MCU communication.

Documentation: <a href="../mods/Uart.md#direct-uart-connection-to-sbc-single-board-computer">See Uart.md</a>.

#### # USB (cmdline.txt)
Optimizations for the USB stack and CPU scheduling.

Path (add to the end): /boot/firmware/cmdline.txt
```
dwc_otg.lpm_enable=0 dwc_otg.fiq_fsm_enable=1 dwc_otg.nak_holdoff=1
```
<b>dwc_otg:</b> Disables USB power management and optimizes interrupt handling to ensure stable MCU connection.


#### # USOLCPUS (cmdline.txt)
Dedicate one CPU core exclusively to running Klipper.

Path (add to the end): /boot/firmware/cmdline.txt
```
isolcpus=3
```
<b>isolcpus=3:</b> Isolates the 4th CPU core from the Linux general scheduler for exclusive Klipper use.

##### Process Priority & CPU Affinity
Script: /bin/klipper_update_priority
```bash
#! /bin/bash
KLIPPER_PID=$(pgrep -f "klippy.py")

if [ -n "$KLIPPER_PID" ]; then
    chrt -f -p 40 $KLIPPER_PID       # Set Real-Time priority
    taskset -cp 3 $KLIPPER_PID       # Bind to isolated core 3
    ionice -c 1 -n 0 -p $KLIPPER_PID # Maximize I/O priority
fi
```
File: /etc/cron.d/klipper
```
@reboot root bash /bin/klipper_update_priority
*/5 * * * * root bash /bin/klipper_update_priority
```
File: /etc/default/irqbalance
```
IRQBALANCE_BANNED_CPUS=00000008
```


#### # System Performance (/etc/rc.local)

##### CPU Frequency

Script (add to the end): /etc/rc.local
```bash
cpupower frequency-set --min 1.2Ghz
cpupower frequency-set -g performance
```

##### Logging & Network
Script (add to the end): /etc/rc.local
```bash
mount -t tmpfs tmpfs /home/alarm/printer_data/logs/
iw dev wlan0 set power_save off
```

##### Extreme Real-Time Tuning
Note: Use with caution. Removes the 5% CPU safety margin for the OS.

Script (add to the end): /etc/rc.local
```bash
sysctl -w kernel.sched_rt_runtime_us=-1
```
