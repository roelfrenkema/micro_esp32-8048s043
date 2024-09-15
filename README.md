# micro

Micro Python for ESP32 8048S043 S3 [full documenation](https://drive.google.com/file/d/1zXjLaWKtLhbnzKqttZI1uOZolPvU32vF/view?usp=sharing)

I will try and help you with micro python and the esp32s3 board 8048S043 also known as CYD short for Cheap Yellow Display.

As these boards are abborations you probably will not have much fun here if you have a 'regular' esp32s3.

It took me some time to get where I am now and that was not necessary. These pages should help you too make a faster jump. Lets start with micro python binaries of this nasty beast.

## ESP32-S3 Installation

Download the latest firmware (bin) here [https://micropython.org/download/ESP32_GENERIC_S3/](https://micropython.org/download/ESP32_GENERIC_S3/)

Put your board in download mode by pressing RESET and BOOT at the same time. Release RESET before BOOT.

Now you should be connected on /dev/ttyUSB0 (test with ls /dev/tty*)

Now first clear all rubish on there:

esptool.py --chip esp32s3 --port /dev/ttyUSB0 erase_flash

Then flash your firmware

esptool.py --chip esp32s3 --port /dev/ttyUSB0 write_flash -z 0 \<filename\>

Now esptool.py flash_id should give you info like:

```
esptool.py v4.8.dev5
Found 5 serial ports
Serial port /dev/ttyUSB0
Connecting....
Detecting chip type... ESP32-S3
Chip is ESP32-S3 (QFN56) (revision v0.2)
Features: WiFi, BLE, Embedded PSRAM 8MB (AP_3v3)
Crystal is 40MHz
MAC: 64:e8:33:44:31:84
Uploading stub...
Running stub...
Stub running...
Manufacturer: c8
Device: 4018
Detected flash size: 16MB
Flash type set in eFuse: quad (4 data lines)
Flash voltage set by eFuse to 3.3V
Hard resetting via RTS pin...
```

If not rinse and repeat. Be a better reader then I am.


## Pin Layout

### Screen 

Once I learned what pins are I got the values from: [https://github.com/bitbank2/bb_spi_lcd](https://github.com/bitbank2/bb_spi_lcd)

```
#define LCD_PIXEL_CLOCK_HZ     (16000000)
#define LCD_BK_LIGHT_ON_LEVEL  1
#define LCD_BK_LIGHT_OFF_LEVEL 0

#define PIN_NUM_BK_LIGHT       2
#define PIN_NUM_HSYNC          39
#define PIN_NUM_VSYNC          41
#define PIN_NUM_DE             40
#define PIN_NUM_PCLK           42
#define PIN_NUM_DATA0          8 // B0
#define PIN_NUM_DATA1          3 // B1
#define PIN_NUM_DATA2          46 // B2
#define PIN_NUM_DATA3          9 // B3
#define PIN_NUM_DATA4          1 // B4
#define PIN_NUM_DATA5          5 // G0
#define PIN_NUM_DATA6          6 // G1
#define PIN_NUM_DATA7          7 // G2
#define PIN_NUM_DATA8          15 // G3
#define PIN_NUM_DATA9          16 // G4
#define PIN_NUM_DATA10         4 // G5
#define PIN_NUM_DATA11         45  // R0
#define PIN_NUM_DATA12         48  // R1
#define PIN_NUM_DATA13         47 // R2
#define PIN_NUM_DATA14         21 // R3
#define PIN_NUM_DATA15         14 // R4
#define PIN_NUM_DISP_EN        -1
```

### Touch

Thanks to: [https://github.com/bitbank2/bb_captouch](https://github.com/bitbank2/bb_captouch)

```
#define PIN_SDA                19
#define PIN_SCL                20
#define PIN_IRQ                -1
#define PIN_RST                38   
```
