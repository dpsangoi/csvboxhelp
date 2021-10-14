---
description: >-
  This page describes the various validation options available inside the
  importer.
---

# Validations

## Column Data Types

While creating a sheet you can specify the column to be any of the data types mentioned below. If the incoming CSV data does not match the column data type (and its validation rules), then the user will see a relevant error message identifying what the problem is and how to fix it.  

### Text

### Number

### Email

### Date

### Boolean

### Regex

### IP

### URL

### Credit Card

### Phone Number

### List

With the **List** data type, you can specify a list of acceptable values. The importer will compare the CSV column data with the list of acceptable values and throw a validation error if there is a mismatch.

