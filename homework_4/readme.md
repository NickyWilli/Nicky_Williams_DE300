## Homework 4: Apache Airflow ReadMe

# DAGs
1. weather_data_2hrs.py: collects current observations from a set of weather stations every 2 hrs (0 */2 * * *) and uploads them to the S3 bucket. 
Key Features:
Targets stations: KORD, KENW, KMDW, KPNT
Extracts fields like temperature, humidity, wind speed, visibility, etc.
Expected output: stores CSV files in S3 under the prefix weather_data/
Each CSV file contains a table of weather observations (cols including time of collection, time stamp, station, etc.) where each row represents a station’s weather at a time of collection 
2. weather_lin_reg.py: trains a linear regression model on collected weather data and forecasts temperature for the next 8 hrs (in 30-minute steps) per station. DAG is scheduled hourly (0 * * * *) with built-in skipping if required conditions are not met.
Key Features:
Triggers only when data spans close to 20 or 40 hours
Features include humidity, dew point, wind speed, hour, station, etc.
Expected output: Outputs temperature predictions CSV to S3 under predictions/
Each row represents a forecast for a given station at a future timestamp. There should be 16 rows per station, one for every 30-min step over the next 8 hrs.  
3. daily_weather.py: Generates and uploads daily visualizations (PNGs) of weather metrics. Scheduled daily. 
Key Features:
Aggregates and plots data from the last 24 hours
Metrics plotted: temperature, visibility, and relativeHumidity
Expected output: PNG image files to S3 under output_graphs/
Each PNG illustrates a time-series plot of the trend of one weather metric over the past 24 hrs (time vs metric value, one line per station.)
TO RUN THE CODE:
AWS S3 Setup
Make sure the following S3 paths are available in AWS account:
Bucket: natarajan-williams-silverman-bucket


weather_data/: For storing raw observations
predictions/: For temperature forecasts
output_graphs/: For dashboard images


Ensure the Airflow environment has appropriate AWS credentials and permissions.
Needed to run
Apache Airflow
Python 3.7+
Packages: pandas, numpy, requests, boto3, matplotlib, scikit-learn, pendulum (provided in the code)
Make sure your Airflow environment includes all dependencies via the requirements.txt


GenAI Disclosure: No AI was used for this assignment (but various help from TAs was!)
