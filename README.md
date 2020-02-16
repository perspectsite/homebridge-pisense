# homebridge-pisense

This [Homebridge](https://github.com/nfarina/homebridge) plugin can be used integrate your Raspberry Pi Sense Hat into HomeKit.  It also requires [Flask PiSense](https://github.com/perspectsite/flask-pisense) which is a Flask-based HTTP server that interfaes with the Sense Hat.

## Installation

First of all you need to have [Homebridge](https://github.com/nfarina/homebridge) installed. Refer to the repo for 
instructions.  
Then run the following command to install `homebridge-pisense`

```
sudo npm install -g homebridge-pisense
```

## Configuration

The configuration can contain the following properties:

##### Basic configuration options:

* `accessory` \<string\> **required**: Defines the plugin used and must be set to **"HTTP-HUMIDITY"** for this plugin.
* `name` \<string\> **required**: Defines the name which is later displayed in HomeKit
* `getUrl` \<string |  [urlObject](#urlobject)\> **required**: Defines the url (and other properties when using 
    and urlObject) to query the current humidity from the sensor. By default it expects the http server 
    to return the humidity in percent.

```json
{
    "accessories": [
        {
          "accessory": "HTTP-HUMIDITY",
          "name": "Humidity Sensor",
          "getUrl": "http://ADDRESS_OF_FLASK_SENSE"
        }   
    ]
}
```

##### Advanced configuration options:

* `statusCache` \<number\> **optional** \(Default: **0**\): Defines the amount of time in milliseconds a queried value 
   of the _CurrentRelativeHumidity_ characteristic is cached before a new request is made to the http device.  
   Default is **0** which indicates no caching. A value of **-1** will indicate infinite caching.

- `pullInterval` \<integer\> **optional**: The property expects an interval in **milliseconds** in which the plugin 
    pulls updates from your http device. For more information read [pulling updates](#the-pull-way).

- `debug` \<boolean\> **optional**: Enable debug mode and write more logs.

```json
{
    "accessories": [
        {
          "accessory": "HTTP-HUMIDITY",
          "name": "Humidity Sensor",
          
          "getUrl": {
            "url": "http://ADDRESS_OF_FLASK_SENSE",
            "method": "GET"
          }
        }   
    ]
}
```
