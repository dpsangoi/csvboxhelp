---
description: Allow users to submit columns not included in the sheet template.
---

# Unmapped Columns

There can be cases where each of your users has unique columns in their sheets that they want to upload. These columns are not known to you beforehand and hence cannot be configured as part of the sheet template. These columns can be discovered only after the user uploads the file. Hence, they cannot be configured as [dynamic columns](dynamic-columns.md#basic-installation) either. We call these columns **Unmapped Columns**.

With CSVbox you now have the option to accept Unmapped Columns as well.&#x20;

### Enabling Unmapped Columns

You can start accepting data from the Unmapped Columns by simply activating the option via your CSVbox dashboard.

1. Login to your account.
2. Edit the sheet of your choice.
3. Go to the '**Options**' Tab.
4. Select '**Yes**' for the '**Accept Unmapped Columns?**' field.
5. Click '**Save**'.

The importer will then start accepting data from the Unmapped Columns submitted by the users.

### **Receiving Data from Unmapped Columns**

The data from the Unmapped Columns is available in the data destinations along with the data from the regular columns. Currently, **** Unmapped Columns are supported by the following destinations only:

1. [API/Webhook](../destinations/#webhook)
2. [Amazon S3](../destinations/#amazon-s3)

#### API/Webhook Data Destination

In the API response JSON object, the dynamic data will be displayed inside the **\_unmapped\_data** object as shown below. The **\_unmapped\_data** object will be visible only if the Unmapped Columns are activated. In the example below check lines 12 and 32.

```json
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
          "_unmapped_data":{
		"Barcode": "7832748937489",
		"_empty_header_1": "TP-Link",
		"Tags": "electronics, networking"
           }
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
           "_unmapped_data":{
		"Barcode": "4532748937411",
		"_empty_header_1": "EPower",
		"Tags": ""
           }
        },
    "custom_fields": {
      "user_id": "1002"
    }
  },
]

```

{% hint style="info" %}
If any of the Unmapped Columns do not have a header specified in the user uploaded file, then the app will auto-insert column names  _\_empty\_header\_1_, _\_empty\_header\_2_, and so on.
{% endhint %}

#### S3 Data Destination

In the AWS S3 file store, the Unmapped Columns will be added as new columns in the uploaded file.
