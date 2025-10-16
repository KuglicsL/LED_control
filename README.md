# PWM & ARGB LED controller
ESP32 based controller for high-current PWM dimming and long-distance addressable LED driving
# Features
- 4x 12V fault-protected differential output digital channels for addressable LED strips
- 4x 30A 0-26V open-drain PWM channels for RGB(W) or single colour LED strips
- 4x isolated optocoupler inputs (0-50V) in two groups
- Onboard programmer using CP2102N USB-UART bridge
- Fused connections on all output power ports - ATO/ATC fuse holders
- Two pinheaders for analog inputs
- Small outline - 100x100mm
- Optional TVS diodes when assembled using cheaper transceivers
- Compatible with [the WLED project](https://kno.wled.ge/)
  
![PCB render](/Documentation/pers_top.png)

## PWM channels
The 4 independent PWM channels are open-drain outputs tested at 30A load. With adequate cooling, it can handle more. The FETs have TVS diodes, snubbers and flyback diodes protecting them.
## Digital channels
The 4 digital channels use THVD2450 transceivers for reliable long-distance addressable LED control. You can solder the in-line [receiver module](https://github.com/KuglicsL/Differential_receiver) to the LED strip at the first pixel.

## Limitations
The 12V input is routed to the digital channels, and the 24V input is for the PWM LED strips (voltage range 0-26V).
The control works from both the 12V and 24V inputs, however it needs the 12V input for the PWM gate drivers. **Without +12V connected, the PWM will not work.**

The differential outputs need a [receiver module](https://github.com/KuglicsL/Differential_receiver) on the LED side.

When using multiple channels at maximum current, the board probably needs cooling. I haven't got the time to test for exact numbers.

The USB-UART bridge IC needs to be configured to toggle the RX/TX leds - this is done with Silicon Labs' own tool. The whole USB-UART section could be replaced with a CH340 alternative for lower cost, but I wanted to use parts readily available from EU/NA distributors.
