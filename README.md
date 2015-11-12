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
    <li>**TemperatureInformation**</li>
      <ul>
        <li>**temperature**</li >
        <ul>
          <li>airTemperature</li>
          <li>dewPointTemperature</li>
        </ul>  
      </ul>
    </ul> 
  </ul>
  <p>
  <ul>
    <li>**PrecipitationInformation**</li>
  </ul>
  <p>
  <ul>
    <li>**WindInformation**</li>
  </ul>
  <p>
  <ul>
    <li>**RoadSurfaceConditionInformation**</li>
  </ul>
  
  
  
