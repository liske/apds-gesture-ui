# APDS-9960 Gesture uInput


## About

*apds-gesture-uid* uses the gesture recognition of a [APDS-9960](https://www.sparkfun.com/products/12787) to simulate keyboard input by using the Linux uinput kernel module. This small script uses [python-apds9960](https://github.com/liske/python-apds9960) and [python-uinput](http://tjjr.fi/sw/python-uinput/) to allow to control your GUI with gestures.

The APDS-9960 is able to detect 4 directions which will trigger a virtual keypress. The [default config](ex/gesture-ui.conf) maps:

| Direction | Key           |
|:---------:|:-------------:|
| UP        | Page Up       |
| DOWN      | Page Down     |
| LEFT      | Left          |
| RIGHT     | Right         |


## Config

The python configuration file is `/etc/gesture-ui.conf`. The following settings are recognized:
- __I2C_PORT__ - the SMBus port number
- __GMAPPINGS__ - defines which gesture direction should trigger which key presses
- __POLLING_SLEEP__ - sleep between polling for new gesture recognition events
