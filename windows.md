# How to find the password for a Wi-Fi network
In cmd run:

> netsh wlan show profile

find the right `NETWORK NAME` and then:

> netsh wlan show profile “NETWORK NAME” key=clear
