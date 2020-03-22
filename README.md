Node-Red-Nuki-Push
==================

This Node-RED flow shows how to react on Nuki Smart Lock state changes via push without constantly polling the API.
The flow uses the Nuki Bridge API to get the trigger for the changed state and afterwards the Nuki Web API to request the current state for the Nuki Smart Lock.

![Flow overview](https://github.com/CNpunkt/Node-Red-Nuki-Push/blob/master/Ressources/Images/Flow%20overview.png "Flow overview")

## Requirements
 - Nuki Smart Lock
 - Nuki Bridge
 - Enabled Nuki Bridge HTTP API (see steps below)



## Configuration
### Enable the Nuki Bridge HTTP API
1. Open the Nuki Bridge configuration in the Nuki App on your smartphone
<img src="https://github.com/CNpunkt/Node-Red-Nuki-Push/blob/master/Ressources/Images/Open%20Nuki%20Bride%20configuration.png" width="300"> 

2. Enable the HTTP API and remember the IP address, the port and the API token for later use
<img src="https://github.com/CNpunkt/Node-Red-Nuki-Push/blob/master/Ressources/Images/Enable%20HTTP%20API.png" width="300">



### Register a callback HTTP endpoint in the Nuki Bridge
The HTTP endpoint will be triggered as soon as the state of the Nuki Smart Lock changes. With the following steps a Node-RED HTTP endpoint will be registered in the Nuki Bridge.

1. Download any prefered tool for sending a HTTP request, for example [Postman](https://www.postman.com/)

2. Build the URL for the request using the informations of step 2 (see above) to register the callback endpoint in the Nuki Bridge:
 - http://**Nuki Bridge IP address**:**Port**/callback/add?url=http%3A%2F%2F**Node-RED IP address**%2Fnuki&token=**API token**
 - Example: http://**192.168.178.208**:**8080**/callback/add?url=http%3A%2F%2F**192.168.178.202**%2Fnuki&token=**4711**

3. Send the get-request using the previous URL to the Nuki Bridge. The response should look like this:
![Callback registered](https://github.com/CNpunkt/Node-Red-Nuki-Push/blob/master/Ressources/Images/Callback%20registered.png "Callback registered")

4. (Optional) Check the registered callbacks by sending a request to the Nuki Bridge by using the following URL: http://**Nuki Bridge IP address**:**Port**/callback/list?token=**API token**

![Callback list](https://github.com/CNpunkt/Node-Red-Nuki-Push/blob/master/Ressources/Images/Callback%20list.png "Callback list")



### Activate the Nuki Web API
1. Open [https://web.nuki.io/](https://web.nuki.io/) and create an account

2. Open the API section on the website and create a new API token
![Generate Web API Token](https://github.com/CNpunkt/Node-Red-Nuki-Push/blob/master/Ressources/Images/Generate%20Web%20API%20Token.png "Generate Web API Token")
![Generate Web API Token2](https://github.com/CNpunkt/Node-Red-Nuki-Push/blob/master/Ressources/Images/Generate%20Web%20API%20Token2.png "Generate Web API Token2")

3. Send a HTTP get-request to the Nuki Web API, for example by using postman, to get the Nuki Smart Lock ID (use the previously generated Web API token). URL for the request: https://api.nuki.io/smartlock
![HTTP Request Web API Smartlocks](https://github.com/CNpunkt/Node-Red-Nuki-Push/blob/master/Ressources/Images/HTTP%20Request%20Web%20API%20get%20Smartlocks.png "HTTP Request Web API Smartlocks")

4. Remember the smartlockId for later use:
![HTTP Request Web API smartlockId](https://github.com/CNpunkt/Node-Red-Nuki-Push/blob/master/Ressources/Images/HTTP%20Request%20Web%20API%20smartlockID.png "HTTP Request Web API smartlockId")



### Configure the Node-RED flow
1. The following node will be triggered by the Nuki Bridge using the previously registered callback when the Nuki Smart Lock state changes.
<img src="https://github.com/CNpunkt/Node-Red-Nuki-Push/blob/master/Ressources/Images/Triggered%20node.png">
![Endpoint node config](https://github.com/CNpunkt/Node-Red-Nuki-Push/blob/master/Ressources/Images/Endpoint%20node%20config.png "Endpoint node config")

2. Store the smartlockId and the Web API token in the credentials node. The node forwards these informations to the HTTP request node which requests the Nuki Smart Lock state from the Web API.
![Credentials node](https://github.com/CNpunkt/Node-Red-Nuki-Push/blob/master/Ressources/Images/Credentials%20node.png "Credentials node")
![Credentials node config](https://github.com/CNpunkt/Node-Red-Nuki-Push/blob/master/Ressources/Images/Credentials%20node%20config.png "Credentials node config")
