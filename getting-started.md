---
description: >-
  This page will guide you through the basic steps to install csvbox.io into
  your app and start accepting data from your users.
---

# Getting Started

## Overview

With csvbox.io you can add a production-ready import feature to your web app in just a few minutes.

#### Key Concepts

Here are a few important terms used throughout the application:

**User:** Any person who uses your application.

**File:** The spreadsheet file that the users want to upload to your application.

{% hint style="info" %}
Users can upload .csv, .xlsx or .xls file formats.
{% endhint %}

**Sheet:** It refers to the data modal that specifies the structure of the data you want to accept. You can add columns to the sheet and configure validation criteria via your csvbox.io dashboard. 

{% hint style="info" %}
Users will be able to match the headers of their file columns with the sheet columns and clean data before uploading.
{% endhint %}

**Import:** The entire process where the user invokes the csvbox.io importer to select the file, match columns, validate data, and submit the file is called Import.

**Destination:** It is the end location where the csvbox.io importer will push the data uploaded by the user.

## Setup

It's easy to get started using csvbox.io importer. In this guide, we will use the bare minimum to get up and running with accepting files from your users.

### 1. Add a sheet

Sheets define the format of the data that you want to accept from the users.

Go to the 'Sheets' page in your dashboard. Add a sheet and specify columns. Configure the validation rules and data format for each column.

{% hint style="info" %}
When users attempt to upload a file, the importer will validate the data for every column and inform the users if there are any errors. Users have to resolve the errors before submitting the file.
{% endhint %}

Under the 'Settings' tab, configure the destination where you want the data to be pushed. The destination could be an API endpoint, Amazon S3 bucket, MYSQL database, or any of the other options mentioned [here](https://help.csvbox.io/destinations). 

### 2. Install Code

Go to the 'Code' tab of the sheet and copy the integration code. The code will look something like this:

```javascript
<button class="btn btn-primary" onclick="importer.openModal();">Import</button>
<script type="text/javascript" src="http://js.csvbox.io/embed/script"></script>
<script type="text/javascript">
    function callback(result) {
        if(result){
            console.log("success");
            //custom code
        }else{
            console.log("fail");
            //custom code
        }
    }
    let importer = new CSVBoxImporter("z0ad8U7en2pFU0bT3z8o5UAUOi5BX6",{        
    }, callback);
    
    importer.setUser({
        user_id: "default123"
    })
</script>
```

Place the code in your application at the location you want to display the import button.

{% hint style="info" %}
You can change the classes of the `<button>` element as per your styling requirements. You also change the default button text **Import** as per your need.
{% endhint %}

#### Referencing the user

You can configure the **`setUser`** method to identify and match the users with their respective imports. When calling the **`setUser`**method, pass custom user attributes that help you identify the users in your platform. The custom user attributes will be pushed to your destination along with the uploaded data.

**user\_id** is the only custom attribute that is mandatory. Apart from **user\_id,** you can add up to 4 custom attributes in the `<key>: <value>`format. Example:

```javascript
  importer.setUser({
        user_id: "1a2b3c4d5e6f",
        team_id: "sales2",
        isAuthenticated: "true",
        permissionLevel: "admin",
        email: "abc@example.com"
    })
```

#### Callback function

Once the import is complete the **`callback`**function returns the status of the import. You can write custom code to handle the success or fail conditions as per your workflow.

### 3. Receive Data

Once the code is installed the users will be able to submit their files via the csvbox importer. The raw files uploaded by the users will be available on your dashboard's 'Import' page. The data will also be pushed to your app as per the destination type configuration of your sheet.

#### Sample JSON response for destination Webhook: <a id="sample-response"></a>

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

{% hint style="warning" %}
All import data and RAW files will be retained for one month. You also have the option to delete them as soon as they are pushed to the destination.
{% endhint %}

#### Import Complete Webhook

Optionally, you can subscribe to the import complete event webhook via the sheet settings page. This webhook will fire when the csvbox completes the import process for any user. Here is some example JSON that could be sent to your webhook endpoint:

```javascript
[
  {
    "import_id": 79418895,
    "sheet_id": 575,
    "sheet_name": "Products Import",
    "destination_type": "webhook"
    "row_count": 100,
    "row_success": 98,
    "row_fail": 2,
    "import_status": "Partial",
    "import_starttime": 87987897897,
    "import_endtime": 90890890809,
    "raw_file": "https://file-download-link",
    "custom_fields": {
      "user_id": "Z1001"
    }
  }
]
```

## Import Links

Use Import Links to accept files from your users without a website or an app. Create an import page in just a few clicks and share the link with your users—no code required. It is an alternative to the import button that can be set up by adding the integration code \(mentioned above.\)

After you have created a sheet go to the 'Code' tab on the Edit Sheet page. Below the integration code find the Import Link of the sheet. It will look something like this:

```javascript
https://app.csvbox.io/upload/2gzJa5YO3QPLYK6Bj7Qmq5bpbFqXno?user_id=default123
```

Simply share this link with your users to start collecting spreadsheet files.

#### Referencing the user in the Import Links

You can configure the query parameters in the link to identify and match the users with their respective imports. Add up to 5 query parameters with custom user attributes that help you identify the users in your platform. The custom user attributes will be pushed to your destination along with the uploaded data.

**user\_id** is the only custom attribute that is mandatory. Apart from **user\_id,** you can add up to 4 custom attributes in the`&key=value`format. Example:

```javascript
https://app.csvbox.io/upload/2gzJa5YO3QPLYK6Bj7Qmq5bpbFqXno?user_id=1a2b3c4d5e6f&team_id=sales2&isAuthenticated=true&permissionLevel=admin&email=abc@example.com
```

