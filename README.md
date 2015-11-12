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
```
  
