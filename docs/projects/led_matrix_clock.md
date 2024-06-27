# Led matrix clock

For our PWS (Profielwerkstuk, final high school project), a friend and I created a clock using 4xHUB75 led matrices. These led-matrices were driven by a RPI-2B running raspbian with the RPI-RGB-LED-Matrix library and hardware hat by [Hzeller](https://github.com/hzeller/rpi-rgb-led-matrix). 

![](assets/DSC00001.JPG)

The library itself did not have enough functionality though; It did offer all the primitives we needed but we also wanted to have;

- Video with sound playback
- Weather forecast
- Timer functionality

So we added this functionality and made our own custom remote control, to control the timer and video playback.

## Video playback

Video playback was already present in the rpi-rgb-led matrix library. Sound was lacking however, so we manually added it using libsdl2 with the MP3 playback functionality. Before videoplayback we would extract the audio tracks using ffmpeg and then play it back using the libsdl2 alongside the videoplayback code of the rpi-rgb-led-matrix library.

![](assets/matrix.gif)


## Weather forecast

Weather forecast used the openweathermap api which is freely available, even as free user you will be able to see forecasts of about 1 hour ahead.
The api data was fetched using libcurl and parsed with a json parser library.

## Timer functionality

The timer functionality uses a simple chrono implementation. Which calculates the new timestamp based on the given user remote control, and then counts till the timestamp.

## Remote control

The code was custom Arduino code which connected with TCP sockets to the matrix over WiFi and updated a local version of it's database with the database on the server (SQLite database, used special version which ran on ESP32).

The pcb was designed in Altium Circuitmaker and used a SSH1106 OLED screen,  SDCard slot, ESP32-WROOM32 module and Li-ion 1S charging circuit. To our surpise the PCB was right first time and did not need any botch wires :).


![](assets/remote_control_assembly_top.jpg)

![](assets/remote_control_pcb_down.jpg)