---
description: >-
  This document defines the different destinations where the importer can push
  the data uploaded by the users. The following is the list of supported
  destinations.
---

# Data Destinations

{% hint style="info" %}
At a time only one destination can be selected per sheet.
{% endhint %}

## None

The user-uploaded data will not be pushed anywhere. The files will be, however, available for download via the csvbox.io admin.

## Webhook

The data will be pushed to a webhook endpoint as configured in the sheet settings. You can choose between JSON, XML, and FORM Data formats for receiving data to your webhook. The data will be pushed in chunks of rows. The number of rows per chunk can be configured in the sheet settings.

#### Sample JSON POST to your API:

```javascript
[
  {
    "import_id": 79418895,
    "sheet_id": 55,
    "sheet_name": "Products",
    "row_number": 1,
    "row_data": {
          "Name": "TP-Link TL-WN822N Wireless N300 High Gain USB Adapter",
          "SKU": "AS-100221",
          "Price": "33.00",
          "Quantity": "3",
          "Image URL": "https://cdn.shopify.com/s/files/1/1491/9536/products/31jJOj1DS5L_070b4893-b7af-482f-8a15-d40f5e06760d.jpg?v=1521803806"
    },
    "custom_fields": {
      "user_id": "1a2b3c4d5e6f",
      "team_id": "sales2"
    }
  },
  {
    "import_id": 79418895,
    "sheet_id": 55,
    "sheet_name": "Products",
    "row_number": 2,
    "row_data":{
          "Name": "EPower Technology EP-600PM Power Supply 600W ATX12V 2.3 Single 120mm Cooling Fan Bare",
          "SKU": "AS-103824",
          "Price": "95.35",
          "Quantity": "8",
          "Image URL": "https://cdn.shopify.com/s/files/1/1491/9536/products/71pRC5VjF-L_8f840eb9-6a47-407f-999c-490f7814159d.jpg?v=1521803806"
        },
    "custom_fields": {
      "user_id": "1a2b3c4d5e6f"
      "team_id": "sales2"
    }
  },
]
```

{% hint style="info" %}
The data will come in as HTTP POST requests. Each request will have an array of rows based on the chunk size defined in the sheet settings. You can set the chunk size to 1 to receive 1 record per HTTP request.
{% endhint %}

## Amazon S3

The files uploaded by the users can be pushed to the AWS S3 Bucket of your choice. You simply need to select the destination type as 'Amazon S3' and provide the AWS credentials, bucket/folder name, and access policy for storing the files.

{% hint style="info" %}
The data will be stored as S3 objects with the name **{{import\_id}}\_{{user\_id}}.csv** where **user\_id** is the custom user attribute that you reference via the **`setUser`**method while installing the importer code. The other 4 custom user attributes will be saved as the [user-defined metadata](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingMetadata.html) of the S3 object.
{% endhint %}

## MySQL Database

Import CSV files and Excel sheets directly into your MySQL tables. How it works:

* Select the destination type as 'MySQL Database'.
* Connect your MySQL database by providing the credentials.
* Specify table name where you want the data to be pushed.

![csv to mysql](../.gitbook/assets/mysql.jpg)

* Map sheet columns to the table column.
* You can also map custom attributes to table columns.

![map sheet to table columns](../.gitbook/assets/map-columns.jpg)

The user CSV data will then be directly be appended to the MySQL table.
