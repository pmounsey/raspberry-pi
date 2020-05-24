# raspberry-pi

## Scan for wifi access points
```
$ sudo iwlist wlan0 scan | grep ESSID

                    ESSID:"Dust_Bunny2Ghz"
                    ESSID:"Dust_Bunny5Ghz"
                    ESSID:"BugsBunny2Ghz"
                    ESSID:"New1969-2"
                    ESSID:"DIRECT-55-HP ENVY 5660 series"
                    ESSID:"xfinitywifi"
                    ESSID:"fuzz"
                    ESSID:"Kingston"
                    ESSID:"Mustang"
```

## Add wifi enpoint to wpa_supplicant.conf 
```
$ sudo vi /etc/wpa_supplicant/wpa_supplicant.conf

ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=US

network={
        ssid="Dust_Bunny2Ghz"
        psk="********"
        key_mgmt=WPA-PSK
        priority=1
	id_str="DustBunny2Ghz"

}

network={
        ssid="Dust_Bunny5Ghz"
        psk="********"
        key_mgmt=WPA-PSK
        priority=2
	id_str="DustBunny5Ghz"
}
```

## Configure static ip address to wifi wlan0
```
$ sudo vi /etc/dhcpcd.conf

interface wlan0
static ip_address=192.168.5.20/24
static routers=192.168.5.1
static domain_name_servers=8.8.8.8
```

## [Raspberry Pi Camera](https://www.raspberrypi.org/documentation/raspbian/applications/camera.md)

### Take a still picture
  - resolution 640x480
```
raspistill -t 2000 -o image.jpg -w 640 -h 480

```
  - Reduce qaulity to reduce file size -q
```
raspistill -t 2000 -o image.jpg -q 5
```
  - Force Privew at coordinate 100,100 and resolution 300x200
```
raspistill -t 2000 -o image.jpg -p 100,100,300,200
```
  - Disable preview -n
```
raspistill -t 2000 -o image.jpg -n
```
  - Save image with Lossless compression -e
```
raspistill -t 2000 -o image.png -e png
```
  - Add Tag Data
```
raspistill -t 2000 -o image.jpg -x IFD0.Artist=Boris -x GPS.GPSAltitude=1235/10
```
  - Add emboss image effect
```
raspistill -t 2000 -o image.jpg -ifx emboss
```
  - Set U and V of YUV for grayscale image
```
raspistill -t 2000 -o image.jpg -p 100,100,320,200 -cfx 128:128
```
  - Preview no saved image
```
raspistill -t 10000
```
  - Take time-lapse picture every 5 seconds for 1 minute
```
raspistill -t 60000 -tl 5000 -o image_num_%03d_today.jpg -l latest.jpg
```

### Take a Video Capture
  - 5second clip at 1080p30
```
raspivid -t 5000 -o video.h264
```
  - 5seconds clip at 3.5Mbits/s
```
raspivid -t 5000 -o video.h264 -b 3500000
```
  - 5seconds at framerate of 5fps
```
raspivid -t 5000 -o video.h264 -f 5
```

