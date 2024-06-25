# JSON settings

!!! note

    This page only applies to the T-Stick 4GW/5GW and their variants.

Several parameters for the T-Stick are defined in the `config.json ` and `settings.json` files in the data folder of the T-Stick firmware.

## config.json Settings

The `config.json` file holds configuration information for the T-Stick including the name of the device, ID number, wifi connection details and the OSC configuration details.

The default `config.json` file is shown below.

```
{
    "device": "TStick",
    "id": 1,
    "author": "T-Stick Builder",
    "institution": "SAT/IDMIL (2024)",
    "APpasswd": "mappings",
    "wifiSSID": "tstick_network",
    "wifiPSK": "mappings",
    "persistentAP": 1,
    "oscIP1": "192.168.137.1",
    "oscPORT1": 8000,
    "oscIP2": "0.0.0.0",
    "oscPORT2": 8001,
    "localPORT": 8000
}
```

### Properties

- __device__: Name of the device. Should not be changed. *(Default: TStick)*
- __id__: ID number of the T-Stick. *(Default: 1)*
- __author__: Owner/Builder of the T-Stick. *(Default: T-Stick Builder)*
- __institution__: Institution that owns/builds the T-Stick. *(Default: SAT/IDMIL (2024))*
- __APpasswd__: Password to the T-Sticks Access Point. *(Default: mappings)*
- __wifiSSID__: Name of WiFi network the T-Stick is connecting to. *(Default: tstick_network)*
- __wifiPSK__: Password of WiFi network the T-Stick is connecting to. *(Default: mappings)*
- __persistentAP__: Set to 1 for the access point of the T-Stick to always be available. Should not be changed from default. *(Default: 1)*
- __oscIP1/2__: IP address to send OSC messages to. Can be set to `0.0.0.0` to disable OSC. *(Default: oscIP1: 192.168.137.1/oscIP2: 0.0.0.0)*
- __oscPORT1/2__: Port OSC messages are sent to. *(Default: oscPORT1: 8000/ oscPORT2: 8001)*
- __localPORT__: Port of the OSC server of the T-Stick. *(Default: 8000)*

## settings.json

The `settings.json` file holds the additional information that is displayed in the t-stick web portal. 

The default `settings.json` file is shown below.

```
{
    "settings": [
        {
            "name": "enable_libmapper",
            "value": 0
        },
        {
            "name": "fsr_offset",
            "value": 2000
        },
        {
            "name": "touch_noise",
            "value": 50
        },
        {
            "name": "jab_threshold",
            "value": 5
        },
        {
            "name": "battery_size_mah",
            "value": 2000
        }
    ]
}
```

### Properties

- __fsr_offset__: Set the minimum value of the FSR when no pressure is being applied. *(Default: 2000)*
- __touch_noise__: Set the minimum value before a touch input is registered. Only applies to T-Sticks that use the Trill board or the EnchantiTouch board. *(Default: 50)*
- __jab_threshold__: Set the sensitivity of the jab gesture. Larger values lower the sensitivity of the jab signal. *(Default 5)*
- __battery_size-mah__: Set the battery size in mAh. Only applies to T-Stick 5GW using the MAX17055/MAX17262 fuel gauge. *(Default 2000)*