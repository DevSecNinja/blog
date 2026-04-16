---
title: 'Use the Sonos API to gather alarm data'
date: 2019-12-15T12:30:29+00:00
draft: false
tags: ['Automation', 'Domotica', 'Home Automation', 'Node-RED', 'Sonos']
description: ""
cover:
  image: ""
  alt: ""
---

**My alarm clock setup is based on a Sonos One that plays music and [Home Assistant in combination with DeCONZ](http://DevSecNinja.com/2019/08/03/bye-philips-hue-xiaomi-bridge/) and Node-RED to automate my bedroom lights as a wake up light. I could also control the music to the Sonos One from Home Assistant, but I don't want to rely on my home automation setup for me to wake up.

Currently, the Home Assistant integration does not get the alarm data itself, but luckily the Sonos API is easily accessible!**

In this blog post, I'm going to explain two methods that you can use to gather the alarm clock data: PowerShell and Node-RED.

## PowerShell

First of all, you can use PowerShell by running the script below. Make sure to change the variables on top before you run the script:

```
#region Variables
# Sonos Settings - Edit where necessary
$sonosIP = "192.168.1.10"
$port = 1400

# SOAP - Do not edit
$uri = "http://${sonosIP}:$port/AlarmClock/Control"
$soapAction = "urn:schemas-upnp-org:service:AlarmClock:1#ListAlarms"
$soapMessage = '<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/" s:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/"><s:Body><u:ListAlarms xmlns:u="urn:schemas-upnp-org:service:AlarmClock:1"><InstanceID>0</InstanceID></u:ListAlarms></s:Body></s:Envelope>'
#endregion

#region Execution
# Create SOAP Request
$soapRequest = \[System.Net.WebRequest\]::Create($uri)

# Set Headers
$soapRequest.Accept = 'gzip'
$soapRequest.Method = 'POST'
$soapRequest.ContentType = 'text/xml; charset="utf-8"'
$soapRequest.KeepAlive = $false
$soapRequest.Headers.Add("SOAPACTION", $soapAction)

# Sending SOAP Request
$requestStream = $soapRequest.GetRequestStream()
$soapMessage = \[xml\] $soapMessage
$soapMessage.Save($requestStream)
$requestStream.Close()

# Sending Complete, Get Response
$response = $soapRequest.GetResponse()
$responseStream = $response.GetResponseStream()
$soapReader = \[System.IO.StreamReader\]($responseStream)
$returnXml = \[Xml\] $soapReader.ReadToEnd() 
$responseStream.Close()
#endregion

# Get alarms
((\[xml\]$returnXml.Envelope.Body.ListAlarmsResponse.CurrentAlarmList).Alarms.Alarm)\[0\]
```

After running this script, you will see that it will return the first alarm. If you want to search for other alarms, you can play with the _$returnXml_ variable.

## Node-RED

As I'm using Node-RED extensively with Home Assistant, I can integrate a SOAP request pretty easily with Node-RED. All we need is the _node-red-contrib-simple-soap_ package, which you can add to your Hass.io Node-RED configuration for easy installation:

```
"npm\_packages": \[
  "node-red-contrib-simple-soap"
\]
```

We apply the same logic as we used in PowerShell to Node-RED, to end up with something like this:

![Node-RED-Sonos](/images/2019/12/node-red-sonos-2.png)

Flow in Node-RED that gathers the Sonos alarm clock data

In this scenario, I trigger a flow every minute, which:

1. Sends out the SOAP Request
2. Parses the XML that comes from the SOAP request
3. Grabs the alarm time & state from the first alarm
   1. Sets the time on the Sonos alarm sensor
   2. Sets the Sonos alarm boolean to True or False

You can easily add the Sonos alarm inputs to your Home Assistant configuration:

```
\# Input booleans
input\_boolean:
  wakeup\_sonos\_alarm\_enabled:
    name: "Sonos Alarm Enabled"
    icon: mdi:theme-light-dark
# Input date time
input\_datetime:
  wakeup\_sonos\_alarm\_time:
    name: "Sonos Alarm Time"
    has\_time: true
    has\_date: false
```

After you've rebooted your Home Assistant, the sensor should come up with the new inputs. Import the flow below into Node-RED and make sure you configure your own Home Assistant server and change the IP address of the Sonos in the SOAP request.

```
\[{"id":"721f6847.34cc88","type":"simple-soap","z":"24b5739b.054a3c","host":"http://192.168.1.10:1400","hostType":"str","path":"AlarmClock/Control","pathType":"str","action":"urn:schemas-upnp-org:service:AlarmClock:1#ListAlarms","actionType":"str","body":"'<s:Envelope xmlns:s=\\"http://schemas.xmlsoap.org/soap/envelope/\\" s:encodingStyle=\\"http://schemas.xmlsoap.org/soap/encoding/\\"><s:Body><u:ListAlarms xmlns:u=\\"urn:schemas-upnp-org:service:AlarmClock:1\\"><InstanceID>0</InstanceID></u:ListAlarms></s:Body></s:Envelope>'","bodyType":"msg","mustache":false,"attrkey":"$","charkey":"\_","stripPrefix":false,"simplify":false,"normalizeTags":false,"normalize":false,"topic":"","name":"SOAP Request","useAuth":false,"x":400,"y":1940,"wires":\[\["90be7158.69234"\]\]},{"id":"e9a4e1fc.10c98","type":"inject","z":"24b5739b.054a3c","name":"Every minute","topic":"","payload":"","payloadType":"date","repeat":"60","crontab":"","once":true,"onceDelay":0.1,"x":140,"y":1940,"wires":\[\["721f6847.34cc88"\]\]},{"id":"90be7158.69234","type":"xml","z":"24b5739b.054a3c","name":"Parse XML","property":"payload\[\\"s:Envelope\\"\]\[\\"s:Body\\"\]\[\\"u:ListAlarmsResponse\\"\].CurrentAlarmList","attr":"","chr":"","x":130,"y":2060,"wires":\[\["2884e5f3.9198ca","c8f07bd4.b12338"\]\]},{"id":"2884e5f3.9198ca","type":"change","z":"24b5739b.054a3c","name":"Set time payload","rules":\[{"t":"set","p":"payload","pt":"msg","to":"payload\[\\"s:Envelope\\"\]\[\\"s:Body\\"\]\[\\"u:ListAlarmsResponse\\"\].CurrentAlarmList.Alarms.Alarm\[0\].$.StartTime","tot":"msg"}\],"action":"","property":"","from":"","to":"","reg":false,"x":410,"y":2040,"wires":\[\["c6a9b36.c1ebd5"\]\]},{"id":"c6a9b36.c1ebd5","type":"api-call-service","z":"24b5739b.054a3c","name":"Set Sonos alarm sensor","server":"47f73e49.02b17","version":1,"debugenabled":false,"service\_domain":"input\_datetime","service":"set\_datetime","entityId":"input\_datetime.wakeup\_sonos\_alarm\_time","data":"{\\"time\\":\\"{{payload}}\\"}","dataType":"json","mergecontext":"","output\_location":"","output\_location\_type":"none","mustacheAltTags":false,"x":710,"y":2040,"wires":\[\[\]\]},{"id":"c8f07bd4.b12338","type":"change","z":"24b5739b.054a3c","name":"Set enabled payload","rules":\[{"t":"set","p":"payload","pt":"msg","to":"payload\[\\"s:Envelope\\"\]\[\\"s:Body\\"\]\[\\"u:ListAlarmsResponse\\"\].CurrentAlarmList.Alarms.Alarm\[0\].$.Enabled","tot":"msg"}\],"action":"","property":"","from":"","to":"","reg":false,"x":420,"y":2100,"wires":\[\["3e848197.6a535e"\]\]},{"id":"235cde14.721e92","type":"api-call-service","z":"24b5739b.054a3c","name":"Disable Sonos alarm boolean","server":"47f73e49.02b17","version":1,"debugenabled":false,"service\_domain":"input\_boolean","service":"turn\_off","entityId":"input\_boolean.wakeup\_sonos\_alarm\_enabled","data":"","dataType":"json","mergecontext":"","output\_location":"","output\_location\_type":"none","mustacheAltTags":false,"x":1060,"y":2060,"wires":\[\[\]\]},{"id":"3e848197.6a535e","type":"switch","z":"24b5739b.054a3c","name":"Enable or Disable","property":"payload","propertyType":"msg","rules":\[{"t":"eq","v":"0","vt":"str"},{"t":"eq","v":"1","vt":"str"}\],"checkall":"true","repair":false,"outputs":2,"x":690,"y":2100,"wires":\[\["235cde14.721e92"\],\["483dac88.5925a4"\]\]},{"id":"483dac88.5925a4","type":"api-call-service","z":"24b5739b.054a3c","name":"Enable Sonos alarm boolean","server":"47f73e49.02b17","version":1,"debugenabled":false,"service\_domain":"input\_boolean","service":"turn\_on","entityId":"input\_boolean.wakeup\_sonos\_alarm\_enabled","data":"","dataType":"json","mergecontext":"","output\_location":"","output\_location\_type":"none","mustacheAltTags":false,"x":1060,"y":2140,"wires":\[\[\]\]},{"id":"47f73e49.02b17","type":"server","z":"","name":"Home Assistant","legacy":false,"hassio":true,"rejectUnauthorizedCerts":true,"ha\_boolean":"y|yes|true|on|home|open","connectionDelay":true}\]
```

Now you can use this new sensor to automate other things like enabling the bedroom lights when the Sonos alarm is set, or turn on the coffee machine after waking up!

Let me know how you will use this new flow to automate your home!
