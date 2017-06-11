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

If the MQTT bridge modus is used, *apds-gesture-uid-pub* and *apds-gesture-uid-sub* are using the
following MQTT settings:
- __MQTT_HOST__ - the MQTT broker hostname or ip address
- __MQTT_OPTS__ - connection options (see also Paho MQTT python client)
- __MQTT_TOPIC__ - the MQTT topic used for publish and subscribe


## Install

### Prerequisites

Install *git*, *python-smbus* and *virtualenv*:

```console
# apt-get install git python-smbus virtualenv
```

### Download source

```console
# git clone --recursive https://github.com/liske/apds-gesture-ui.git /opt/apds-gesture-ui
```

### Kernel module

The *apds-gesture-ui* and the *apds-gesture-ui-sub* scripts require the kernel module *uinput.ko* to be loaded:

```console
# modprobe uinput
```

Put `uinput` into `/etc/modules` to load the module during system boot automaticly.


### Python modules

It is recommended to create a dedicated [virtualenv](https://virtualenv.pypa.io/en/stable/userguide/) where
the python modules required by *apds-gesture-uid* will be installed:
- create new virtualenv
```console
# virtualenv --system-site-packages /opt/apds-gesture-ui/venv
```
- enter the virtualenv
```console
# . /opt/apds-gesture-ui/venv/bin/activate
```
- install Python-uinput
```console
# pip install python-uinput
```
- install Paho MQTT python client (optional)
```console
# pip install paho-mqtt
```

### System service

This project contains example *systemd.service* files (see [ex/](ex/)). For activation copy the service file to
`/etc/systemd/system/` and change the containing paths to match you environment:

```console
# cp ex/apds-gesture-ui.service /etc/systemd/system/
# systemctl daemon-reload
# systemctl start apds-gesture-ui.service
# systemctl status apds-gesture-ui.service
```
