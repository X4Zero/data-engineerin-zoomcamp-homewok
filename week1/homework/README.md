# Homework data-engineering-zoomcamp
Author: Alexander Romero

## Q1:
370.0.0

## Q2:
'''
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
'''

## Q3 How many taxi trips were there on January 15?
ANSWER: 53024

## Q4 On which day it was the largest tip in January? (note: it's not a typo, it's "tip", not "trip")
ANSWER: 2021-01-20