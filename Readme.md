# Hackathon II - Drone API

## Getting Started

### WiFi Setup
1. Connect to the raspberry Pi controller by WiFi
  * **SSID**: DronePiFi
  * **Password**: Drones123
  * Note: Once connected to the WiFi you won't have internet access anymore, and will need to switch to another WiFi if you need to download anything
2. If using your work laptop, disable proxy settings  
  a. Click windows 'Start' button  
  b. Type `Internet Options`, and select it from the menu  
  c. On the Connections tab, click the 'LAN settings' button  
  d. Uncheck all the checkboxes and click OK  
  e. Click OK on the Internet Options window  
  

### Before you Start
* **Note the DroneId of your drone.** It's written on your drone's box. You'll need to pass it to all the API calls (So you're controlling the right drone!)
* The API is hosted by the Raspberry Pi at http://192.168.4.1:8081/ All api calls should be made against this address.
* All the code examples below use JQuery. You don't have to use JQuery- any way to make HTTP GET requests will do. If you do decide to use JQuery you'll need to include it the library. You can download from https://jquery.com/download/, save it in the same directory as your HTML file and then include it with the following:
```HTML
<script src="jquery-3.4.1.min.js"></script>
```
* The drone can only do 1 thing at a time. **If you send a request while your drone is busy doing something else, it'll return a 409 response code (HTTP Conflict)** and the following request body:
```json
  {
    "success": false,
    "error": "Drone not ready"
  }
```
* All successful API calls will return with a 200 response (HTTP Success) and the follwing body:
```json
  {
    "success": true
  }
```

## API  
#### - Connect
Connect to the Drone. This method must be called before any other action can be executed.
This can also be used to reconnect if the drone becomes unresponsive.  
**Endpoint:** /connect?droneId=[droneId]  
**Method:** GET  
**Parameters:**  
droneId - _The ID of your drone_  
**Example Code:**
```javascript
$.getJSON('http://192.168.4.1:8081/connect?droneId=MyDroneId')
  .done(function() {
    //The connection was successful! We can do something here
  })
  .fail(function(err) {
    //The call failed, we can check the HTTP status with err.status, or the response body with err.responseJSON
  });
```
#### - Take Off
**Endpoint:** /takeoff?droneId=[droneId]  
**Method:** GET  
**Parameters:**  
droneId - _The ID of your drone_  
**Example Code:**
```javascript
$.getJSON('http://192.168.4.1:8081/takeoff?droneId=MyDroneId')
  .done(function() {
    //The connection was successful! We can do something here
  })
  .fail(function(err) {
    //The call failed, we can check the HTTP status with err.status, or the response body with err.responseJSON
  });
```
#### - Land
**Endpoint:** /land?droneId=[droneId]  
**Method:** GET  
**Parameters:**  
droneId - _The ID of your drone_  
**Example Code:**
```javascript
$.getJSON('http://192.168.4.1:8081/land?droneId=MyDroneId')
  .done(function() {
    //The connection was successful! We can do something here
  })
  .fail(function(err) {
    //The call failed, we can check the HTTP status with err.status, or the response body with err.responseJSON
  });
```
#### - Movement
**Endpoint:** /move?droneId=[droneId]&direction=[direction]&speed=[speed]&steps=[steps]  
**Method:** GET  
**Parameters:**  
droneId - _The ID of your drone_  
direction - _How you want the drone to move. Valid values [up, down, forward, backward, right, left, turnRight, turnLeft]_  
steps - _number 0-100 of steps you want to move_  
speed - _number 0-100 at what speed you want to move_  
**Example Code:**
```javascript
$.getJSON('http://192.168.4.1:8081/move?droneId=MyDroneId&direction=forward&steps=20&speed=20')
  .done(function() {
    //The connection was successful! We can do something here
  })
  .fail(function(err) {
    //The call failed, we can check the HTTP status with err.status, or the response body with err.responseJSON
  });
```
#### - Flip
**Endpoint:** /land?droneId=[droneId]  
**Method:** GET  
**Parameters:**  
droneId - _The ID of your drone_  
direction - _How you want the drone to move. Valid values [up, down, forward, backward, right, left, turnRight, turnLeft]_  

**Example Code:**
```javascript
$.getJSON('http://192.168.4.1:8081/move?droneId=MyDroneId&direction=forward&steps=20&speed=20')
  .done(function() {
    //The connection was successful! We can do something here
  })
  .fail(function(err) {
    //The call failed, we can check the HTTP status with err.status, or the response body with err.responseJSON
  });
```
