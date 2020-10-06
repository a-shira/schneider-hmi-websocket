# schneider-hmi-websocket

## Overview:

This is a WebSocket protocol for Schneider HMI the product is BLUE and EcoStruxure Operator Terminal.

## Change log:

The first version.

## Current Features: 

- Support basic feature
  - Variables
  - Alarms
  - System errors

## Limitation:

- Do not support security: user name and password.

## Sample:

Here's a short example connect to the HMI which IP address is 192.168.1.100.

```javascript
const HmiSchneiderWebSocket = require('./schneider-hmi-websocket.js');

var ws = new HmiSchneiderWebSocket();
var host = "192.168.1.100";
var port = 8082;

ws.onopen = function () {
  var vars = ["Var1", "Var2"];
  ws.send_add_monitor(vars);
};

ws.onclose = function (){
};

ws.onmessage = function(){
  alet updated = jsonObj.updated;
  if (updated == "variable") {
    //  variable
    jsonObj.data.foreach(item){
      let name = item.name;
      let quality = item.quality;
      let value = item.value;
    }
  } else if (updated == "alarm") {
    //  alarm
    jsonObj.data.foreach(item){
      let variable = item.variable;
      let status = item.status;
      let message = item.message;
    }
  } else if (updated == "error") {
    //  error 
  }

  ws.open("ws://" + host + ":" + port + "/api/v1/ws", undefined);

  ws.close();
};
```
