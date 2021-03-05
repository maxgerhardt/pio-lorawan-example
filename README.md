# PlatformIO LoRaWAN example 

A copy of [mbed-os-example-lorawan](https://github.com/ARMmbed/mbed-os-example-lorawan/tree/mbed-os-6.6.0) that is compilable with
PlatformIO in the currently used mbed-os version (6.6.0).  

# Settings 

See `mbed_app.json`. You must change the pin settings and LoRa keys (OTA/ABP parameteres) for this to work.

This example copies the SX127x configuration file from the `mbed_app.json` file of the repo.
Other configs are available at https://github.com/ARMmbed/mbed-os-example-lorawan/tree/master/config but currently incorrect (see https://github.com/ARMmbed/mbed-os-example-lorawan/issues/216), so beware.

Example: This projects `platformio.ini` uses `board = nucleo_l152re` which maps to the mbed-os target `NUCLEO_L152RE`. The `mbed_app.json` contains a section defining the settings for that mbed-os board using 

```json
	"NUCLEO_L152RE": {
		"lora-spi-mosi":       "D11",
		"lora-spi-miso":       "D12",
		"lora-spi-sclk":       "D13",
		"lora-cs":             "D10",
		"lora-reset":          "A0",
		"lora-dio0":           "D2",
		"lora-dio1":           "D3",
		"lora-dio2":           "D4",
		"lora-dio3":           "D5",
		"lora-dio4":           "D8",
		"lora-dio5":           "D9",
		"lora-rf-switch-ctl1": "NC",
		"lora-rf-switch-ctl2": "NC",
		"lora-txctl":          "NC",
		"lora-rxctl":          "NC",
		"lora-ant-switch":     "A4",
		"lora-pwr-amp-ctl":    "NC",
		"lora-tcxo":           "NC"
	},
```

which defines the radio pins. (not-connected pins can are to NC). 

The settings from the `*` override section also apply. Settings regarding keys (for OTA in this case) and the radio type are contained.

```json
    "target_overrides": {
        "*": {
            "platform.stdio-convert-newlines": true,
            "platform.stdio-baud-rate": 115200,
            "platform.default-serial-baud-rate": 115200,
            "lora.over-the-air-activation": true,
            "lora.duty-cycle-on": true,
            "target.components_add": ["SX1272", "SX1276", "SX126X"],
            "lora.phy": "EU868",
            "lora.device-eui": "{ 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00 }",
            "lora.application-eui": "{ 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00 }",
            "lora.application-key": "{ 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00 }",
            "target.components_add": ["SX1276"]
        },
```

If your target board is not in explicitly mentioned in the `mbed_app.json` settings, the pin settings from the `config` object in there apply (all `NC` default). 

For other `lora.*` settings, see https://github.com/ARMmbed/mbed-os/blob/master/connectivity/lorawan/mbed_lib.json (e.g. regarding ABP configuration). 

# TTN notice

mbed-os listens by default on SF12 for the RX2 window. Since TTN sends RX2 traffic on SF9, your node will hear
nothing. If you want to receive data when using TTN and ABP, see https://github.com/ARMmbed/mbed-os/issues/9761. This issue can be ignored when using OTA.

# Credits

Radio driver code is curtesy of the people at https://github.com/ARMmbed/mbed-semtech-lora-rf-drivers
