## 1.22I - 010525
## Modify
- All MQTT commands to have user name and time stamp similar to TCP commands
#3 020525
-- send TC command when coin inserted / hardware.c
-- created a new function SendTCResponse / mqtt.c
-- created new variable TCPRequired, Send response only if TCPRequired is set / vars. externvars, calls
-- create one more sub topic as GVC/KP/BROADCAST mqtt.c
-- if HBT-OK not received in X minutes and wifi is okay and MQTT is connected the reset the device
-- HBT-D is the command from device and HBT-S is the command from server
-- Pulse wisth is between 20 and 250 msec / hardware.c

#4 030525
-- stack for publish_mqtt task increased from 5k to 8k
#5 050525
-- do not reply when *HBT-S# is received / command.c
-- QOS option added on Subscribe
-- compare topic with broadcast as well serial number to allow action
-- ??? some times data not being senses by MQTT
-- ??? on 3rd May 2:52:00 pm one pulse missed while generating or receiving
-- blink leds when MQTT received moved 3 lines from analysePacketTcp.c to command.c

## 1.23- 090525
#1 090525
-- Add setting for MQTT_BROKER1, MQTT_BROKER2, MQTT_BROKER3. changed in /main/inc/defs
-- Change mqtt server as per *SIP:x# changed in /main/src/SaveRecallNVS.c
-- *MQTT:user:password# command added & saved in memory  changed in /main/src/commands.c
-- sent TC-D at sendTCresponse  changed in /main/src/mqttRoutine.c
-- *MQTT?# command added changed in /main/src/commands/c
--- & saved MQTT default user & pASSWORD values in memory. changed in/main/src/SaveRecallNvs.c
-- remove comparison of topic with expected topic  case MQTT_EVENT_DATA:/mqttRoutines.c
-- when INH input changes, send TCP/MQTT/UARt

## 1.23 - 100525
-- write code to get free heap and free internal heap
-- get that value on command *HEAP?# /main/src/analysePacketUart.c
-- send value to MQTT and TCP and UART 
-- removed retyrMqtt task . /main/main.c
-- enabled auto reconnect in mqtt configuration. //.network.disable_auto_reconnect = false,
-- *MIP:MipUsername:MipDateTime:MipNumber# command added in commands.c
-- & recalled from SaveRecallNVS.c
-- *MIP? command added in commands.c

## 1.23A - 290525
-- *TESTON# will start self test. Send pulse once per second and MQTT when all seven pulses match with input
-- change TESTCOIN and gpio_read_n_act
-- get RSSI info every 15 seocnds if wifi connected
-- *RSSI?# reply with *RSSI,value);


## 1.23 C - 130625
-- UartDebugInfo variannble added to disable Uart Logs.
-- Only QR:, STATUS? commands enabled on uart.


## 1.23D - 030925
FW- *Kwikpay_040925_VER_1.24C Naico Ltd#
-- add new command
-- ignore pulses on pins x,y,z,a,b,c
-- format - *CHENA:1:1:0:0:1:1:0#
-- *PULSES?# - reply *CHENA:1:1:0:0:1:1:0#
-- meaning - there are seven channels 
-- 0 in any channel is disabled 
-- 1 in any channel is enabled
-- save in memory as EnabledChannel[7]


-- TC-D remove

## 1.24X
-- all MQTT commands should go to UART
-- change in mqttRoutines.c

-- 100925
-- added TC_D when coin added
-- do not send TC-D regularly in loop

-- 120925 Changes done b siddhi
-- InitMqtt() called from main.c file
-- network.disabled_auto_reconnect set true line removed
-- called mqtt_app_start frm when wifi cnnected using FirstTryMqtt variable.
-- mqtt_app_stop() function created & called before mqtt_app_start().

## 1.25x
-- add new command *MAXTIME:mintime:maxtime#

## 1.25A
-- when jumper inserted change LED blinking
-- when jumper removed chnage led blinking to normal

## 1.25B (Planned)
-- when jumper (not ESPTOUCH but other pin) inserted set wifi/tcp/mqtt to GVC options (SIP:3) (MIP:3) (SSID: GVCSYS1/2/3 PW:GVC3065V)
-- when JUMPER is LOW at powe om shift to GVC credentials
-- remoevd JUMPER PORT code at NVS READ 
-- ERASE Bug solved. This was erasing even when there is an error