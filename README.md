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

# Edit wpa_supplicant.conf file with wifi password and ssid
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

# Add static ip addres to wifi wlan0
```
$ sudo vi /etc/dhcpcd.conf

interface wlan0
static ip_address=192.168.5.20/24
static routers=192.168.5.1
static domain_name_servers=1.1.1.1
```
