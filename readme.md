Thethingsnetwork V3 upgrade is in full swing. So if you migrated some devices and you use Node-Red, you noticed that the ttn-contrib doesn't work anymore and that the payload format is much different than V2.<br>This is an example for upgrading the Node-Red TTN devices (The Things Nework) from V2 to V3 while using the same InfluxDB (or any other) and eventually running TTN devices on v2 and V3 in paralell on Node-Red<br>
 I am using here the RAK Wisnode with a a BME680 as described in https://github.com/baxtery/LoRawan_Wisblock_BME680 (inlcuding decoder)
<br><br>
 <img src="images/Node-Red_v2_v3_ttn.png" alt="Upgrade TTN nodes from V2 to V3 on Node-Red"> 
 <br>
 You noticed here that the old V2 Node-Red Contrib is deprecated and doesn't work for V3, but actually u can still run them in paralell to write to the same DB while you move the devices in the TTN console.<br>
 Prerequisits:<p>
1-you have moved your device from V2 to V3 - basically recreate the device in V3<br>
2-you have copied/made a decrypt function in V3 in the console<br>
3-you have created the MQTT integration in the device console and created an API key (to use in Node-Red MQTT node)<br>
 for more information on this part you can use the TTN howto https://www.thethingsindustries.com/docs/integrations/node-red/
 </p>
 <p>
 You will need to<br>1-use and configure the MQTT node in the Node_red contrib (no need to inslall anything)<br>Configure Node-Red as MQTT client for TTN <br>Server : <i>eu1.cloud.thethings.network</i> Port <i>1883</i> and subscribe to your device uplink (topic)<br>
   <img src="images/create_mqtt_broker_api_keys.png" alt="Configure the API Keys for you Device" width="500"><br>
  use <i>v3/{application id}@{tenant id}/devices/{device id}/up</i> as described in https://www.thethingsindustries.com/docs/integrations/mqtt/<br>

  <img src="images/create_mqtt_broker_ttn_v3_up.png" alt="Configure the TTN MQTT Broker" width="500"><br>
  generate the keys in your device console. #todo see how to generate keys for app and not device<br>
  2-then use a JSON formatter node available in the Node-red Contrib<br>
   <img src="images/Json_node.png" alt="Parse MQTT into JSON" width="500"><br>
   Now go to security tab and add the API keys
 3- then update the function to prepare the data you want to inject in Influx DB (the path has changed)<br>
  as shown in TTN_V3_Node_red_function https://github.com/baxtery/TTN_V3_Node-Red/blob/main/TTN_V3_Node_red_function<br>
 please refer to the code for V2 and V3</p>
 #todo: here we are connecting single devices, in v2 we connected APPs<br>Note that I am connecting to a V2 Gateway, hence "Gateway ID" is shown as "Broker". 
