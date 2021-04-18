This is a example for upgrading the Node_red TTN (The Things Nework) from V2 to V3 while using the same InfluxDB (or any other) and eventually running TTN nodes on v2 and V3 in paralell on Node-Red
<br><br>
 <img src="images/Node-Red_v2_v3_ttn.png" alt="Upgrade TTN nodes from V2 to V3 on Node-Red"> 
 <br>
 You noticed here that the old V2 Node-Red COntrib is deprecated and doesn't work for V3.<p>
 You will need to<br>1-install the MQTT contrib<br>2-then use a JSON formatter node<br>3- then update the function to make capture the data you want (the path has changed)</p>
Prerequisits:<p>
1-you have moved your device from V2 to V3 - basically recreadted the device in V3<br>
2-you have copied/made a decrypt function in V3<br>
3-you have created the MQTT integration in the device console and create an API key <br>
 for more information on this part you can use the TTN howto https://www.thethingsindustries.com/docs/integrations/node-red/
 </p>
 
