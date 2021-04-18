This is a example for upgrading the Node_red TTN (The Things Nework) from V2 to V3 while using the same InfluxDB (or any other) and eventually running TTN nodes on v2 and V3 in paralell on Node-Red
<br><br>
 <img src="images/Node-Red_v2_v3_ttn.png" alt="Upgrade TTN nodes from V2 to V3 on Node-Red"> 
 <br>
 You noticed here that the old V2 Node-Red COntrib is deprecated and doesn't work for V3./n
 You will need to/n 1-install the MQTT contrib/n 2-then use a JSON formatter node/n 3- then update the function to make capture the data you want (the path has changed)
