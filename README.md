Node-Red-Nuki-Push
==================

This Node-RED flow shows how to react on Nuki Smart Lock state changes via push without constantly polling the API.

![Flow overview](https://github.com/CNpunkt/Node-Red-Nuki-Push/blob/master/Ressources/Images/Flow%20overview.png "Flow overview")

## Requirements
 - Nuki Smart Lock
 - Nuki Bridge
 - Enabled HTTP Bridge API

## Configuration
### Enable HTTP Bridge API
1. Open the Nuki Bridge configuration in the Nuki App on your smartphone
![Open Bridge Configuration](https://github.com/CNpunkt/Node-Red-Nuki-Push/blob/master/Ressources/Images/Open%20Nuki%20Bride%20configuration.png "Open Bridge Configuration")

2. Enable the HTTP API and save the IP address, the port and the API token for later use
![Enable HTTP API](https://github.com/CNpunkt/Node-Red-Nuki-Push/blob/master/Ressources/Images/Enable%20HTTP%20API.png "Enable HTTP API")

### Register a callback HTTP endpoint in the Nuki Bridge
The HTTP endpoint will be triggered as soon as the state of the Nuki Smart Lock changes

1. Download any prefered tool for sending a HTTP request, for example [Postman](https://www.postman.com/)
2. Build the URL for the request using the informations of step 2 (see above):
 *  http://<IP address>:<port>/callback/add
 *  
3. We want to register the HTTP endpoint on our Node-RED server. Therefore the URL for the request needs 