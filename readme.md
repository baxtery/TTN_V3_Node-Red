This is a example for upgrading the Node_red TTN (The Things Nework) from V2 to V3 while using the same InfluxDB (or any other) and eventually running TTN nodes on v2 and V3 in paralell on Node-Red
<br><br>
 <img src="images/Node-Red_v2_v3_ttn.png" alt="Upgrade TTN nodes from V2 to V3 on Node-Red"> 
 <br>
 You noticed here that the old V2 Node-Red COntrib is deprecated and doesn't work for V3.
 Prerequisits:<p>
1-you have moved your device from V2 to V3 - basically recreadted the device in V3<br>
2-you have copied/made a decrypt function in V3<br>
3-you have created the MQTT integration in the device console and create an API key <br>
 for more information on this part you can use the TTN howto https://www.thethingsindustries.com/docs/integrations/node-red/
 </p>
 <p>
 You will need to<br>1-use and configure the MQTT in the Node_red contrib<br>
  <img src="images/create_mqtt_broker_ttn_v3_up.png" alt="Configure the TTN MQTT Broker"><br>
  <img src="images/create_mqtt_broker_api_keys.png" alt="Configure the API Keys for you Device"><br>
  2-then use a JSON formatter node available in the Node-red Contrib<br>
   <img src="images/Json_node.png" alt="Parse MQTT into JSON"><br>
 3- then update the function to prepare the data you want to inject in Influx DB (the path has changed)<br>
  as shown in TTN_V3_Node_red_function<br>
 please refer to the code for V2 and V3</p>
