# kestra-workflow

Please refer to the Kestra workflow file [nyc-taxi-trip-data-flow.yaml](https://github.com/harshaspace/kestra-workflow/blob/main/nyc-taxi-trip-data-flow.yaml), which ingests taxi data into a Google Cloud BigQuery dataset.

#### Use the `Backfill` feature to trigger past dates

![Backfill screenshot](https://github.com/user-attachments/assets/43077cc1-e591-4d96-9ce7-d05e7c5ecf4f)

1. Within the execution for Yellow Taxi data for the year 2020 and month 12: what is the uncompressed file size (i.e., the output file `yellow_tripdata_2020-12.csv` of the extract task)?

- 134.5 MB

2. What is the rendered value of the variable `file` when the inputs `taxi` is set to `green`, `year` is set to `2020`, and `month` is set to `04` during execution?

- `green_tripdata_2020-04.csv`

![Rendered file screenshot](https://github.com/user-attachments/assets/a448c207-49d9-41c4-8445-b82de4cc5950)

3. How many rows are there for the Yellow Taxi data for all CSV files in the year 2020?

- **24,648,499**

```
SELECT
  SUM(row_count) AS total_trips_2020
FROM `curious-helix-484819-a6.taxi_dataset.__TABLES__`
WHERE table_id LIKE 'yellow_tripdata_2020_%'
  AND table_id NOT LIKE '%_ext'
  AND type = 1;
```

4. How many rows are there for the Green Taxi data for all CSV files in the year 2020?

- **1,734,051**

```
SELECT
  SUM(row_count) AS total_trips_2020
FROM `curious-helix-484819-a6.taxi_dataset.__TABLES__`
WHERE table_id LIKE 'green_tripdata_2020_%'
  AND table_id NOT LIKE '%_ext'
  AND type = 1;
```

5. How many rows are there for the Yellow Taxi data for the March 2021 CSV file?

- **1,925,152**

```
SELECT COUNT(*)
FROM `curious-helix-484819-a6.taxi_dataset.yellow_tripdata_2021_03`;
```

6. How do you configure the timezone to New York in a Schedule trigger?

```
- id: yellow_schedule
  type: io.kestra.plugin.core.trigger.Schedule
  cron: "40 22 1 * *"
  timezone: America/New_York
  inputs:
    taxi: yellow
```
