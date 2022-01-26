# Homework data-engineering-zoomcamp
Author: Alexander Romero

## Q1:
370.0.0

## Q2:
```
var.project
  Your GCP Project ID

  Enter a value: dtc-de-339413

google_storage_bucket.data-lake-bucket: Refreshing state... [id=dtc_data_lake_dtc-de-339413]
google_bigquery_dataset.dataset: Refreshing state... [id=projects/dtc-de-339413/datasets/trips_data_all]

Note: Objects have changed outside of Terraform

Terraform detected the following changes made outside of Terraform since the last "terraform apply":

  # google_bigquery_dataset.dataset has changed
  ~ resource "google_bigquery_dataset" "dataset" {
        id                              = "projects/dtc-de-339413/datasets/trips_data_all"
      + labels                          = {}
        # (10 unchanged attributes hidden)

        # (4 unchanged blocks hidden)
    }

  # google_storage_bucket.data-lake-bucket has changed
  ~ resource "google_storage_bucket" "data-lake-bucket" {
        id                          = "dtc_data_lake_dtc-de-339413"
      + labels                      = {}
        name                        = "dtc_data_lake_dtc-de-339413"
        # (9 unchanged attributes hidden)


        # (2 unchanged blocks hidden)
    }
```

## Q3 How many taxi trips were there on January 15?
ANSWER: 53024

```
SELECT COUNT (*) FROM  yellow_taxi_trips WHERE tpep_pickup_datetime::timestamp::date = '2021-01-15';
```

## Q4 On which day it was the largest tip in January? (note: it's not a typo, it's "tip", not "trip")
ANSWER: 2021-01-20
```
SELECT  tpep_pickup_datetime, MAX(tip_amount) MAX_TIP
FROM  yellow_taxi_trips 
WHERE tpep_pickup_datetime 
BETWEEN '2021-01-01 00:00:00'::timestamp AND '2021-01-31 23:59:59'
GROUP BY tpep_pickup_datetime
ORDER BY MAX_TIP DESC
```

## Q5 Most popular destination
What was the most popular destination for passengers picked up in central park on January 14? Enter the zone name (not id). If the zone name is unknown (missing), write "Unknown"  
ANSWER: Upper East Side North
```
SELECT z."LocationID", z."Zone",  count(*) NUM_TRIPS
FROM  yellow_taxi_trips ytt
INNER JOIN zones z ON z."LocationID" = ytt."PULocationID"
WHERE ytt.tpep_pickup_datetime::timestamp::date = '2021-01-14'
GROUP BY  z."LocationID", z."Zone"
ORDER BY NUM_TRIPS DESC
```

## Q6 Most expensive route
What's the pickup-dropoff pair with the largest average price for a ride (calculated based on total_amount)? Enter two zone names separated by a slashFor example:"Jamaica Bay / Clinton East"If any of the zone names are unknown (missing), write "Unknown". For example, "Unknown / Clinton East".  
ANSWER: Alphabet City/Unknown

```
SELECT z."LocationID" PULocation_ID, z."Zone" PUZone, z2."LocationID" DOLocation_ID, z2."Zone" DOZone, AVG(ytt.total_amount) AS AVG_AMOUNT
FROM yellow_taxi_trips ytt
INNER JOIN zones z ON z."LocationID" = ytt."PULocationID"
INNER JOIN zones z2 ON z2."LocationID" = ytt."DOLocationID"
GROUP BY z."LocationID",z."Zone", z2."LocationID",z2."Zone"
ORDER BY AVG_AMOUNT DESC
```