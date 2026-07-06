# EVCC Configuration for MQTT
Configurations to publish PV data from Home Assistant to EVCC via MQTT.

## Sungrow Inverter
It has been developed based on the following "integration" (https://github.com/mkaiser/Sungrow-SHx-Inverter-Modbus-Home-Assistant) to use the Modbus TCP connection for the Sungrow inverter without a Modbus Proxy.

### Monitoring (read-only)
**automations.yaml:** Home Assistant automation to publish the required data to the MQTT broker

**evcc.yaml:** Things you have to add/change to the main configuration file for the EVCC addon

### Battery Control (write)
**battery_control_automations.yaml:** Home Assistant automation that subscribes to EVCC's battery mode commands via MQTT and controls the Sungrow inverter (EMS mode, forced charge/discharge, power) using the mkaiser integration's select/number entities.

The battery meter in evcc.yaml includes a `batterymode` write plugin that publishes EVCC's desired battery mode (1=normal, 2=hold, 3=charge) to `pvdataevcc/battery/mode/set`. HA picks up the message and maps it:
- **normal** → Self-consumption mode (battery operates freely based on PV surplus and household demand)
- **hold** → Forced mode + Stop/0W (prevents discharge during fast EV charging)
- **charge** → Forced mode + Forced charge at max power (grid charging when prices are cheap)

On HA startup, the automation defaults to self-consumption mode as a safe fallback.

