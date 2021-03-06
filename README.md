# GMIT Data Representation and Querying Project 2015-2


## Introduction
This project provides the design and documentation for the dataset "National Roads Weather Station Data" which is available at [https://data.gov.ie/dataset/national-roads-weather-station-data](https://data.gov.ie/dataset/national-roads-weather-station-data).

## About the data
This dataset is provided in Extensible Markup Language (XML) format, and was downloaded from [this link](http://data.tii.ie/Datasets/Its/DatexII/WeatherData/Content.xml).
The XML file contains rows "siteMeasurements" with the items:
    <br/>- **measurementSiteReference**: where exactly on the road the measurement was taken.
    <br/>- **measurementTimeDefault**: when exactly the measurement was taken.
  <br/>And contains indexed "measuredValues".
  <br/>Each **measuredValue** has:
    <br/>- **index**: starts by 1 and is incremented as the siteMeasurements has more items.
  <br/>And a measuredValue has a **period** and more variables depending on which one of these types it is: 
    <ul>
        <li>**TemperatureInformation**
          <ul>
            <li>**temperature**
                <ul>
                  <li>airTemperature</li>
                  <li>dewPointTemperature</li>
                </ul>  
            </li>
          </ul>
         </li>
        <li>**PrecipitationInformation**
            <ul>
                <li>precipitationDetail</li>
            </ul>
        </li>    
        <li>**WindInformation**
            <ul>
                <li>**wind**
                    <ul>
                        <li>maximumWindSpeed</li>
                        <li>windDirectionBearing</li>
                        <li>windDirectionCompass</li>
                        <li>windSpeed</li>
                    </ul>
                </li>
            </ul>
        </li>
        <li>**RoadSurfaceConditionInformation**
            <ul>
                <li>**roadSurfaceConditionMeasurements**
                    <ul>
                        <li>protectionTemperature</li>
                        <li>roadSurfaceTemperature</li>
                     </ul>
                </li>
            </ul>
        </li>
    </ul>
    
    A example in XML may be looked below:
```xml
    <siteMeasurements>
        <measurementSiteReference>NRA1681</measurementSiteReference>
            <measurementTimeDefault>2015-11-12T19:10:00+00:00</measurementTimeDefault>
            <measuredValue index="1">
            <basicDataValue xsi:type="TemperatureInformation">
                <period>3600</period>
                <temperature>
                    <airTemperature>7.9</airTemperature>
                    <dewPointTemperature>4.2</dewPointTemperature>
                </temperature>
            </basicDataValue>
        </measuredValue>
        <measuredValue index="2">
            <basicDataValue xsi:type="PrecipitationInformation">
                <period>3600</period>
                <precipitationDetail></precipitationDetail>
            </basicDataValue>
        </measuredValue>
        <measuredValue index="3"></measuredValue>
        <measuredValue index="4"></measuredValue>
    </siteMeasurements>
 ```
 And in JSON format:
 ```json
 {
    "siteMeasurements": {
        "measurementSiteReference": "NRA1681",
        "measurementTimeDefault": "2015-11-12T19:10:00+00:00",
        "measuredValue": [
            {
                "_index": "1",
                "xsi:type" : "TemperatureInformation",
                "value":{
                    "period": "3600",
                    "temperature": {
                        "airTemperature": "7.9",
                        "dewPointTemperature": "4.2"
                    }    
                }
                
            },
            {
                "_index": "2",
                "xsi:type" : "PrecipitationInformation",
                "value":{
                    
                    "period": "3600",
                    "precipitationDetail": ""
                }
                
            },
            {
                "_index": "3"
            },
            {
                "_index": "4"
            }
        ]
    }
}
```
## URLs
This API provides a few URLs to get Roads Weather. For example, a GET request with the following URL

http://api.irishroadsweather.com/measurements/

Will return a list of all the measurements (siteMeasurements) present on the dataset.

```json
 {
    "siteMeasurements": {
        "measurementSiteReference": "NRA1682",
        "measurementTimeDefault": "2015-11-12T19:10:00+00:00",
        "measuredValue": [
            ...
        ]
    },
    "siteMeasurements": {
        "measurementSiteReference": "NRA1681",
        "measurementTimeDefault": "2015-11-13T10:40:00+00:00",
        "measuredValue": [
            ...
        ]
    },
    ...
}
```

### Filters
Obviously, you may  want request not all the measurements but only determined ones.
In this case, use a parameterized URL, as below:

http://api.irishroadsweather.com/measurements?filterby=[argname]&value=[value]

And the possible values for [argname]

| Argument | Type |
|------|-----|
measurementSiteReference | String |
measurementTimeDefault | Formated [YYYY-MM-DD]T[HH:MM:SS]+[00:00] |
TemperatureInformationPeriod | Integer |
PrecipitationInformationPeriod | Integer |
WindInformationPeriod | Integer |
RoadSurfaceConditionPeriod | Integer |
airTemperature | Decimal |
dewPointTemperature | Decimal |
precipitationDetail | String |
maximumWindSpeed | Decimal |
windDirectionBearing | Integer |
windDirectionCompass | Integer |
windSpeed | Decimal |
protectionTemperature | Decimal |
roadSurfaceTemperature | Decimal |

### Calculated requests
These will be probably useful to get specific and, might, frequent rows:

Get the row with a maximum value for a arg:
<br/>http://api.irishroadsweather.com/measurements/max/[arg]

Get the row with a minimum value for a arg:
<br/>http://api.irishroadsweather.com/measurements/min/[arg]

Get the row with a average value for a arg:
<br/>http://api.irishroadsweather.com/measurements/avg/[arg]

Get all the rows where the the value for a [arg] is smaller than [value]
<br/>http://api.irishroadsweather.com/measurements/upto/[arg]/[value]

Get all the rows where the the value for a [arg] is larger than [value]
<br/>http://api.irishroadsweather.com/measurements/from/[arg]/[value]

Order the rows by criteria ([arg] and [descrescent/crescent] 
<br/>http://api.irishroadsweather.com/measurements/orderby/[arg]/[desc:cres]

Limit the result to the first [nrows] 
<br/>http://api.irishroadsweather.com/measurements/top/[nrows]

##Going further
This set of URLs GET requests may look limited at a first glance. However, try combining two or more of those above. It can provide a significant amount of possibilities to select proper information from the dataset.

Giving a example for that:
<br/>http://api.irishroadsweather.com/measurements/from/maximumWindSpeed/30.5/orderby/maximumWindSpeed/desc

Your response will bring a list of site measurements where the maximum wind speed measured was 30.5 km/h, ordering those rows by the maximum wind speed from the larger to the smaller. 









 
