# kestra-workflow
Please refer Ketra  workflow file [nyc-taxi-trip-data-flow.yaml](https://github.com/harshaspace/kestra-workflow/blob/main/nyc-taxi-trip-data-flow.yaml) which ingest data to GCP BigQuery data set.

#### Use `Backfill` feature to trigger pass dates

<img width="300" height="220" alt="image" src="https://github.com/user-attachments/assets/43077cc1-e591-4d96-9ce7-d05e7c5ecf4f" />


1. Within the execution for Yellow Taxi data for the year 2020 and month 12: what is the uncompressed file size (i.e. the output file yellow_tripdata_2020-12.csv of the extract task)?

-  134.5 MB	

2. What is the rendered value of the variable file when the inputs taxi is set to green, year is set to 2020, and month is set to 04 during execution?

green_tripdata_2020-04.csv

<img width="300" height="220" alt="image" src="https://github.com/user-attachments/assets/a448c207-49d9-41c4-8445-b82de4cc5950" />

3. How many rows are there for the Yellow Taxi data for all CSV files in the year 2020?
  - 24648499

   """
   SELECT 
  SUM(row_count) as total_trips_2020
FROM `curious-helix-484819-a6.taxi_dataset.__TABLES__`
WHERE table_id LIKE 'yellow_tripdata_2020_%'
  AND table_id NOT LIKE '%_ext'
  AND type = 1;
  
  """

4. How many rows are there for the Green Taxi data for all CSV files in the year 2020?

-  1734051

   """
      SELECT 
  SUM(row_count) as total_trips_2020
FROM `curious-helix-484819-a6.taxi_dataset.__TABLES__`
WHERE table_id LIKE 'green_tripdata_2020_%'
  AND table_id NOT LIKE '%_ext'
  AND type = 1;
   """
