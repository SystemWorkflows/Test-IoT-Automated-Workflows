# Attempt 6

Model Used: Google Gemini-1.5-flash-001
Notes/Explanation: Working workflow
Values set to msg.payload were off, but were consistently formatted so could be fixed
Parameters Used: Temperature = 0
Top-P = 0

System prompt:

```
You are an expert IoT system developer, proficient with Web of Things (WoT) descriptions and Node-RED workflow programming. 

Ensure that all node IDs are unique.
Ensure that quote marks used within strings are handled.
Take care not to provide multiple inputs to a node where not required.
Change msg.payload before nodes that require the change.

The following text, marked by the surrounding markers "----" is an example of a system definition.

----
The list WoT Thing descriptions of Things/devices available to use when producing the Node-RED workflow:

[
{
 "@context": [
  "http://www.w3.org/ns/td"
 ],
 "@type": [
  "Thing"
 ],
 "title": "AlertSystem",
 "securityDefinitions": {
  "no_sec": {
   "scheme": "nosec"
  }
 },
 "security": "no_sec",
 "actions": {
  "alertRole":{
   "type": "",
   "title": "Alert Role",
   "description": "Alerts the given system role with a provided message",
   "input": {
    "type": "object",
    "properties":{
     "role":{
      "type": "string",
      "description": "The role to be alerted"
     },
     "message":{
      "type": "string",
      "description": "The message to be sent to the role"
     }
    }
   },
   "forms": []
  },
  "dispatchRescueTeam":{
   "type": "",
   "title": "Dispatch Rescue Team",
   "description": "Sends the rescue team to the provided location",
   "input":{
    "type": "string",
    "description": "The location to send the rescue team too"
   },
   "forms": []
  }
 },
 "properties": {},
 "events": {}
},
{
 "@context": [
  "http://www.w3.org/ns/td"
 ],
 "@type": [
  "Thing"
 ],
 "title": "AvalancheDetector",
 "securityDefinitions": {
  "no_sec": {
   "scheme": "nosec"
  }
 },
 "security": "no_sec",
 "actions": {},
 "properties": {},
 "events": {
  "avalancheDetected":{
   "title": "Avalanche Detected",
   "description": "An event made when an avalanche is detected",
   "subscription": {},
   "data": {
    "type": "string",
    "description": "the location of the avalanche"
   },
   "cancellation": {},
   "forms": []
  }
 }
},
{
 "@context": [
  "http://www.w3.org/ns/td"
 ],
 "@type": [
  "Thing"
 ],
 "title": "CustomerContacts",
 "securityDefinitions": {
  "no_sec": {
   "scheme": "nosec"
  }
 },
 "security": "no_sec",
 "actions": {
  "notifyCustomer":{
   "type": "",
   "title": "Notify Customer",
   "description": "Notifies the customer with the provided ID of the given message",
   "input": {
    "type": "object",
    "properties":{
     "customerID":{
      "type": "string",
      "description": "The ID of the customer to be notified"
     },
     "message":{
      "type": "string",
      "description": "The message to be sent to the customer"
     }
    }
   },
   "forms": []
  }
 },
 "properties": {},
 "events": {}
},
{
 "@context": [
  "http://www.w3.org/ns/td"
 ],
 "@type": [
  "Thing"
 ],
 "title": "DigitalSignage",
 "securityDefinitions": {
  "no_sec": {
   "scheme": "nosec"
  }
 },
 "security": "no_sec",
 "actions": {
  "displayText":{
   "type": "",
   "title": "Display Signage",
   "description": "Displays the given text on signage around the ski slopes",
   "input": {
    "type": "string",
    "description": "The text to be displayed on the signs"
   },
   "forms": []
  }
 },
 "properties": {},
 "events": {}
},
{
 "@context": [
  "http://www.w3.org/ns/td"
 ],
 "@type": [
  "Thing"
 ],
 "title": "RentalDevice",
 "securityDefinitions": {
  "no_sec": {
   "scheme": "nosec"
  }
 },
 "security": "no_sec",
 "actions": {},
 "properties": {},
 "events": {
  "emergencyButtonPressed":{
   "title": "Emergency Button Pressed",
   "description": "An alert made when a user has pressed the emergency button on this device",
   "subscription": {},
   "data": {
    "type": "object",
    "properties":{
     "location":{
      "type": "string",
      "description": "The current location of this rental device"
     },
     "rentalID":{
      "type": "string",
      "description": "The ID of the rental this device is currently assigned too"
     }
    }
   },
   "cancellation": {},
   "forms": []
  }
 }
},
{
 "@context": [
  "http://www.w3.org/ns/td"
 ],
 "@type": [
  "Thing"
 ],
 "title": "RentalSystem",
 "securityDefinitions": {
  "no_sec": {
   "scheme": "nosec"
  }
 },
 "security": "no_sec",
 "actions": {
  "awaitRentalReturn":{
   "type": "",
   "title": "Await Rental Return",
   "description": "Starts a timer for the specified rental to be completed by. The timer is completed when it expires or the rental is returned",
   "input": {
    "type": "object",
    "properties":{
     "rentalID":{
      "type":"string",
      "description": "The ID of the rental completion to be awaited"
     },
     "timeout":{
      "type": "number",
      "description": "The number of minutes to wait before deaming the rental to be not returned"
     }
    }
   },
   "output": {
    "type": "boolean",
    "description": "Whether or not the rental was returned. True - The rental was returned, False - The timer expired and the rental was deamed to not have returned"
   },
   "forms": []
  }
 },
 "properties": {},
 "events": {
  "rentalGiven":{
   "title": "Rental Given",
   "description": "An alert made when a rental is given",
   "subscription": {},
   "data": {
    "type":"object",
    "properties":{
     "rentalID":{
      "type": "string",
      "description": "The ID of the rental"
     },
     "customerID":{
      "type": "number",
      "description": "The ID of the customer that purchased the rental"
     }
    }
   },
   "cancellation": {},
   "forms": []
  }
 }
},
{
 "@context": [
  "http://www.w3.org/ns/td"
 ],
 "@type": [
  "Thing"
 ],
 "title": "ResortActuators",
 "securityDefinitions": {
  "no_sec": {
   "scheme": "nosec"
  }
 },
 "security": "no_sec",
 "actions": {},
 "properties": {
  "resortHeating":{
   "type": "number",
   "title": "Resort Heating",
   "description": "The current temperature of the heaters in the ski resort",
   "forms": []
  },
  "resortLighting":{
   "type": "number",
   "title": "Resort Heating",
   "description": "The current brightness of the lighting in the ski resort",
   "forms": []
  }
 },
 "events": {
  "resortEnergyUsage":{
   "title": "Resort Energy Usage Change",
   "description": "An event made when there is a fluctuation in energy usage within the resort",
   "subscription": {},
   "data": {
    "type":"number",
    "description":"The current energy usage"
   },
   "cancellation": {},
   "forms": []
  }
 }
},
{
 "@context": [
  "http://www.w3.org/ns/td"
 ],
 "@type": [
  "Thing"
 ],
 "title": "SlopeSafetySystem",
 "securityDefinitions": {
  "no_sec": {
   "scheme": "nosec"
  }
 },
 "security": "no_sec",
 "actions": {
  "updateAvalancheRiskCalculation":{
   "type": "",
   "title": "Update Avalanche Risk Calculation",
   "description": "Updates the estimated risk of an avalanche based on newly added data",
   "input": {
    "type": "object",
    "properties":{
     "dataType":{
      "type": "string",
      "description": "The type/source of the data being added"
     },
     "value":{
      "type": "string",
      "description": "The value of the data being added"
     }
    }
   },
   "output": {
    "type": "string",
    "description": "The estimated risk level (none, minor or major)"
   },
   "forms": []
  },
  "blockSlopeEntry":{
   "type": "",
   "title": "Block Slope Entry",
   "description": "Blocks entry to the ski slope at the given location",
   "input": {
    "type": "string",
    "description": "The location of the ski slope"
   },
   "forms": []
  },
  "haltLift":{
   "type": "",
   "title": "Halt Lift",
   "description": "Stops the ski lift at the given position from working",
   "input": {
    "type": "string",
    "description": "The location of the ski lift"
   },
   "forms": []
  },
  "getSlopeBusyness":{
   "type": "",
   "title": "Get Slope Busyness",
   "description": "Gets the busyness of the various ski slopes",
   "output": {
    "type": "string",
    "description": "Details about the busyness of each ski slope"
   },
   "forms": []
  }
 },
 "properties": {
  "liftWaitTime":{
   "type": "number",
   "title": "Lift Wait Time",
   "description": "Provides an estimate of the current wait time for using a ski lift",
   "readOnly": true,
   "forms": []
  }
 },
 "events": {
  "slopeBusynessChange":{
   "title": "Slope Busyness Change",
   "description": "A broadcast of the new busyness level of a ski slope, made when the level changes",
   "subscription": {},
   "data": {
    "type": "object",
    "properties":{
     "location":{
      "type": "string",
      "description": "The location of the ski slope"
     },
     "busyness":{
      "type": "string",
      "description": "The busyness of the provided slope (not busy, moderately busy or crowded)"
     }
    }
   },
   "cancellation": {},
   "forms": []
  },
  "liftMalfunction":{
   "title": "Lift Malfunction",
   "description": "An event made when a lift malfunctions",
   "subscription": {},
   "data": {
    "type": "string",
    "description": "The location of the lift"
   },
   "cancellation": {},
   "forms": []
  }
 }
},
{
 "@context": [
  "http://www.w3.org/ns/td"
 ],
 "@type": [
  "Thing"
 ],
 "title": "UserDevice",
 "securityDefinitions": {
  "no_sec": {
   "scheme": "nosec"
  }
 },
 "security": "no_sec",
 "actions": {
  "receiveWeatherConditions":{
   "type": "",
   "title": "Receive Weather Conditions",
   "description": "Relays the given weather conditions to the user of this device",
   "input": {
    "type": "string",
    "description": "The details of the current weather conditions on the ski slopes"
   },
   "forms": []
  },
  "receiveSlopeDetails":{
   "type": "",
   "title": "Receive Slope Details",
   "description": "Passes the details of slope busyness and lift wait times to the user of this device",
   "input": {
    "type": "object",
    "properties":{
     "busyness":{
      "type": "string",
      "description": "The busyness of the ski slopes"
     },
     "waitTime":{
      "type": "string",
      "description": "The estimated lift wait time"
     }
    }
   },
   "forms": []
  }
 },
 "properties": {},
 "events": {
  "requestWeatherConditions":{
   "title": "Request Weather Conditions",
   "description": "A user request for the current weather conditions of the ski slopes",
   "subscription": {},
   "data": {},
   "cancellation": {},
   "forms": []
  },
  "requestSlopeDetails":{
   "title": "Request Slope Details",
   "description": "A user request for dentails about the ski slopes, concerning their busyness and lift wait times",
   "subscription": {},
   "data": {},
   "cancellation": {},
   "forms": []
  }
 }
},
{
 "@context": [
  "http://www.w3.org/ns/td"
 ],
 "@type": [
  "Thing"
 ],
 "title": "WeatherMonitor",
 "securityDefinitions": {
  "no_sec": {
   "scheme": "nosec"
  }
 },
 "security": "no_sec",
 "actions": {
  "getWeatherDetails":{
   "type": "",
   "title": "Get Weather Details",
   "description": "Gets all weater details for the ski slopes",
   "output": {
    "type":"string",
    "description": "A textual description of the slope weather conditions"
   },
   "forms": []
  }
 },
 "properties": {},
 "events": {
  "temperature":{
   "title": "Temperature",
   "description": "The current temperature on the slopes",
   "subscription": {},
   "data": {
    "type": "number",
    "description": "The current temperature"
   },
   "cancellation": {},
   "forms": []
  },
  "windSpeed":{
   "title": "Wind Speed",
   "description": "The current speed of the wind over the slopes",
   "subscription": {},
   "data": {
    "type": "number",
    "description": "The current wind speed"
   },
   "cancellation": {},
   "forms": []
  },
  "snowfall":{
   "title": "Snowfall",
   "description": "The current amount of snowfall on the slopes",
   "subscription": {},
   "data": {
    "type": "number",
    "description": "The current amount of snowfall"
   },
   "cancellation": {},
   "forms": []
  }
 }
}
]

The IoT system proposal/description, to be implemented as a Node-RED workflow:

If temperature, wind speed, or snowfall indicate a potential risk for skiers. If there is a minor risk of avalanches display warnings on digital signage across the resort. If there is a major risk, alert the resort management and close all slopes.

If an avalanche is detected, the system immediately alerts the resort management and close off affected slopes as well as dispatching the rescue team, and stopping lifts near the affected area.

If a slope becomes too crowded, the system alerts the resort management, who can then take measures to redirect skiers to less crowded slopes.

Allow rentals to be made for 3 days. If rented equipment is not returned within the given time, send a notification to the customer that made the rental order to prompt them to return the equipment. After that, give the customer 1 hour to return the equipment. If the equipment is still not returned alert the rental shop.

If a skier presses the emergency button on their resort-provided wearable device, the system alerts the resort's medical team and provides them with the skier's location.

If a lift malfunctions, the system alerts the maintenance team and initiates repair procedures.

Allow guests to query real-time information about weather conditions, slope traffic, and lift wait times.

If the resort’s energy usage exceeds a certain threshold, the system alerts the facilities manager and lowers the resort’s heating or lighting systems to conserve energy.

The Node-RED workflow produced when implementing the system, based on the system proposal and using the Things/devices provided:

[
 {
  "id": "c348ea29f9cebfd1",
  "type": "tab",
  "label": "Flow 10",
  "disabled": false,
  "info": "",
  "env": []
 },
 {
  "id": "a129d19cd8939580",
  "type": "system-event-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingEvent": "temperature",
  "thingEventValue": "{\"uri\":\"http://localhost:8080/weathermonitor\",\"output\":{\"type\":\"number\",\"description\":\"The current temperature\"},\"description\":\"The current temperature on the slopes\",\"title\":\"Temperature\",\"event\":\"temperature\"}",
  "outputToMsg": true,
  "redeploy": "true",
  "x": 110,
  "y": 60,
  "wires": [
   [
    "36432ba29f1a7ebb"
   ]
  ]
 },
 {
  "id": "4ac5fcb15d4e246f",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "displayText",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/digitalsignage\",\"params\":{},\"description\":\"Displays the given text on signage around the ski slopes\",\"title\":\"Display Signage\",\"action\":\"displayText\"}",
  "outputToMsg": true,
  "redeploy": "true",
  "x": 630,
  "y": 200,
  "wires": [
   []
  ]
 },
 {
  "id": "3b620808f3ea7e01",
  "type": "system-event-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingEvent": "windSpeed",
  "thingEventValue": "{\"uri\":\"http://localhost:8080/weathermonitor\",\"output\":{\"type\":\"number\",\"description\":\"The current wind speed\"},\"description\":\"The current speed of the wind over the slopes\",\"title\":\"Wind Speed\",\"event\":\"windSpeed\"}",
  "outputToMsg": true,
  "redeploy": "false",
  "x": 100,
  "y": 100,
  "wires": [
   [
    "e18e421a7f9aa823"
   ]
  ]
 },
 {
  "id": "92ad923b1e39cdea",
  "type": "system-event-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingEvent": "snowfall",
  "thingEventValue": "{\"uri\":\"http://localhost:8080/weathermonitor\",\"output\":{\"type\":\"number\",\"description\":\"The current amount of snowfall\"},\"description\":\"The current amount of snowfall on the slopes\",\"title\":\"Snowfall\",\"event\":\"snowfall\"}",
  "outputToMsg": true,
  "redeploy": "false",
  "x": 100,
  "y": 140,
  "wires": [
   [
    "5d7ddd2273902710"
   ]
  ]
 },
 {
  "id": "b04346057594b86d",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "updateAvalancheRiskCalculation",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/slopesafetysystem\",\"params\":{\"dataType\":\"string\",\"value\":\"string\"},\"output\":{\"type\":\"string\",\"description\":\"The estimated risk level (none, minor or major)\"},\"description\":\"Updates the estimated risk of an avalanche based on newly added data\",\"title\":\"Update Avalanche Risk Calculation\",\"action\":\"updateAvalancheRiskCalculation\"}",
  "outputToMsg": true,
  "redeploy": "false",
  "x": 540,
  "y": 100,
  "wires": [
   [
    "43016e5e043c412f"
   ]
  ]
 },
 {
  "id": "36432ba29f1a7ebb",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "payload",
    "pt": "msg",
    "to": "{\"dataType\":\"temprature\",\"value\":msg.payload}",
    "tot": "jsonata"
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 280,
  "y": 60,
  "wires": [
   [
    "b04346057594b86d"
   ]
  ]
 },
 {
  "id": "e18e421a7f9aa823",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "payload",
    "pt": "msg",
    "to": "{\"dataType\":\"windSpeed\",\"value\":msg.payload}",
    "tot": "jsonata"
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 280,
  "y": 100,
  "wires": [
   [
    "b04346057594b86d"
   ]
  ]
 },
 {
  "id": "5d7ddd2273902710",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "payload",
    "pt": "msg",
    "to": "{\"dataType\":\"snowfall\",\"value\":msg.payload}",
    "tot": "jsonata"
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 280,
  "y": 140,
  "wires": [
   [
    "b04346057594b86d"
   ]
  ]
 },
 {
  "id": "43016e5e043c412f",
  "type": "switch",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "property": "payload",
  "propertyType": "msg",
  "rules": [
   {
    "t": "eq",
    "v": "minor",
    "vt": "str"
   },
   {
    "t": "eq",
    "v": "major",
    "vt": "str"
   }
  ],
  "checkall": "true",
  "repair": false,
  "outputs": 2,
  "x": 250,
  "y": 240,
  "wires": [
   [
    "1f0964d30901557e"
   ],
   [
    "14aecb896fb3394b",
    "a5c5a1521513c390"
   ]
  ]
 },
 {
  "id": "1f0964d30901557e",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "payload",
    "pt": "msg",
    "to": "Avalanches risk, ski with care",
    "tot": "str"
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 460,
  "y": 200,
  "wires": [
   [
    "4ac5fcb15d4e246f"
   ]
  ]
 },
 {
  "id": "14aecb896fb3394b",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "payload",
    "pt": "msg",
    "to": "{\"role\":\"management\", \"message\":\"Major risk of avalanche, barring entry to all slopes\"}",
    "tot": "jsonata"
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 460,
  "y": 260,
  "wires": [
   [
    "35d771a07e109291"
   ]
  ]
 },
 {
  "id": "35d771a07e109291",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "alertRole",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/alertsystem\",\"params\":{\"role\":\"string\",\"message\":\"string\"},\"description\":\"Alerts the given system role with a provided message\",\"title\":\"Alert Role\",\"action\":\"alertRole\"}",
  "outputToMsg": true,
  "redeploy": "false",
  "x": 620,
  "y": 260,
  "wires": [
   []
  ]
 },
 {
  "id": "71cb6eeb1e1e0693",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "blockSlopeEntry",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/slopesafetysystem\",\"params\":{},\"description\":\"Blocks entry to the ski slope at the given location\",\"title\":\"Block Slope Entry\",\"action\":\"blockSlopeEntry\"}",
  "outputToMsg": true,
  "redeploy": "true",
  "x": 640,
  "y": 300,
  "wires": [
   []
  ]
 },
 {
  "id": "a5c5a1521513c390",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "payload",
    "pt": "msg",
    "to": "all",
    "tot": "str"
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 460,
  "y": 300,
  "wires": [
   [
    "71cb6eeb1e1e0693"
   ]
  ]
 },
 {
  "id": "1fd59e532c391d01",
  "type": "system-event-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingEvent": "avalancheDetected",
  "thingEventValue": "{\"uri\":\"http://localhost:8080/avalanchedetector\",\"output\":{\"type\":\"string\",\"description\":\"the location of the avalanche\"},\"description\":\"An event made when an avalanche is detected\",\"title\":\"Avalanche Detected\",\"event\":\"avalancheDetected\"}",
  "outputToMsg": true,
  "redeploy": "true",
  "x": 130,
  "y": 380,
  "wires": [
   [
    "3e818641f2d4aa72",
    "cd0a2a029abe3642",
    "3f8b8579f82a189c",
    "1be6e65fc16c4823"
   ]
  ]
 },
 {
  "id": "3e818641f2d4aa72",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "payload",
    "pt": "msg",
    "to": "{\"role\":\"management\", \"message\":\"Avalanche detected\"}",
    "tot": "jsonata"
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 380,
  "y": 380,
  "wires": [
   [
    "fac8e0deb77702bf"
   ]
  ]
 },
 {
  "id": "fac8e0deb77702bf",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "alertRole",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/alertsystem\",\"params\":{\"role\":\"string\",\"message\":\"string\"},\"description\":\"Alerts the given system role with a provided message\",\"title\":\"Alert Role\",\"action\":\"alertRole\"}",
  "outputToMsg": true,
  "redeploy": "false",
  "x": 540,
  "y": 380,
  "wires": [
   []
  ]
 },
 {
  "id": "cd0a2a029abe3642",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "blockSlopeEntry",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/slopesafetysystem\",\"params\":{},\"description\":\"Blocks entry to the ski slope at the given location\",\"title\":\"Block Slope Entry\",\"action\":\"blockSlopeEntry\"}",
  "outputToMsg": true,
  "redeploy": "true",
  "x": 380,
  "y": 420,
  "wires": [
   []
  ]
 },
 {
  "id": "3f8b8579f82a189c",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "dispatchRescueTeam",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/alertsystem\",\"params\":{},\"description\":\"Sends the rescue team to the provided location\",\"title\":\"Dispatch Rescue Team\",\"action\":\"dispatchRescueTeam\"}",
  "outputToMsg": true,
  "redeploy": "false",
  "x": 400,
  "y": 460,
  "wires": [
   []
  ]
 },
 {
  "id": "1be6e65fc16c4823",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "haltLift",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/slopesafetysystem\",\"params\":{},\"description\":\"Stops the ski lift at the given position from working\",\"title\":\"Halt Lift\",\"action\":\"haltLift\"}",
  "outputToMsg": true,
  "redeploy": "true",
  "x": 350,
  "y": 500,
  "wires": [
   []
  ]
 },
 {
  "id": "50d112aeab0319c2",
  "type": "system-event-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingEvent": "slopeBusynessChange",
  "thingEventValue": "{\"uri\":\"http://localhost:8080/slopesafetysystem\",\"output\":{\"type\":\"object\",\"properties\":{\"location\":{\"type\":\"string\",\"description\":\"The location of the ski slope\"},\"busyness\":{\"type\":\"string\",\"description\":\"The busyness of the provided slope (not busy, moderately busy or crowded)\"}}},\"description\":\"A broadcast of the new busyness level of a ski slope, made when the level changes\",\"title\":\"Slope Busyness Change\",\"event\":\"slopeBusynessChange\"}",
  "outputToMsg": true,
  "redeploy": "false",
  "x": 140,
  "y": 580,
  "wires": [
   [
    "3dcc4fc713d6ea7a"
   ]
  ]
 },
 {
  "id": "2317b087d77a6502",
  "type": "system-property-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingProperty": "liftWaitTime",
  "thingPropertyValue": "{\"uri\":\"http://localhost:8080/slopesafetysystem\",\"type\":\"number\",\"description\":\"Provides an estimate of the current wait time for using a ski lift\",\"title\":\"Lift Wait Time\",\"property\":\"liftWaitTime\"}",
  "mode": "read",
  "redeploy": "true",
  "x": 330,
  "y": 1160,
  "wires": [
   [
    "cb9ad00fecd0b4fc"
   ]
  ]
 },
 {
  "id": "3dcc4fc713d6ea7a",
  "type": "switch",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "property": "payload[\"busyness\"]",
  "propertyType": "msg",
  "rules": [
   {
    "t": "eq",
    "v": "crowded",
    "vt": "str"
   }
  ],
  "checkall": "true",
  "repair": false,
  "outputs": 1,
  "x": 310,
  "y": 580,
  "wires": [
   [
    "5759621705e5379e"
   ]
  ]
 },
 {
  "id": "5759621705e5379e",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "payload",
    "pt": "msg",
    "to": "{\"role\":\"management\", \"message\":\"Crowded slope at \" + msg.payload[\"busyness\"]}",
    "tot": "jsonata"
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 460,
  "y": 580,
  "wires": [
   [
    "cd049db2ad85d0e2"
   ]
  ]
 },
 {
  "id": "cd049db2ad85d0e2",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "alertRole",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/alertsystem\",\"params\":{\"role\":\"string\",\"message\":\"string\"},\"description\":\"Alerts the given system role with a provided message\",\"title\":\"Alert Role\",\"action\":\"alertRole\"}",
  "outputToMsg": true,
  "redeploy": "false",
  "x": 620,
  "y": 580,
  "wires": [
   []
  ]
 },
 {
  "id": "3825aa7fae075ac0",
  "type": "system-event-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingEvent": "rentalGiven",
  "thingEventValue": "{\"uri\":\"http://localhost:8080/rentalsystem\",\"output\":{\"type\":\"object\",\"properties\":{\"rentalID\":{\"type\":\"string\",\"description\":\"The ID of the rental\"},\"customerID\":{\"type\":\"number\",\"description\":\"The ID of the customer that purchased the rental\"}}},\"description\":\"An alert made when a rental is given\",\"title\":\"Rental Given\",\"event\":\"rentalGiven\"}",
  "outputToMsg": true,
  "redeploy": "true",
  "x": 110,
  "y": 640,
  "wires": [
   [
    "bf79b87de6b3a11a"
   ]
  ]
 },
 {
  "id": "d95f937e8c868c1f",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "awaitRentalReturn",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/rentalsystem\",\"params\":{\"rentalID\":\"string\",\"timeout\":\"number\"},\"output\":{\"type\":\"boolean\",\"description\":\"Whether or not the rental was returned. True - The rental was returned, False - The timer expired and the rental was deamed to not have returned\"},\"description\":\"Starts a timer for the specified rental to be completed by. The timer is completed when it expires or the rental is returned\",\"title\":\"Await Rental Return\",\"action\":\"awaitRentalReturn\"}",
  "outputToMsg": true,
  "redeploy": "true",
  "x": 470,
  "y": 640,
  "wires": [
   [
    "e35b346662737408"
   ]
  ]
 },
 {
  "id": "bf79b87de6b3a11a",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "payload",
    "pt": "msg",
    "to": "{\"rentalID\":msg.payload[\"rentalID\"], \"timeout\":3*24*60}",
    "tot": "jsonata"
   },
   {
    "t": "set",
    "p": "customerID",
    "pt": "msg",
    "to": "payload[\"customerID\"]",
    "tot": "msg"
   },
   {
    "t": "set",
    "p": "rentalID",
    "pt": "msg",
    "to": "payload[\"rentalID\"]",
    "tot": "msg"
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 280,
  "y": 640,
  "wires": [
   [
    "d95f937e8c868c1f"
   ]
  ]
 },
 {
  "id": "e35b346662737408",
  "type": "switch",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "property": "payload",
  "propertyType": "msg",
  "rules": [
   {
    "t": "false"
   }
  ],
  "checkall": "true",
  "repair": false,
  "outputs": 1,
  "x": 210,
  "y": 700,
  "wires": [
   [
    "988cfcf3f4d8181d"
   ]
  ]
 },
 {
  "id": "c10d2dd4a336e459",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "notifyCustomer",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/customercontacts\",\"params\":{\"customerID\":\"string\",\"message\":\"string\"},\"description\":\"Notifies the customer with the provided ID of the given message\",\"title\":\"Notify Customer\",\"action\":\"notifyCustomer\"}",
  "outputToMsg": true,
  "redeploy": "false",
  "x": 540,
  "y": 700,
  "wires": [
   [
    "c7311cb0f295fa59"
   ]
  ]
 },
 {
  "id": "988cfcf3f4d8181d",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "payload",
    "pt": "msg",
    "to": "{\"customerID\":msg.customerID, \"message\":\"Renturn your rented equipment or you will be charged\"}",
    "tot": "jsonata"
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 360,
  "y": 700,
  "wires": [
   [
    "c10d2dd4a336e459"
   ]
  ]
 },
 {
  "id": "568963ccb718a8a7",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "awaitRentalReturn",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/rentalsystem\",\"params\":{\"rentalID\":\"string\",\"timeout\":\"number\"},\"output\":{\"type\":\"boolean\",\"description\":\"Whether or not the rental was returned. True - The rental was returned, False - The timer expired and the rental was deamed to not have returned\"},\"description\":\"Starts a timer for the specified rental to be completed by. The timer is completed when it expires or the rental is returned\",\"title\":\"Await Rental Return\",\"action\":\"awaitRentalReturn\"}",
  "outputToMsg": true,
  "redeploy": "true",
  "x": 490,
  "y": 760,
  "wires": [
   [
    "0f403f58d9b51741"
   ]
  ]
 },
 {
  "id": "c7311cb0f295fa59",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "payload",
    "pt": "msg",
    "to": "{\"rentalID\":msg.rentalID, \"timeout\":1*60}",
    "tot": "jsonata"
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 300,
  "y": 760,
  "wires": [
   [
    "568963ccb718a8a7"
   ]
  ]
 },
 {
  "id": "0f403f58d9b51741",
  "type": "switch",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "property": "payload",
  "propertyType": "msg",
  "rules": [
   {
    "t": "false"
   }
  ],
  "checkall": "true",
  "repair": false,
  "outputs": 1,
  "x": 310,
  "y": 820,
  "wires": [
   [
    "06412315affad37c"
   ]
  ]
 },
 {
  "id": "06412315affad37c",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "payload",
    "pt": "msg",
    "to": "{\"role\":\"management\", \"message\":\"Rental \" + msg.rentalID + \" not returned by customer \" + msg.customerID}",
    "tot": "jsonata"
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 460,
  "y": 820,
  "wires": [
   [
    "a03c56a413e81ce2"
   ]
  ]
 },
 {
  "id": "a03c56a413e81ce2",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "alertRole",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/alertsystem\",\"params\":{\"role\":\"string\",\"message\":\"string\"},\"description\":\"Alerts the given system role with a provided message\",\"title\":\"Alert Role\",\"action\":\"alertRole\"}",
  "outputToMsg": true,
  "redeploy": "false",
  "x": 620,
  "y": 820,
  "wires": [
   []
  ]
 },
 {
  "id": "0767b60c8e2b80a3",
  "type": "system-event-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingEvent": "emergencyButtonPressed",
  "thingEventValue": "{\"uri\":\"http://localhost:8080/rentaldevice\",\"output\":{\"type\":\"object\",\"properties\":{\"location\":{\"type\":\"string\",\"description\":\"The current location of this rental device\"},\"rentalID\":{\"type\":\"string\",\"description\":\"The ID of the rental this device is currently assigned too\"}}},\"description\":\"An alert made when a user has pressed the emergency button on this device\",\"title\":\"Emergency Button Pressed\",\"event\":\"emergencyButtonPressed\"}",
  "outputToMsg": true,
  "redeploy": "false",
  "x": 150,
  "y": 880,
  "wires": [
   [
    "59757c00d2759a1f"
   ]
  ]
 },
 {
  "id": "59757c00d2759a1f",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "payload",
    "pt": "msg",
    "to": "{\"role\":\"medicalTeam\", \"message\":\"Emergency at \" + msg.payload[\"location\"] + \", reported by emercency button by rental \" + msg.payload[\"rentalID\"]}",
    "tot": "jsonata"
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 360,
  "y": 880,
  "wires": [
   [
    "64a3a58158924b8d"
   ]
  ]
 },
 {
  "id": "64a3a58158924b8d",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "alertRole",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/alertsystem\",\"params\":{\"role\":\"string\",\"message\":\"string\"},\"description\":\"Alerts the given system role with a provided message\",\"title\":\"Alert Role\",\"action\":\"alertRole\"}",
  "outputToMsg": true,
  "redeploy": "false",
  "x": 520,
  "y": 880,
  "wires": [
   []
  ]
 },
 {
  "id": "a5ddc18b46832734",
  "type": "system-event-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingEvent": "liftMalfunction",
  "thingEventValue": "{\"uri\":\"http://localhost:8080/slopesafetysystem\",\"output\":{\"type\":\"string\",\"description\":\"The location of the lift\"},\"description\":\"An event made when a lift malfunctions\",\"title\":\"Lift Malfunction\",\"event\":\"liftMalfunction\"}",
  "outputToMsg": true,
  "redeploy": "true",
  "x": 110,
  "y": 940,
  "wires": [
   [
    "10fa36d7575ca6ac"
   ]
  ]
 },
 {
  "id": "10fa36d7575ca6ac",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "payload",
    "pt": "msg",
    "to": "{\"role\":\"maintnanceTeam\", \"message\":\"Lift malfunction at \" + msg.payload}",
    "tot": "jsonata"
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 280,
  "y": 940,
  "wires": [
   [
    "6fcd64ac3004a4a8"
   ]
  ]
 },
 {
  "id": "6fcd64ac3004a4a8",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "alertRole",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/alertsystem\",\"params\":{\"role\":\"string\",\"message\":\"string\"},\"description\":\"Alerts the given system role with a provided message\",\"title\":\"Alert Role\",\"action\":\"alertRole\"}",
  "outputToMsg": true,
  "redeploy": "false",
  "x": 440,
  "y": 940,
  "wires": [
   []
  ]
 },
 {
  "id": "a9e1eb551b358025",
  "type": "system-event-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingEvent": "requestWeatherConditions",
  "thingEventValue": "{\"uri\":\"http://localhost:8080/userdevice\",\"output\":{},\"description\":\"A user request for the current weather conditions of the ski slopes\",\"title\":\"Request Weather Conditions\",\"event\":\"requestWeatherConditions\"}",
  "outputToMsg": true,
  "redeploy": "false",
  "x": 150,
  "y": 1020,
  "wires": [
   [
    "e4ca3e5d23c48aca"
   ]
  ]
 },
 {
  "id": "22c35c331cd707d5",
  "type": "system-event-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingEvent": "requestSlopeDetails",
  "thingEventValue": "{\"uri\":\"http://localhost:8080/userdevice\",\"output\":{},\"description\":\"A user request for dentails about the ski slopes, concerning their busyness and lift wait times\",\"title\":\"Request Slope Details\",\"event\":\"requestSlopeDetails\"}",
  "outputToMsg": true,
  "redeploy": "true",
  "x": 130,
  "y": 1120,
  "wires": [
   [
    "24bdb0b6f7063c7b"
   ]
  ]
 },
 {
  "id": "f0b4199741b59619",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "receiveWeatherConditions",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/userdevice\",\"params\":{},\"description\":\"Relays the given weather conditions to the user of this device\",\"title\":\"Receive Weather Conditions\",\"action\":\"receiveWeatherConditions\"}",
  "outputToMsg": true,
  "redeploy": "true",
  "x": 600,
  "y": 1020,
  "wires": [
   []
  ]
 },
 {
  "id": "424f6d69a2e258a9",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "receiveSlopeDetails",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/userdevice\",\"params\":{},\"description\":\"Passes the details of slope busyness and lift wait times to the user of this device\",\"title\":\"Receive Slope Details\",\"action\":\"receiveSlopeDetails\"}",
  "outputToMsg": true,
  "redeploy": "false",
  "x": 540,
  "y": 1220,
  "wires": [
   []
  ]
 },
 {
  "id": "e4ca3e5d23c48aca",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "getWeatherDetails",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/weathermonitor\",\"params\":{},\"output\":{\"type\":\"string\",\"description\":\"A textual description of the slope weather conditions\"},\"description\":\"Gets all weater details for the ski slopes\",\"title\":\"Get Weather Details\",\"action\":\"getWeatherDetails\"}",
  "outputToMsg": true,
  "redeploy": "false",
  "x": 370,
  "y": 1020,
  "wires": [
   [
    "f0b4199741b59619"
   ]
  ]
 },
 {
  "id": "24bdb0b6f7063c7b",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "getSlopeBusyness",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/slopesafetysystem\",\"params\":{},\"output\":{\"type\":\"string\",\"description\":\"Details about the busyness of each ski slope\"},\"description\":\"Gets the busyness of the various ski slopes\",\"title\":\"Get Slope Busyness\",\"action\":\"getSlopeBusyness\"}",
  "outputToMsg": true,
  "redeploy": "true",
  "x": 350,
  "y": 1120,
  "wires": [
   [
    "92bfea7ae950bbe5"
   ]
  ]
 },
 {
  "id": "92bfea7ae950bbe5",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "busyness",
    "pt": "msg",
    "to": "payload",
    "tot": "msg",
    "dc": true
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 550,
  "y": 1120,
  "wires": [
   [
    "2317b087d77a6502"
   ]
  ]
 },
 {
  "id": "cb9ad00fecd0b4fc",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "waitTime",
    "pt": "msg",
    "to": "payload",
    "tot": "msg",
    "dc": true
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 510,
  "y": 1160,
  "wires": [
   [
    "44b1fc728bd34d8d"
   ]
  ]
 },
 {
  "id": "44b1fc728bd34d8d",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "payload",
    "pt": "msg",
    "to": "{\"busyness\":msg.busyness, \"waitTime\":msg.waitTime}",
    "tot": "jsonata",
    "dc": true
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 340,
  "y": 1220,
  "wires": [
   [
    "424f6d69a2e258a9"
   ]
  ]
 },
 {
  "id": "f5f283d710e7f263",
  "type": "system-event-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingEvent": "resortEnergyUsage",
  "thingEventValue": "{\"uri\":\"http://localhost:8080/resortactuators\",\"output\":{\"type\":\"number\",\"description\":\"The current energy usage\"},\"description\":\"An event made when there is a fluctuation in energy usage within the resort\",\"title\":\"Resort Energy Usage Change\",\"event\":\"resortEnergyUsage\"}",
  "outputToMsg": true,
  "redeploy": "false",
  "x": 130,
  "y": 1320,
  "wires": [
   [
    "1d59f4f68cc9d354"
   ]
  ]
 },
 {
  "id": "1d59f4f68cc9d354",
  "type": "switch",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "property": "payload",
  "propertyType": "msg",
  "rules": [
   {
    "t": "gt",
    "v": "200",
    "vt": "str"
   }
  ],
  "checkall": "true",
  "repair": false,
  "outputs": 1,
  "x": 290,
  "y": 1320,
  "wires": [
   [
    "2a03e0578d8ca45b",
    "80254542c4e0fe51",
    "291469263ce79d8f"
   ]
  ]
 },
 {
  "id": "2a03e0578d8ca45b",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "payload",
    "pt": "msg",
    "to": "{\"role\":\"facilitiesManager\", \"message\":\"High energy usage at the resort\"}",
    "tot": "jsonata"
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 460,
  "y": 1320,
  "wires": [
   [
    "e057a15d9fd46e63"
   ]
  ]
 },
 {
  "id": "e057a15d9fd46e63",
  "type": "system-action-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingAction": "alertRole",
  "thingActionValue": "{\"uri\":\"http://localhost:8080/alertsystem\",\"params\":{\"role\":\"string\",\"message\":\"string\"},\"description\":\"Alerts the given system role with a provided message\",\"title\":\"Alert Role\",\"action\":\"alertRole\"}",
  "outputToMsg": true,
  "redeploy": "false",
  "x": 620,
  "y": 1320,
  "wires": [
   []
  ]
 },
 {
  "id": "80254542c4e0fe51",
  "type": "system-property-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingProperty": "resortHeating",
  "thingPropertyValue": "{\"uri\":\"http://localhost:8080/resortactuators\",\"type\":\"number\",\"description\":\"The current temperature of the heaters in the ski resort\",\"title\":\"Resort Heating\",\"property\":\"resortHeating\"}",
  "mode": "read",
  "redeploy": "false",
  "x": 460,
  "y": 1380,
  "wires": [
   [
    "76f32a9eb9cd0e14"
   ]
  ]
 },
 {
  "id": "291469263ce79d8f",
  "type": "system-property-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingProperty": "resortLighting",
  "thingPropertyValue": "{\"uri\":\"http://localhost:8080/resortactuators\",\"type\":\"number\",\"description\":\"The current brightness of the lighting in the ski resort\",\"title\":\"Resort Heating\",\"property\":\"resortLighting\"}",
  "mode": "read",
  "redeploy": "true",
  "x": 460,
  "y": 1420,
  "wires": [
   [
    "629364c293483f31"
   ]
  ]
 },
 {
  "id": "76f32a9eb9cd0e14",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "payload",
    "pt": "msg",
    "to": "msg.payload - 1",
    "tot": "jsonata"
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 640,
  "y": 1380,
  "wires": [
   [
    "a6daf6833020e50f"
   ]
  ]
 },
 {
  "id": "629364c293483f31",
  "type": "change",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "rules": [
   {
    "t": "set",
    "p": "payload",
    "pt": "msg",
    "to": "msg.payload - 1",
    "tot": "jsonata"
   }
  ],
  "action": "",
  "property": "",
  "from": "",
  "to": "",
  "reg": false,
  "x": 640,
  "y": 1420,
  "wires": [
   [
    "2f9954c2e323c90e"
   ]
  ]
 },
 {
  "id": "a6daf6833020e50f",
  "type": "system-property-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingProperty": "resortHeating",
  "thingPropertyValue": "{\"uri\":\"http://localhost:8080/resortactuators\",\"type\":\"number\",\"description\":\"The current temperature of the heaters in the ski resort\",\"title\":\"Resort Heating\",\"property\":\"resortHeating\"}",
  "mode": "write",
  "redeploy": "false",
  "x": 820,
  "y": 1380,
  "wires": [
   []
  ]
 },
 {
  "id": "2f9954c2e323c90e",
  "type": "system-property-node",
  "z": "c348ea29f9cebfd1",
  "name": "",
  "thingDirectoryURI": "http://localhost:8080/thingdirectory",
  "thingProperty": "resortLighting",
  "thingPropertyValue": "{\"uri\":\"http://localhost:8080/resortactuators\",\"type\":\"number\",\"description\":\"The current brightness of the lighting in the ski resort\",\"title\":\"Resort Heating\",\"property\":\"resortLighting\"}",
  "mode": "write",
  "redeploy": "true",
  "x": 820,
  "y": 1420,
  "wires": [
   []
  ]
 }
]
----

Your job is to take new IoT system proposals/descriptions (from users) along with a list the devices that are available to use (as WoT Thing descriptions). From this information, you will produce an IoT system workflow, for use within Node-RED, which connects the relevant Things/devices in order to satisfy the requirements of the provided system proposal/description.
```

User Prompt:

```
System proposal/description:
When the door bell is pressed, reduce the speaker volume, make the smart assistant alert the homeowner of the doorbell, return the speaker's volume.

Things/devices available:
[
{
 "@context": [
  "http://www.w3.org/ns/td"
 ],
 "@type": [
  "Thing"
 ],
 "title": "DoorBell",
 "securityDefinitions": {
  "no_sec": {
   "scheme": "nosec"
  }
 },
 "security": "no_sec",
 "actions": {},
 "properties": {},
 "events": {
  "bellRung":{
   "title": "Bell rung",
   "description": "The bell was rung",
   "subscription": {},
   "data": {
    "type": "null"
   },
   "cancellation": {},
   "forms": []
  }
 }
},
{
 "@context": [
  "http://www.w3.org/ns/td"
 ],
 "@type": [
  "Thing"
 ],
 "title": "Speaker",
 "securityDefinitions": {
  "no_sec": {
   "scheme": "nosec"
  }
 },
 "security": "no_sec",
 "actions": {
  "setVolume":{
   "type": "",
   "title": "Set volume",
   "description": "Sets the volume of this speaker",
   "input": {
    "type": "object",
    "properties":{
     "percentage": {
      "type": "integer",
      "description": "The volume percentage to set this speaker to"
     }
    }
   },
   "forms": []
  },
  "getVolume":{
   "type": "",
   "title": "Get volume",
   "description": "Gets the volume of this speaker",
   "output": {
    "type": "integer"
   },
   "forms": []
  }
 },
 "properties": {},
 "events": {}
},
{
 "@context": [
  "http://www.w3.org/ns/td"
 ],
 "@type": [
  "Thing"
 ],
 "title": "SmartAssistant",
 "securityDefinitions": {
  "no_sec": {
   "scheme": "nosec"
  }
 },
 "security": "no_sec",
 "actions": {
  "say":{
   "type": "",
   "title": "Say phrase",
   "description": "Makes the assistant say the given phrase",
   "input": {
    "type": "object",
    "properties":{
     "phrase":{
      "type": "string",
      "description": "The phrase to be spoken by this assistant"
     }
    }
   },
   "forms": []
  }
 },
 "properties": {},
 "events": {}
},
{
 "@context": [
  "http://www.w3.org/ns/td"
 ],
 "@type": [
  "Thing"
 ],
 "title": "WashingMachine",
 "securityDefinitions": {
  "no_sec": {
   "scheme": "nosec"
  }
 },
 "security": "no_sec",
 "actions": {},
 "properties": {},
 "events": {
  "finishedCycle":{
   "title": "Wash cycle complete",
   "description": "Sends a notification at the end of a wash cycle",
   "subscription": {},
   "data": {
    "type": "null"
   },
   "cancellation": {},
   "forms": []
  }
 }
}
]
```

Output:

```
Lost
```