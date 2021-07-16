<!-- Generated automatically, DO NOT EDIT! -->
<a name="head.Channel_Plugin"></a>
# Cable

**Version: 1.0**

**Status: :black_circle::black_circle::black_circle:**

<!--org.rdk.Cable plugin for Thunder framework.-->

### Table of Contents

- [Introduction](#head.Introduction)
- [Description](#head.Description)
- [Configuration](#head.Configuration)
- [Methods](#head.Methods)
- [Notifications](#head.Notifications)

<a name="head.Introduction"></a>
# Introduction

<a name="head.Scope"></a>
## Scope

This document describes purpose and functionality of the org.rdk.channel plugin. It includes detailed specification about its configuration, methods provided and notifications sent.

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

<a name="head.Description"></a>
# Description

The `Wifi` plugin is used to manage Wifi network connections on a set-top device.

The plugin is designed to be loaded and executed within the Thunder framework. For more information about the framework refer to [[Thunder](#ref.Thunder)].

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

The following methods are provided by the org.rdk.Wifi plugin:

WifiManager interface methods:

| Method | Description |
| :-------- | :-------- |
| [getCableFrequencyList](#method.getChannelFrequencyList) | Returns the Cable handlemode search setting list |
| [addNewFrequency](#method.addNewFrequency) | add new search frequency |
| [deleteFrequency](#method.deleteFrequency) | delete useless frequency |
| [getFrequencyInfo](#method.getFrequencyInfo) | Returns frequency information like quality and level |
| [updateFrequency](#method.updateFrequency) | Returns the current Wifi state |
| [searchCable](#method.searchCable) | Returns the show which at the all frenquency point |


<a name="method.getCableFrequencyList"></a>
## *getCableFrequencyList <sup>method</sup>*

get cable frequency list that returns the default data or the data saved by the user

### Parameters

This method takes no parameters.

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.result | array | The result of the frequency list |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 1234567890,
    "method": "org.rdk.Cable.1.getCableFrequencyList"
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
                "id":11111
                "frequency":"417",
                "symbolRate":"5017",
                "QAM":"16"
            }
        ],
        "success": true
    }
}
```

<a name="method.addNewFrequency"></a>
## *addNewFrequency <sup>method</sup>*

Add new frequency to cable Frequency list

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.frequency | string | The new frequency |
| params.symbolRate | string | The new symbolRate |


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
    "method": "org.rdk.Cable.1.addNewFrequency"
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 1234567890,
    "result": {
        "result": 0,
        "id":222222
        "success": true
    }
}
```

<a name="method.deleteFrequency"></a>
## *deleteFrequency <sup>method</sup>*

Attempts to delete the frequency from cable list

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
        "id": "123412341234",
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

<a name="method.getFrequencyInfo"></a>
## *getFrequencyInfo <sup>method</sup>*

get frequency infomation

### Parameters
| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.id | string | The frequency id |

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.result | object | The result of the frequency |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 1234567890,
    "method": "org.rdk.Cable.1.getFrequencyInfo"
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 1234567890,
    "result": {
        "result": {
            "id":11111
                "frequency":"417",
                "symbolRate":"5017",
                "QAM":"16"
        },
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
| params.frequency | string | The new frequency |
| params.symbolRate | string | The new symbolRate |
| params.QAM | string | The new QAM |

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
    "method": "org.rdk.Cable.1.updateFrequency"
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

<a name="method.searchCable"></a>
## *searchCable <sup>method</sup>*

Returns the cable List.  


### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | array |  |
| params[0] | object |  |
| params[0].frequency | string |  |
| params[0].symbolrate | string |  |
| params[0].qam | string |  |


### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | array |  |
| result.result | array |  |
|result.result[0]|object|
|result.result[0].id | string | show id |
|result.result[0].name | string | show name |
|result.result[0].level | string | signal level |
|result.result[0].strength | string | signal strength |
|result.result[0].logo | string | show logo |
|result.result[0].source | string | signal source |


### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 1234567890,
    "method": "org.rdk.Cable.1.searchCable "
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 1234567890,
    "result": {
        "result":[
            {
               "id":'5424',
               "logo":'http://jdkfhl',
               "level":39,
               "strength":68,
               "source":"signal 1",
               "name":"cctv1"
            }
        ]
        "success": true
    }
}
```


