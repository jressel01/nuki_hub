## About

The NUKI Hub software acts as a bridge between a NUKI Lock and a smart home system. Via MQTT, the state can be queried and commands can be executed

## Setup

The firmware uses the Wifi Manager to configure the WiFi network. Power up the ESP32, a new Access Point should appear. Connect to this access point and in a browser navigate to "192.168.4.1". Use the web interface configure your Wifi network.

After configuring the Wifi, the ESP should automatically connect to your network. Use the web interface to setup the MQTT broker; just navigate to the IP-Address assigned to the ESP32 via DHCP (often found the web interface of the internet router).

## Paring

Just enable pairing mode on the NUKI lock and power on the ESP32. Pairing should be automatic. Unfortunately there's no feedback at the time, except for debug output on the serial line. If it worked, the lock state and the battery level should be reported via MQTT.

## MQTT Interface

- nuki/lock/state: Reports the current lock state as a string. Possible values are: uncalibrated, locked, unlocked, unlatched, unlockedLnga, unlatching, bootRun, motorBlocked
- nuki/lock/trigger: The trigger of the last action: autoLock, automatic, button, manual, system
- nuki/lock/completionStatus: Status of the last action: success, motorBlocked, canceled, tooRecent, busy, lowMotorVoltage, clutchFailure, motorPowerFailure, incompleteFailure, invalidCode, otherError, unknown
- nuki/lock/doorSensorState: State of the door sensor: unavailable, deactivated, doorClosed, doorOpened, doorStateUnknown, calibrating
- nuki/lock/action: (to be renamed to action). Allows to execute lock actions. After executing the action, the value is reset to an empty string. Possible actions: unlock, lock, unlatch, lockNgo, lockNgoUnlatch, fullLock, fobAction1, fobAction2, fobAction3
- 
- battery/voltage: Reports the current battery voltage in Volts.
- nuki/battery/level: Battery level in percent
- nuki/battery/critical: 1 if battery level is critical, otherwise 0
- nuki/battery/charging: 1 if charging, otherwise 0
- nuki/battery/voltage: Current Battery voltage (V)
- nuki/battery/drain: The drain of the last lock action in Milliwattseconds (mWs)
- nuki/battery/maxTurnCurrent: The highest current of the turn motor during the last lock action (A)

# Disclaimer

This is a third party software for NUKI smart door locks. This project or any of it's authors aren't associated with Nuki Home Solutions GmbH. Please refer for official products and offical support to their website:

https://nuki.io/

For further license details, check the included LICENSE file.