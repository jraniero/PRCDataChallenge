# PRC Data Challenge 2024

This repository contains the code of [team_versatile_yacht](https://ansperformance.eu/study/data-challenge/teams.html#team_versatile_yacht) used for the [PRC Data Challenge 2024](https://ansperformance.eu/study/data-challenge/)

## The Team
The team is composed of aeronautical engineers and data scientist

## The approach
### Feature engineering
We have built different features from the data provided
- Trajectory based features
  - First stable fl after take-off
  - Average climb rate till that stable fl
  - Average ground speed
  - Wind speed and direction
  - Airspeed and direction
- non-trajectory based features
  - aircraft type
  - ADEP/ADES
  - Distance flown
  - Hour of the day
  - Day of the year

We build features to take into account non-linearities in the relationship between TOW and features, for instance:
- Square of speed
- Square root of speed
- sine and cosine of hour of the day: This allows having continuous variables representing the time
- sine and cosine of day of the year: This allows having continuous variables representing the day
- sine and cosine of track and windspeed angle

 
### Model testing
We have tested different models:
- Linear Regression
- KNN
- ANN
- RF
- Gradient Boost
It comes out that the best performance is achieved with a random forest, this is the one retained.
 
## Usage
### Configuration
Configuration is based on env variables:
- SOURCE_FOLDER: folder with the .parquet and .csv files provided by the PRC Challenge
- DESTINATION_FOLDER: folder where the temporary data has to be stored
- CHALLENGE_FILE: Name of the PRC Challenge file with the challenge set
- CHALLENGE_FILE_PREPROC: Name of the temporary file used for adding features to the challenge set
- SUBMISSION_FILE:  Name of the PRC Challenge file with the submission set
- SUBMISSION_FILE_PREPROC: Name of the temporary file used for adding features to the submission set
- AIRCRAFT_DB: Name of csv file with aircraft performance data (provided)
- TRAJECTORY_DATA: Name of csv file with post-processing of trajectory (generated by trajectory_processing_00.py)
- UTC_OFFSET: File with local UTC offset
### Execution
1. Run the trajectory_processing_00.py file: This can take significant time as it will cycle through the .parquet files
2. Run the add_features.ipynb notebook: This will increment the challenge and submission set with additional features
3. Run the rf_model.ipynb notebook: This will test a Random Forest Model and generate the TOW for the submission set
   
# References
|Topic|Methodology/comments|Lien source|
|----|-------|-----|
|Aircraft performance|eurocontrol data|https://contentzone.eurocontrol.int/aircraftperformance/default.aspx?|
|aircraft OEW|own assessment with Airline and  manufacturer information in typical configuration|airbus.com|
|||boeing.com|
|||https://fr.wikipedia.org/wiki/Bombardier_Canadair_Regional_Jet|
|||https://www.atr-aircraft.com/aircraft-services/aircraft-family/atr-42-600/|
|||https://embraer.com/|
||cabin configuration|https://www.seatguru.com/|
|||airlines website|
|RECAT EU|To determine our own heavy medium and light model.|https://www.eurocontrol.int/archive_download/all/node/9681|
|||https://www.easa.europa.eu/en/downloads/117238/en|
||Taxi-in time|Eurocontrol stat|||
|Airport data and runway ||https://ourairports.com/data/|
|flight stats||https://www.eurocontrol.int/sites/default/files/2022-12/eurocontrol-comprehensive-air-traffic-assessment-20221208-2022-overview.pdf|
|||https://www.eurocontrol.int/sites/default/files/2024-04/eurocontrol-european-aviation-overview-20240403.pdf|
|"taxi-in out fuel burn|""Estimation of Aircraft Taxi-out Fuel Burn using"|
|"Flight Data Recorder Archives""|https://web.mit.edu/hamsa/www/pubs/KhadilkarBalakrishnanGNC2011.pdf"|
|taxi times||https://www.eurocontrol.int/publication/taxi-times-summer-2023|
