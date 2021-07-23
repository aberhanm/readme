<!-- Generated automatically, DO NOT EDIT! -->
<a name="head.Channel_Plugin"></a>
# Cable

**Version: 1.0**

**Status: :black_circle::black_circle::black_circle:**

<!--org.rdk.Cable plugin for Thunder framework.-->

### Table of Contents

- [Introduction](#head.Introduction)
- [Configuration](#head.Configuration)
- [Methods](#head.Methods)
- [Notifications](#head.Notifications)

<a name="head.Introduction"></a>
# Introduction

<a name="head.Scope"></a>
## Scope

This document describes purpose and functionality of the org.rdk.Cable plugin. It includes detailed specification about its configuration, methods provided and notifications sent.

<a name="head.Case_Sensitivity"></a>
## Case Sensitivity

All identifiers of the interfaces described in this document are case-sensitive. Thus, unless stated otherwise, all keywords, entities, properties, relations and actions should be treated as such.

<a name="head.Acronyms,_Abbreviations_and_Terms"></a>
## Acronyms, Abbreviations and Terms

The table below provides and overview of acronyms used in this document and their definitions.

| Acronym | Description |
| :-------- | :-------- |
| <a name="acronym.API">API</a> | Application Programming Interface |
| <a name="acronym.HTTP">HTTP</a> | Hypertext Transfer Protocol |
| <a name="acronym.JSON">JSON</a> | JavaScript Object Notation; a data interchange format |
| <a name="acronym.JSON-RPC">JSON-RPC</a> | A remote procedure call protocol encoded in JSON |

The table below provides and overview of terms and abbreviations used in this document and their definitions.

| Term | Description |
| :-------- | :-------- |
| <a name="term.callsign">callsign</a> | The name given to an instance of a plugin. One plugin can be instantiated multiple times, but each instance the instance name, callsign, must be unique. |

<a name="head.References"></a>
## References

| Ref ID | Description |
| :-------- | :-------- |
| <a name="ref.HTTP">[HTTP](http://www.w3.org/Protocols)</a> | HTTP specification |
| <a name="ref.JSON-RPC">[JSON-RPC](https://www.jsonrpc.org/specification)</a> | JSON-RPC 2.0 specification |
| <a name="ref.JSON">[JSON](http://www.json.org/)</a> | JSON specification |
| <a name="ref.Thunder">[Thunder](https://github.com/WebPlatformForEmbedded/Thunder/blob/master/doc/WPE%20-%20API%20-%20WPEFramework.docx)</a> | Thunder API Reference |



<a name="head.Configuration"></a>
# Configuration

The table below lists configuration options of the plugin.

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| callsign | string | Plugin instance name (default: *org.rdk.Wifi*) |
| classname | string | Class name: *org.rdk.Wifi* |
| locator | string | Library name: *libWPEFrameworkWifiManager.so* |
| autostart | boolean | Determines if the plugin shall be started automatically along with the framework |

<a name="head.Methods"></a>
# Methods

The following methods are provided by the org.rdk.Cable plugin:

WifiManager interface methods:

| Method | Description |
| :-------- | :-------- ||

| [getFrequencyList](#method.getFrequencyList) | Returns the frequency list from cable/sat/T |
| [addFrequency](#method.addFrequency) | add new search frequency |
| [deleteFrequency](#method.deleteFrequency) | delete useless frequency |
| [updateFrequency](#method.updateFrequency) | update frequency by id|
| [getSignalStatus](#method.getSignalStatus) | Returns frequency information like quality and level |
| [getsatelliteList](#method.getsatelliteList) | Returns the array of satellites defined in the database. |
| [addSatellite](#method.addSatellite) | Add a new satellite to the database |
| [createSearch](#method.createSearch) | Returns the searchID used for mutil Tuner |
| [setSearchParam](#method.setSearchParam) | set Search Config |
| [startSearch](#method.startSearch) | start search with all choosed frequency |
| [stopSearch](#method.stopSearch) | stop search |
| [destorySearch](#method.destorySearch) | destory search |


<a name="method.getFrequencyList"></a>
## *getFrequencyList <sup>method</sup>*

Returns the frequency list from cable/sat/T or the data saved by the user

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.type | string/null | C/S/T  default return cable frequencyList |
| params.SatId| string | required when type is S/T |

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.result | array | The result of the frequency list |
| result.result[#].id| string | the frequency id |
| result.result[#].frequencyKhz| string | the frequency (Khz、Mhz、Ghz)|
| result.result[#].symbolRateSps| string | the symbolRate(MS/s、MB/s、Ks/s) |
| result.result[#].modulation| string | the modulation( QAM) |
| result.result[#].polarzation| string | return pol when type is S |
| result.result[#].bandwidth| string | return bandwidth when type is S |
| result.result[#].mode| string | AUTO: FE Type detecting Mode.return when type is T |
| result.result[#].hierarchy| string | hierarchy info. return when type is T |
| result.success | boolean | Whether the request succeeded | 

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 1234567890,
    "method": "org.rdk.Cable.1.getFrequencyList",
    "params":{
      "type":"S",
      "SatId":"d5fdsd6s576"
    }
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 1234567890,
    "result": {
      "result": [
        {
          "id":11111,
          "frequencyKhz" : "417",
          "symbolRateSps" : "5017",
          "polarzation":"ver"
          },
          {
            "id":222222,
            "frequencyKhz" : "417",
            "symbolRateSps" : "5017",
            "modulation" : "16",
            "polarzation":"ver"
          },
        ],
      "success": true
    }
}
```

<a name="method.addFrequency"></a>
## *addFrequency <sup>method</sup>*

Add new frequency to  Frequency list

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.type | string | type to add new frequency cable/sat/T  |
| params.SatId| string | required when type is S|
| params.frequencyKhz | string | The new frequency  ex: range 0~5000 |
| params.symbolRateSps | string | The new symbolRate ex: range 0~5000 |
| params.modulation | string | The new modulation |
| params.polarzation| string |  required when type is S|
| params.bandwidth| string |  required when type is T|
| params.mode| string | required when type is T|
| params.hierarchy| string | required when type is T|


### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.result | integer | The result of the operation (must be one of the following: *0*, *1*) |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 1234567890,
    "method": "org.rdk.Cable.1.addFrequency",
     "params": {
       "type":"S",
       "SatId":"T-800",
       "frequencyKhz": "432",
       "symbolRateSps": "432",
       "modulation": "432",
       "polarzation":"ver"
    }
}
```

#### Response

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "result": {
    "result": 0,
    "id":222222,
    "success": true
  }
}
```

<a name="method.deleteFrequency"></a>
## *deleteFrequency <sup>method</sup>*

Attempts to delete the frequency

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.id | string | The frequency id |


### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "method": "org.rdk.Cable.1.deleteFrequency",
  "params": {
    "id": "4132",
  }
}
```

#### Response

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "result": {
    "success": true
  }
}
```
<a name="method.updateFrequency"></a>
## *updateFrequency <sup>method</sup>*

when user change frequency infomation

### Parameters
| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.id | string | The change frequency id |
| params.frequencyKhz | string | The new frequency |
| params.symbolRateSps | string | The new symbolRate |
| params.modulation | string | The new modulation |
| params.polarzation| string | required when type is S |
| params.bandwidth| string |  required when type is T|
| params.mode| string | required when type is T|
| params.hierarchy| string | required when type is T|


### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "method": "org.rdk.Cable.1.updateFrequency",
  "params":{
    "id":11223,
    "frequencyKhz":"421",
    "symbolRateSps":"5668",
    "modulation":"128",
    "polarzation":"LEFT"
  }
}
```

#### Response

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "result": {
    "success": true
  }
}
```

<a name="method.getSignalStatus"></a>
## *getSignalStatus <sup>method</sup>*

get signaStrength / signalQuality in dB/dBuV or percentag

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.TunerID | number | TunerID (0,1,2,3...)|

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.result | object | The result of the SignalStatus |
| result.result.LockeState | boolean | |
| result.result.signalQuality | number | Signal quality, i.e. SNR, signal-to-noise ratio, in dB.  |
| result.result.signaStrength | number | Signal strength, in dBuV. |
| result.result.SignalStrengthPercentage | number | Signal strength, in percentag. |
| result.result.SignalQualityPercentage | number | Signal quality, i.e. SNR, signal-to-noise ratio, in percentag. |
| result.result.nBER | number |  |
| result.result.nBERPercentage | number | |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "method": "org.rdk.Cable.1.getSignalStatus",
  "params":{
    "TunerID":"156465"
  }
}
```

#### Response

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "result": {
    "result": {
      "LockeState":true,
      "signalStrength":80,
      "signalQuality":55,
      "nBER":1216
    },
  "success": true
  }
}
```
<a name="method.getsatelliteList"></a>
## *getsatelliteList <sup>property</sup>*

Provides access to the returns the array of satellites defined in the database.

> This property is **read-only**.

### Value

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | array | Returns the array of satellites defined in the database |
| result[#] | object |  |
| result[#].name | string |  |
| result[#].longitude | number | Longitudinal location of the satellite in 1/10ths of a degree, with an east coordinate given as a positive value and a west coordinate as negative. Astra 28.2E would be defined as 282 and Eutelsat 5.0W would be -50 |
| result[#].lnb | string | Name of the LNB settings to be used when tuning to this satellite |

### Example

#### Get Request

```json
{
    "jsonrpc": "2.0",
    "id": 1234567890,
    "method": "org.rdk.Cable.1.getsatelliteList"
}
```

#### Get Response

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "result": [
    {
      "name": "Astra 28.2E",
      "longitude": 282,
      "lnb": "Universal"
    }
  ]
}
```
<a name="method.addSatellite"></a>
## *addSatellite <sup>method</sup>*

Add a new satellite.

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.name | string |  |
| params.longitude | number | Longitudinal location of the satellite in 1/10ths of a degree, with an east coordinate given as a positive value and a west coordinate as negative. Astra 28.2E would be defined as 282 and Eutelsat 5.0W would be -50 |
| params.lnb | string | Name of the LNB settings to be used when tuning to this satellite |

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | boolean | true if the satellite is added, false otherwise |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 1234567890,
    "method": "org.rdk.Cable.1.addSatellite",
    "params": {
      "name": "Astra 28.2E",
      "longitude": 282,
      "lnb": "Universal"
    }
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 1234567890,
    "result": true
}
```

<a name="method.GetSatInfo"></a>
## *GetSatInfo <sup>method</sup>*

get GetSatInfo

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.SatId | number | |

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.result | object | The result of the SignalStatus |
| result.result.LnbIndex | boolean |卫星参数配置 |
| result.result.NetType | string | < Net type, S/T */ |
| result.result.SatelliteDegree | number | 0~3600. |
| result.result.MotorPosition | number | Motor Position. 0、1、2.... |
| result.result.MotorType | number | 0- NONE / 1-1.2 /2-1.3 Motor Type. |
| result.result.DiSEqCType | string | DiSEqC Type 0- NONE / 1-toneburst  |
| result.result.DiSEqCPort | number | |
| result.result.SwitchPower | number |switch power. 0-off 1-on |
| result.result.SwitchVoltage | number | switch voltage. 0-off 1-13v/2-14v/3-18v/4-19v |
| result.result.Switch22K | number | 22KHZ Switch 0-Disable，1-Enable. |
| result.result.stTunerConnect | number | |
| result.result.TunerIndex | number | || result.result.DiSEqCPort | number | |
| result.result.szNetName[BLL_DM_MAX_NETNAME_LEN + 1] | number | Net name|
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "method": "org.rdk.Cable.1.getSignalStatus",
  "params":{
    "SatId":"156465"
  }
}
```

#### Response

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "result": {
    "result": {
      "LnbIndex":true,
      "NetType":"S",
      "SatelliteDegree":55,
      "MotorPosition":5,
      "MotorType":1,
      "DiSEqCType":1,
      "DiSEqCPort":0,
      "SwitchPower":1,
      "SwitchVoltage":1,
      "Switch22K":0,
      "stTunerConnect":10,
      "TunerIndex":55,
      "szNetName":1216
    },
  "success": true
  }
}
```


<a name="method.createSearch"></a>
## *createSearch <sup>method</sup>*

Returns the searchID used for mutil Tuner

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.type| string | S/C/T  |



### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.searchID | string |   |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "method": "org.rdk.Cable.1.createSearch",
  "params":{
    "type":"C"
  }
}
```

#### Response

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "result": {
    "searchID":"156165",
    "success": true
  }
}
```

<a name="method.setSearchParam"></a>
## *setSearchParam <sup>method</sup>*

set some search config

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.searchID | string |  |
| params.searchConfig | object |  |
| params.searchConfig.searchMode | string | //Nit/manual/Auto |
| params.searchConfig.serviceType | string | //TV/Radio/All |
| params.searchConfig.scrambleMode | string | //Free/Scramble/All |
| params.searchConfig.satelliteDegree | number | 0~3600 |
| params.searchConfig.motorPosition | string | Motor Position. 0、1、2.... |
| params.searchConfig.motorType | string | 0- NONE / 1-1.2 /2-1.3 Motor Type. |
| params.searchConfig.LNB | string |  |
| params.searchConfig.DiSEqCType | number | DiSEqC Type 0- NONE / 1-toneburst / 2-1.0 / 3-1.1. |
| params.searchConfig.DiSEqCPort | number |  DiSEqC Port.1,2,3,4.. |
| params.searchConfig.SwitchPower | number |  switch voltage. 0-off 1-13v/2-14v/3-18v/4-19v*/ |
| params.searchConfig.22K | number | 22KHZ Switch 0-Disable，1-Enable. |
| params.searchConfig.TunerConnect | string  |
| params.searchConfig.TunerIndex | string |  |
| params.searchConfig.NetName | string |  |


### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "method": "org.rdk.Cable.1.setSearchParam",
  "params":{
    "searchID":"4654546",
    "searchConfig":{
      "LNB":"12316",
      "DiSEqCType":1,
      "DiSEqCPort":1,
      "22K":0,
      "nit":0,
      "serviceType":"all",
      ...
    }
  }
}
```

#### Response

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "result": {
    "success": true
  }
}
```

<a name="method.startSearch"></a>
## *startSearch <sup>method</sup>*

search all choosed frequency 

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | array |  |
| params[#] | object |  |
| result.params[#].id | string | frequency id |
| result.params[#].frequencyKhz | string | |
| result.params[#].symbolRateSps | string |  |
| result.params[#].modulation | string |  |

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.result | object |  |


### Example

#### Request

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "method": "org.rdk.Cable.1.startSearch ",
  "params":[
    {
      "id":11223,
      "frequencyKhz":"421",
      "symbolRateSps":"5668",
      "modulation":"128"
    },
    {
      "id":11223,
      "frequencyKhz":"421",
      "symbolRateSps":"5668",
      "modulation":"128"
    }
  ]
}
```

#### Response

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "result": {
    "success": true
  }
}
```

<a name="method.stopSearch"></a>
## *stopSearch <sup>method</sup>*

stopsearch

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.searchID | string | searchID |

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.success | boolean | Whether the request succeeded |

#### Request

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "method": "org.rdk.Cable.1.stopSearch ",
  "params":{
    "searchID":"15646"
  }
}
```

#### Response

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "result": {
    "success": true
  }
}
```

<a name="method.destorySearch"></a>
## *destorySearch <sup>method</sup>*

destorySearch

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.searchID | string | searchID |

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.success | boolean | Whether the request succeeded |

#### Request

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "method": "org.rdk.Cable.1.destorySearch ",
  "params":{
    "searchID":"15646"
  }
}
```

#### Response

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "result": {
    "success": true
  }
}
```

<a name="head.Notifications"></a>
# Notifications

Notifications are autonomous events, triggered by the internals of the implementation, and broadcasted via JSON-RPC to all registered observers. Refer to [[Thunder](#ref.Thunder)] for information on how to register for a notification.

The following events are provided by the org.rdk.Cable plugin:

| Event | Description |
| :-------- | :-------- |
| [onSearchStateChanged](#event.onSearchStateChanged) | Triggered when finish signle frenquency search |


<a name="event.onSearchStateChanged"></a>
## *onSearchStateChanged <sup>event</sup>*

Triggered when finish signle frenquency search

### Parameters

### Example

```json
{
  "jsonrpc": "2.0",
  "method": "client.events.1.onSearchStateChanged",
}
```

#### Response

```json
{
  "jsonrpc": "2.0",
  "id": 1234567890,
  "result": {
    "result":{
      "id":"5424",
      "name":"cctv1",
      "video_pid":"8191",
      "audio_pid":"8191",
      "frequencyKhz":"10992",
      "symbolRateSps":"27500",
      "service_id":"8557",
      "PCR_pid":"8191",
      "subTitle_pid":"0"
    },
    "success": true
  }
}
```


  
