# EVCC Configuration for MQTT
Configurations to publish PV data from Home Assistant to EVCC via MQTT. 

## Sungrow Inverter
It has been developed based on the following "integration" (https://github.com/mkaiser/Sungrow-SHx-Inverter-Modbus-Home-Assistant) to use the Modbus TCP connection for the Sungrow inverter without a Modbus Proxy.

**automations.yaml:** Home Assistant automation to publish the required data to the MQTT broker

**evcc.yaml:** Things you have to add/chnage to the main configuration file for the EVCC addon

