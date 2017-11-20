### Webradio application supporting ePaper(GDEH0154D27)

For update binary on ePaper plus ESP32-ADB board, just execute

```
make menuconfig
```

and edit SSID and password in "Web Radio / Bluetooth Speaker" section.(no need to touch another parts) After that
```
make makefs
make copyfs
make flashfs
make flash
```
will update everything on the board.



As same as another ESP32-ADB series, preset station can be edit through web interface running on ESP32. Preset URL of the streaming radio station can be editby the following commands:

```
GET /  - list stations
GET /P - change to previous station
GET /N - change to next station
GET /0..9 - select station
GET /0..9+URL - set station URL
GET /0..-URL - remove station URL
```
for example, if your board has IP address of 192.168.1.10, then accessing following address by web browser
```
http://192.168.1.10/1+http://beatles.purestream.net/beatles.mp3
```
will add new preset "1" with the address of "http://beatles.purestream.net/beatles.mp3"


'GPIO-0' on board activate station switching to next preset station.

----

Please use latest esp-idf environment (envorinment just before will make lots error)

original code (w/o OLED, ePaper) is
https://github.com/MrBuddyCasino/ESP32_MP3_Decoder

OLED display mode for WiFi Radio/Bluetooth spaker will be set by menuconfig (select BT speaker or Wifi radio)

Bluetooth device name is defined in bt_config.h in include file folder. (default: "hogehoge_mont")

----
Wiring is same as original, as
ESP pin   - I2S signal
```
----------------------
GPIO25/DAC1   - LRCK
GPIO26/DAC2   - BCLK
GPIO22        - DATA
```
and GPIO25/26 are fixed but GPIO22 can be re-arranged as you wish.
(defined in components/audio_renderer.c)

ePaper is connected, as
ESP pin   - ePaper signal
```
----------------------
GPIO21   - BUSY
GPIO16   - RESET
GPIO17   - D/C
GPIO4    - CS
GPIO14   - SCLK
GPIO15   - MOSI
```
,which defined in components/epaper/EPDspi.h Please change as you wish...


More details can be found in the original author's explanation at
https://github.com/MrBuddyCasino/ESP32_MP3_Decoder
