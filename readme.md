Thethingsnetwork V3 upgrade is in full swing. So if you migrated some devices and you use Node-Red, you noticed that the ttn-contrib doesn't work anymore and that the payload format is much different than V2.<br>This is an example for upgrading the Node-Red TTN devices (The Things Nework) from V2 to V3 while using the same InfluxDB (or any other) and eventually running TTN devices on v2 and V3 in paralell on Node-Red<br>
 <img src="images/thethingsnetwork_v3_console.png" alt="Upgrade TTN devices from V2 to V3"> 
 I am using here the RAK Wisnode with a a BME680 as described in https://github.com/baxtery/LoRawan_Wisblock_BME680 (inlcuding decoder)
<br><br>
 <img src="images/Node-Red_v2_v3_ttn.png" alt="Upgrade TTN nodes from V2 to V3 on Node-Red"> 
 <br>
 So the old V2 Node-Red-ttn Contrib is deprecated and doesn't work for V3, but actually u can still run it in paralell to write to the same DB while you move the devices in the TTN console.<br>
 Prerequisits:<p>
1-you have moved your device from V2 to V3 - basically recreate the device in V3 console https://console.cloud.thethings.network/<br>
2-you have copied/made a decrypt function in V3 in the console<br>
3-you have created the MQTT integration in the device console and created an API key (to use in Node-Red MQTT node)<br>
 for more information on this part you can use the TTN howto https://www.thethingsindustries.com/docs/integrations/node-red/
 </p>
 <p>
 You will need to<br>1-use the MQTT node in the Node_red contrib (no need to inslall anything)<br>Configure the node as MQTT client for TTN<br>Server : <mark>eu1.cloud.thethings.network</mark> Port <i><mark>1883</mark></i> and subscribe to your device uplink (topic)<br>
   <img src="images/create_mqtt_broker_api_keys.png" alt="Configure the API Keys for you Device" width="500"><br>
 Go to Security tab and add you API keys<br>
 Now go back to the main screen of the MQTT node<br>
  use <i><mark>v3/{application id}@{tenant id}/devices/{device id}/up</mark></i> as described in https://www.thethingsindustries.com/docs/integrations/mqtt/<br>
 #todo see how to generate keys and subscribe for app instead of device<br>
  <img src="images/create_mqtt_broker_ttn_v3_up.png" alt="Configure the TTN MQTT Broker" width="500"><br>
  2-then use a JSON formatter node available in the Node-red Contrib<br>
   <img src="images/Json_node.png" alt="Parse MQTT into JSON" width="500"><br>
 3- then update the function to prepare the data you want to inject in Influx DB. The path msg.payload has changed significantly.<br>
 <p>Most variables are now in <i><mark>msg.payload.uplink_message.decoded_payload.XXX</mark></i><br></p>
 <p>Device info are in <br>
 <i><mark>dev_id: msg.payload.end_device_ids.device_id,<br>
 app_id: msg.payload.end_device_ids.application_ids.application_id,</mark>
 </i><br></p>
<p>Network info<br>
<i><mark>rssi: msg.payload.uplink_message.rx_metadata[i].rssi,<br>
 snr: msg.payload.uplink_message.rx_metadata[i].snr,<br>
 frequency: msg.payload.uplink_message.settings.frequency,
 </mark></i><br></p>
 You can refer to TTN_V3_Node_red_function https://github.com/baxtery/TTN_V3_Node-Red/blob/main/TTN_V3_Node_red_function<br>
 please compare the code for V2 and V3 and make sure you have all your vairables as in V2</p>
 #todo: here we are connecting single devices, in v2 we connected APPs, check if this can be done<br>Note that I am connecting to a V2 Gateway, hence "Gateway ID" will appear as "Broker". 
