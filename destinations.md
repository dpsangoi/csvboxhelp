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

## Webhook / API

The data will be pushed to a webhook endpoint as configured in the sheet settings. You can choose between JSON, XML, and FORM Data formats for receiving data to your webhook. The data will be pushed in chunks of rows. The number of rows per chunk can be configured in the sheet settings.

#### Sample JSON POST to API:

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
      "user_id": "1002"
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
      "user_id": "1002"
    }
  },
]
```

{% hint style="info" %}
The data will come in as HTTP POST requests. Each request will have an array of rows based on the chunk size defined in the sheet settings. You can set the chunk size to 1 to receive 1 record per HTTP request.
{% endhint %}

## Amazon S3

The files uploaded by the users can be pushed to the AWS S3 Bucket of your choice. You simply need to select the destination type as 'Amazon S3' and provide the AWS credentials, bucket/folder, and access policy for receiving the files. 

{% hint style="info" %}
The files in S3 will be stored with the filename **{{import\_id}}\_{{userId}}.csv** where userId is the optional attribute that you configure in the **CSVBoxImporter\(\)** function of the installation code.
{% endhint %}

## MySQL Database

coming soon

