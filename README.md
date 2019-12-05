# PRTG_XML_udf - AutoIt3 UDF for PRTG

## Introduction

A set of user defined functions to ease the process of outputting XML return values for your PRTG [EXE/Script Advanced](https://www.paessler.com/manuals/prtg/exe_script_advanced_sensor) sensors.

Some of the functions:
* `_PrtgChannel()`      - print a channel
* `_PrtgPrintTag()`     - print specific XML tag
* `_PrtgComment()`      - print an XML comment
* `_PrtgReturnError()`  - set the sensor to error mode, and print related error message
* `_SecsToTime()`       - return human-readable time (i.e. for status text)

The XML prolog and PRTG root elements can be omitted by setting `Global $_CHAONLY = True`, allowing the program to be used in i.e. batch scripts together with multiple custom sensors.

### Usage example:
```
#include "PRTG_XML_udf.au3"
_PrtgShowXML()
_PrtgChannel("Barometer", 1014.3, "hPa", $PRTG_FLOAT_YES)
_PrtgChannel("Thermo", 25.3, Default, $PRTG_CS_TEMP)
_PrtgChannel("Hygro", 67, Default, $PRTG_UNIT_PERCENT+$PRTG_FLOAT_YES+$PRTG_DECIMALMODE_AUTO+$PRTG_SHOWCHART_NO+$PRTG_SHOWTABLE_NO)
_PrtgPrintTag("Text", "Air quality OK")
_PrtgComment("No errors found")
_PrtgShowXML()
```

### Output example:
```
<?xml version="1.0" encoding="Windows-1252" ?>
<prtg>

    <result>
    <Channel>Barometer</Channel>
    <Value>1014.3</Value>
    <Unit>Custom</Unit>
    <CustomUnit>hPa</CustomUnit>
    <Float>1</Float>
    </result>
    <result>
    <Channel>Thermo</Channel>
    <Value>25.3</Value>
    <Unit>Temperature</Unit>
    <Float>1</Float>
    <DecimalMode>All</DecimalMode>
    </result>
    <result>
    <Channel>Hygro</Channel>
    <Value>67</Value>
    <Unit>Percent</Unit>
    <Float>1</Float>
    <DecimalMode>Auto</DecimalMode>
    <ShowChart>0</ShowChart>
    <ShowTable>0</ShowTable>
    </result>
    <Text>Air quality OK</Text>
    <!--No errors found-->

</prtg>
```

#### References:
* https://www.paessler.com/manuals/prtg/custom_sensors
