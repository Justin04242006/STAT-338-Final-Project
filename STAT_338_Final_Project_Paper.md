## Justin Peabody

## Project title:

### I. Background Information and Problem Statement

(A description of how air pollution is a big concern in urban areas,
what particulate matter (and pm2.5) is, and the adverse effects of pm2.5
on public health

(The questions you wish to answer, via inference and prediction,
pertaining to particulate matter concentrations in Chicago

Air quality is a major public health concern, particularly in urban
areas, due to its many adverse health effects encompassing a wide
variety of respiratory and cardiovascular illnesses (1). Urban areas
contain some of the largest sources of anthropogenic air pollution,
including industrial facilities, power plants, traffic exhaust
emissions, and landfills and other waste management facilities. Of
especially great concern for public health is a class of air pollutant
particles known as particulate matter 2.5 (PM2.5), which include solid,
liquid, and gaseous pollutant particles less than 2.5 micrometers in
diameter. The small diameter of such particles enables easier
infiltration into the airways and bodily tissues and more acute health
effects.

As the prevalence of automobiles drastically increased throughout the
early and middle 1900s, car exhaust emissions contributed to increasing
levels of particulate matter in the form of ground level ozone, which
resulted in concerning levels of smog (2). Federal air quality
monitoring sensors, manufactured by organizations such as the
Environmental Protection Agency (EPA), began to provide highly accurate
measurements of particulate matter during the 1970s, acting as the
United States’ core tool for measuring compliance with early pieces of
air pollution reduction legislation aimed at regulating this increase in
pollution.

While federal grade air quality sensors remain an essential monitoring
equipment today, their high accuracy comes with high purchasing and
operational costs. Because of this, such sensors exist sparsely in most
urban areas, with only a few per city. The measurements from federal
sensors mask hyperlocal variations in particulate matter between urban
neighborhoods, especially those with marginalized and less affluent
populations. This is where low-cost, hyperlocal sensors, such as the
sensors sold worldwide by the PurpleAir, AirGradient, and Clarity
companies, possess a crucial advantage. Due to their lower cost, tighter
networks of several dozen sensors can be installed in a city, supporting
more detailed analysis of the spatial variability of air pollution than
is possible with federal sensors alone.

To provide air quality monitoring data to marginalized communities in
Chicago, Loyola University’s Community Local Engaged Air Research
(CLEAR) lab partners with city organizations to install low cost PM2.5
sensors. These sensors support cloud based data uploading and retrieval,
which has allowed for the creation of an air quality SQL database shared
by the CLEAR lab via downloads from the PurpleAir company API (3). After
completing an Undergraduate Summer Research Experience project orienting
me with this database, I joined the lab as a Database Manager in
September 2026. I have worked to increase the number of sensors
containing historical data in the database and have expanded the
database to include sensors from Clarity and AirGradient in addition to
PurpleAir.

Most of my work as Database Manager has focused on the development of
the database schema and producing workflows to streamline updates to the
historical data and metadata contained therein. I realized that I had
not done any heavy modeling with the data in the database, and this
project seemed an apt opportunity to apply statistical learning methods
to messy, real world environmental data. My project aims to develop a
model that best predicts changes in 2025 particulate matter
concentrations as a function of changes in humidity, temperature,
pressure, wind speed and direction, distances from nearby pollution
sources, and the amount of PM2.5 emitted by these sources in 2025. Such
changes in meteorological variables were aggregated and calculated on
both hourly and daily intervals.

### II. Data description

Purpleair Sensor Data:

As aforementioned, the CLEAR lab database contains historical data and
metadata for sensors from three companies: PurpleAir, Clarity, and
AirGradient. For this project, I focus on PurpleAir data since
observations exist from the entire year of 2025. Clarity historical
readings date back to July 2025, while Airgradient historical readings
date back to April 2025. Obtaining an entire calendar year of data
smooths out seasonal discrepancies in meteorologcial variables.

The Purpleair historical data table, called Purpleair\_air\_history,
contains the following variables (Every row in this table corresponds to
a measurement reading):

- sensor\_index: a unique ID number assigned to each sensor

- time\_stamp: the time, down to the second, when the measurement
  reading was uploaded by the sensor to the cloud. Purpleair historical
  readings are taken once every second and averaged over 2 minute
  intervals. It is the 2 minute averages that are uploaded to the cloud.

- humidity: the relative humidity (as a percentage) inside the sensor
  unit. This is NOT the same as the relative humidity of the ambient
  air. Due to the heat generated by the electronic components inside the
  sensor, relative humidity measurements tend to be underestimates of
  ambient relative humidity. For this reason, the PurpleAir company has
  developed correction formulas to make relative humidity readings a
  closer approximation of ambient relative humidity and the readings of
  federal grade sensors (see Methodology section for more details).

- temperature: the temperature (in degrees Fahrenheit) inside the sensor
  unit. The heat generated by the electronic components inside the
  sensor causes temperature readings to be overestimates of ambient
  temperature. Additional correction formulas exist to address this
  upward bias (see Methodology section).

- pressure: the atmospheric pressure (in millibars).

- pm2p5\_cf\_1\_a/pm2p5\_cf\_1\_b: the particulate matter 2.5
  concentration of Channel A and Channel B inside the sensor,
  respectively. Each Purpleair sensor has two internal channels: Channel
  A and Channel B. Within each channel, PM2.5 concentrations are
  estimated using optical sensing, in which a laser beam inside the
  channel illuminates each particle, causing it to scatter visible light
  at various frequencies. The scattered light contacts a photodiode
  within the channel, which estimates the particle size and
  concentration based on the wavelength ranges of the scattered light.

The Purpleair sensor metadata table, called
Purpleair\_sensor\_information, contains the following variables:

- sensor\_index: the same sensor\_index field in Purpleair\_air\_history

- date\_created: the date of installation of the sensor

- last\_seen: the time stamp of the latest historical measurement upload
  by the sensor

- name: A descriptive name given to each sensor, which usually includes
  the street and/or neighborhood it is located in

- location\_type: a binary variable taking on the value of 0 if the
  sensor is located outdoors and 1 if it is indoors

- latitude/longitude: the latitude/longitude coordinates of the sensor’s
  location

- additional variables pertaining to the model, hardware, and
  availability status of sensor data to the general public

As explained in the Methodology section, the sensor\_index, latitude,
and longitude variables are most relevant to my project.

The first dataset I obtained for my project was a data frame of all the
2025 historical readings for PurpleAir sensors from the CLEAR lab
database. I did so via RMySQL, a R based wrapper for SQL code that
allows users to query information, in the form of data frames, from
tables within the database. This raw dataframe contained 19,978,035
observations from 116 sensors throughout Chicago.

I then curated a dataset of documented Chicago particulate matter
sources from the Climate Trace website (4). This dataset contains the
name of each facility emitting particulate matter, the latitude and
longitude of each facility (obtained via Google Maps), and the amount of
particulate matter (in tons) emitted by the facility in 2025. 53
observations, representing 53 facilities, are in this dataset.

The third dataset I needed was the metadata for Purpleair sensors, which
was also obtained via querying the database. This dataset contained 116
observations (1 for each sensor).

### III. Methodology

### IV. Results

### V. Conclusion and Further Research

### VI. Works cited

1.  <https://www.epa.gov/air-research/healthy-heart-toolkit-and-research>

2.  <https://www.clarity.io/blog/the-history-of-air-quality-monitoring-technology-how-has-air-quality-measurement-evolved-over-the-years>

3.  <https://api.purpleair.com>

4.  

### VII. Appendix

## Justin Peabody

## Project title: ADD TITLE HERE

### ADD SUBMISSION DATE HERE
