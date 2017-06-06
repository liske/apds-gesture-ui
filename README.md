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

The *python-apds9960* package requires *python-smbus* which should be installed using your package manager:
```console
# apt-get install python-smbus
```

It is recommended to create a dedicated [virtualenv](https://virtualenv.pypa.io/en/stable/userguide/) where
the python modules required by *apds-gesture-uid* will be installed:

```bash
# create empty virtualenv
$ virtualenv --system-site-packages /path/to/env
# enter the virtualenv
$ . /path/to/env/bin/activate

# install SMBus
$ pip install python-uinput

# install Paho MQTT python client (optional)
$ pip install paho-mqtt
```
