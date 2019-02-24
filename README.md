# PlatformIO LoRaWAN example 

A copy of [mbed-os-example-lorawan](https://github.com/ARMmbed/mbed-os-example-lorawan) that is compilable with
PlatformIO. 

# Settings 

See `mbed_app.json`. You must change the pin settings and LoRa keys (OTA/ABP parameteres) for this to work.

# TTN notice

mbed-os listens by default on SF12 for the RX2 window. Since TTN sends RX2 traffic on SF9, your node will hear
nothing. If you want to receive data when using TTN and ABP, see https://github.com/ARMmbed/mbed-os/issues/9761

# Credits

Radio driver code is curtesy of the people at https://github.com/ARMmbed/mbed-semtech-lora-rf-drivers
