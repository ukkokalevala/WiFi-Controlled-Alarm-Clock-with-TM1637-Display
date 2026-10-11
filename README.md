WiFi-Controlled Alarm Clock with TM1637 Display
A network-connected digital alarm clock built on the WeMos D1 Mini (ESP8266) and a TM1637 4-digit 7-segment display. Time is synchronized automatically from internet NTP servers, and alarms are set, snoozed, or cancelled from any browser on the same WiFi network — no buttons to fiddle with, no cloud service, no app to install.

What It Does
Always-accurate time via NTP sync every 60 seconds, with configurable timezone offset (no RTC module required)

Web interface served directly from the ESP8266 — open the device's IP in any browser to set the alarm time and snooze duration

Buzzer alarm with a blinking display when the alarm fires

Physical stop button for silencing the alarm without reaching for your phone

Snooze with adjustable delay (1–30 minutes), available from both the web page and the hardware button

Live status — the web page polls the device every 3 seconds and shows whether the alarm is off, idle, snoozed, or ringing

Hardware
Part	Purpose
WeMos D1 Mini (ESP8266)	Main controller + WiFi
TM1637 4-digit display	Shows time, blinks on alarm
Active buzzer	Audible alarm
Momentary push button	Stop / snooze on the device
Breadboard + jumpers	Wiring
Total cost: roughly the price of a coffee. No RTC, no cloud, no subscription.

Wiring Summary
TM1637 CLK → D2, DIO → D1

Buzzer + → D5

Button → D6 (internal pull-up, other leg to GND)

Technical Highlights
Non-blocking design — the buzzer uses tone() with a short duration per loop iteration rather than delay(), so the web server and button stay responsive even while the alarm is ringing

NTPClient + TimeLib for time handling with timezone offset applied at the source

ESP8266WebServer with routes for /, /set, /stop, /snooze, and a JSON /status endpoint

Debounced button with software filtering (300ms window) and edge detection

Single-file firmware — everything in one .ino, easy to flash and modify

Snooze implemented with millis() target so it survives independently of the NTP update cycle

Why I Built It
Most commercial alarm clocks either lock you into an app, require a cloud account, or are just ugly. This one is a small weekend project that turns ~$5 of parts into a genuinely useful desk companion — a clock that always knows the right time and that you can reprogram from your phone in ten seconds.

Hardware Setup
Component	WeMos D1 Mini Pin
TM1637 CLK	D2 (GPIO4)
TM1637 DIO	D1 (GPIO5)
TM1637 VCC	3.3V
TM1637 GND	GND
Buzzer (+)	D5 (GPIO14)
Buzzer (-)	GND
Button (one leg)	D6 (GPIO12)
Button (other leg)	GND
The button uses the internal pull-up, so no external resistor is needed.

Required Libraries
Install these from the Arduino IDE Library Manager:

TM1637 by Avishay Orpaz

NTPClient by Fabrice Weinberg

ESP8266WebServer (built into ESP8266 board package)

ESP8266WiFi (built in)
