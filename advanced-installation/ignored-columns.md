---
description: Option for users to drop columns for the import process.
---

# Ignored Columns

There can be a situation where users want to skip a column during data submission. This is especially useful when using the importer to update existing data. To avoid overwriting existing columns, the users can mark those columns as **Ignored** and the importer will skip them.

With CSVbox you can give the option to the users to mark certain columns as Ignored.&#x20;

### Enabling Ignored Columns

The first step is to activate the Ignore Columns option via your CSVbox dashboard.

1. Login to your account.
2. Edit the sheet of your choice.
3. Go to the '**Options**' Tab.
4. Select '**Yes**' for the '**Allow Columns to be Ignored**' field.
5. Click '**Save**'.

The importer will then show the option to mark the columns as Ignored on the Column Mapping screen.

<figure><img src="../.gitbook/assets/Ignore Colum1..png" alt=""><figcaption><p>Ignored Column Selection</p></figcaption></figure>

<figure><img src="../.gitbook/assets/Ignore Colum2.png" alt=""><figcaption><p>Ignored Column</p></figcaption></figure>

The columns that are marked as Ignored will not be visible on the Verify Data screen.

{% hint style="info" %}
For columns that are marked as "Required", the Ignore Column option will not be available for selection.
{% endhint %}

### **Data from Unmapped Columns**

The Ignored Columns will not be pushed to any destination. Only the metadata (List of Ignored Columns) will be pushed to the following destinations:

1. [API/Webhook](../destinations/#webhook)
2. [Zapier](../destinations/zapier.md)
3. [Client Side](../getting-started/3.-receive-data.md#data-at-the-client-side)

#### Ignored Column List

In the API response JSON object, the list of Ignored Columns will be displayed inside the **ignored\_columns** object as shown below. The **ignored\_columns** object will be visible only if the Ignored Columns are activated. In the example below check lines 16 and 36.

{% code lineNumbers="true" %}
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
          "Quantity": "3"        
    },
    "custom_fields": {
      "user_id": "1002"
    },
    "ignored_columns": ["qualification", "experience"]
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
           "_ignored_data":{
		"qualification": "MA",
		"experience": "6"
           }
        },
    "custom_fields": {
      "user_id": "1002"
    },
    "ignored_columns": ["qualification", "experience"]
  }
]
```
{% endcode %}

