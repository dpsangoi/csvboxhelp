---
description: >-
  This page will guide you through the basic steps to install the csvbox.io CSV
  importer widget into your app and start accepting data from your users.
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

**Sheet or Template: **It refers to the data modal that specifies the structure of the data you want to accept. You can add columns to the sheet and configure validation criteria via your csvbox.io dashboard.&#x20;

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

Under the 'Settings' tab, configure the destination where you want the data to be pushed. The destination could be an API endpoint, Amazon S3 bucket, MYSQL database, or any of the other options mentioned [here](https://help.csvbox.io/destinations).&#x20;

### 2. Install Code

Go to the 'Code' tab of the sheet and find the integration code. Place the code in your application at the location you want to display the import button.

{% tabs %}
{% tab title="Javascript" %}
Sample code with basic usage:

```javascript
<button class="btn btn-primary" data-csvbox disabled onclick="importer.openModal();">Import</button>
<script type="text/javascript" src="http://js.csvbox.io/embed/script"></script>
<script type="text/javascript">
    function callback(result, data) {
        if(result){
            console.log("success");
            console.log(data.row_success + " rows uploaded");
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

{% hint style="info" %}
Each sheet has a unique Licence Key. Find the Licence Key of the sheet on the 'Code' tab of the sheet page and pass it to the **CSVBoxImporter** function.
{% endhint %}
{% endtab %}

{% tab title="React" %}
Install using npm:

```javascript
npm install @csvbox/react
```

&#x20;This will give you access to the **`CSVBoxButton`** component having the basic functionality of our importer. Import the **`CSVBoxButton`** component to your project.

```javascript
import { CSVBoxButton } from '@csvbox/react'
```

Basic usage:

```javascript
<CSVBoxButton
  licenseKey="z0ad8U7en2pFU0bT3z8o5UAUOi5BX6"
  user={{
    user_id: "default123"
  }}
  onImport={(result, data) => {
    if(result){
      console.log("success");
      console.log(data.row_success + " rows uploaded");
      //custom code
    }else{
      console.log("fail");
      //custom code
    }
  }}
  render={(launch)=>{
    return <button data-csvbox disabled onClick={launch}>Upload file</button>;
  }}
>
  Import
</CSVBoxButton>
```

{% hint style="info" %}
Each sheet has a unique Licence Key. Find the Licence Key of the sheet on the Code section of the sheet page and attach it to the **licenseKey** property of the **CSVBoxButton **component.
{% endhint %}

{% hint style="info" %}
The optional **render **property allows you to pass in your button to use in place of the standard csvbox element.
{% endhint %}
{% endtab %}

{% tab title="Angular" %}
Install using npm:

```javascript
npm install @csvbox/angular
```

Import:&#x20;

Add `CSVBoxAngularModule` to your module imports.

```javascript
import { CSVBoxAngularModule } from "@csvbox/angular";

@NgModule({
  ...
  imports: [
    ...
    CSVBoxAngularModule
  ]
})
```

Once you have this setup, in your app component file, you will be able to import and access the`CSVBoxMethods` module for use.

It will bring the `csvbox-button` component into your project. Example:

```
<csvbox-button [licenseKey]="licenseKey" [onImport]="onData.bind(this)" [user]="user" [dynamicColumns]="dynamicColumns">Import</csvbox-button>
```

Basic usage:

```javascript
import { CSVBoxMethods } from "@csvbox/angular"

@Component({
  selector: 'app-root',
  template: `
    <csvbox-button
      [licenseKey]="licenseKey"
      [user]="user"
      [dynamicColumns]="dynamicColumns"
      [onImport]="onData.bind(this)">
      Import
    </csvbox-button>
  `
})

export class AppComponent implements CSVBoxMethods {

  title = 'example';
  licenseKey = 'YOUR_LICENSE_KEY_HERE';
  user = { user_id: 'default123' };

  onData(result: boolean, data: any) {
    if(result) {
      console.log("Sheet uploaded successfully");
      console.log(data.row_success + " rows uploaded");
    }else{
      console.log("There was some problem uploading the sheet");
    }
  }

}
```

{% hint style="info" %}
Each sheet has a unique Licence Key. Find the Licence Key of the sheet on the Code section of the sheet page and attach it to the **licenseKey** property of the **AppComponent**.
{% endhint %}

Styling the button:

In order to style the `<csvbox-button>` from within your parent component, ensure that your parent component has `ViewEncapsulation.None`, pass down a class to `<csvbox-button>`, and now you will be able to style the `button` one-level down.

```javascript
import { Component, ViewEncapsulation } from '@angular/core';
```

```javascript
@Component({
  selector: 'app-root',
  template: `
    <csvbox-button
      [licenseKey]="licenseKey"
      [user]="user"
      [dynamicColumns]="dynamicColumns"
      [onImport]="onData.bind(this)"
      class=“csvbox-btn”      
      >
      Import
    </csvbox-button>
  `,
  encapsulation: ViewEncapsulation.None,
  styles: [`
    .csvbox-btn button {        
        background: #007bff;
        border-radius: 3px;        
      }
  `],
export class AppComponent implements CSVBoxMethods { 
    //...
}
```
{% endtab %}

{% tab title="Vuejs" %}
Install using npm:

```javascript
npm install @csvbox/vuejs
```

&#x20;This will give you access to the **`CSVBoxButton`** component. Import the **`CSVBoxButton`** component to your project.

```javascript
import { CSVBoxButton } from '@csvbox/vuejs'
```

&#x20;Now just import the **`CSVBoxButton`** and include it in your Vue `components`, and you're ready to get started.

Basic usage:

```javascript
<template>
  <div id="app">
    <CSVBoxButton 
      :licenseKey="licenseKey"
      :user="user"
      :dynamicColumns="dynamicColumns"      
      :onImport="onImport">
      Upload File
    </CSVBoxButton>
  </div>
</template>

<script>
import { CSVBoxButton } from '@csvbox/vuejs';

export default {
  name: 'App',
  components: {
    CSVBoxButton,
  },
  data: () => ({
    licenseKey: 'z0ad8U7en2pFU0bT3z8o5UAUOi5BX6',
    user: {
      user_id: 'default123',
    },
  }),
  methods: {    
    onImport: function (result, data) {    
       if(result){
          console.log("success");
          console.log(data.row_success + " rows uploaded");
          //custom code
      }else{
          console.log("fail");
          //custom code
      }
    }
  },
}
</script>
```

{% hint style="info" %}
Each sheet has a unique Licence Key. Find the Licence Key of the sheet on the Code section of the sheet page and attach it to the **licenseKey** property of the **CSVBoxButton **component.
{% endhint %}
{% endtab %}
{% endtabs %}

#### Referencing the user

You can configure **custom user attributes** in the installation code to identify the users in your platform and match them with their respective imports.&#x20;

{% tabs %}
{% tab title="Javascript" %}
Pass custom user attributes as input parameters to the **`setUser`**method. The custom user attributes will be pushed to your destination along with the uploaded data.

**user\_id **is the only custom attribute that is mandatory. Apart from **user\_id, **you can add up to 4 custom attributes in the**`<key>: <value>`**format. Example:

```javascript
 importer.setUser({
        user_id: "1a2b3c4d5e6f",
        team_id: "sales2",
        isAuthenticated: "true",
        permissionLevel: "admin",
        email: "abc@example.com"
    })
```
{% endtab %}

{% tab title="React" %}
Pass custom user attributes as an object to the **`user`**property of the **`CSVBoxButton`** component. The custom user attributes will be pushed to your destination along with the uploaded data.

**user\_id **is the only custom attribute that is mandatory. Apart from **user\_id, **you can add up to 4 custom attributes in the **`<key>: <value>`**format. Example:

```javascript
  user={{
              user_id: "1a2b3c4d5e6f",
              team_id: "sales2",
              isAuthenticated: "true",
              permissionLevel: "admin",
              email: "abc@example.com"
  }}
```
{% endtab %}

{% tab title="Angular" %}
Pass custom user attributes as an object to the **`user`**property of the AppComponent. The custom user attributes will be pushed to your destination along with the uploaded data.

**user\_id **is the only custom attribute that is mandatory. Apart from **user\_id, **you can add up to 4 custom attributes in the **`<key>: <value>`**format. Example:

```javascript
  user={
              user_id: "1a2b3c4d5e6f",
              team_id: "sales2",
              isAuthenticated: "true",
              permissionLevel: "admin",
              email: "abc@example.com"
 }
```
{% endtab %}

{% tab title="Vuejs" %}
Pass custom user attributes as an object to the **`user`**property of the **`CSVBoxButton`** component. The custom user attributes will be pushed to your destination along with the uploaded data.

**user\_id **is the only custom attribute that is mandatory. Apart from **user\_id, **you can add up to 4 custom attributes in the **`<key>: <value>`**format. Example:

```javascript
  user: {
              user_id: "1a2b3c4d5e6f",
              team_id: "sales2",
              isAuthenticated: "true",
              permissionLevel: "admin",
              email: "abc@example.com"
  },
```
{% endtab %}
{% endtabs %}

#### Callback function

Once the user uploads a file the importer will return the status of the import along with metadata describing the completed import. Data is returned via two variables: **`result `**and **`data`**.&#x20;

1. **`result `**- It is of type boolean with the value **true **if the import is successful and **false **if the import fails.
2. **`data `**- It returns JSON data as shown below:

```javascript
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
```

You can write custom code to handle the success or failure conditions client side.

{% tabs %}
{% tab title="Javascript" %}
The **`result `**and **`data`**variables will be available in the **`callback`**function that is triggered when the import is completed.

```javascript
function callback(result, data) {
        if(result){
            console.log("success");
            console.log(data.row_success + " rows uploaded");
            //custom code
        }else{
            console.log("fail");
            //custom code
        }
    }
```
{% endtab %}

{% tab title="React" %}
The **`onImport `**property provides access to the **`result `**and **`data`**variables.

```javascript
  onImport={(result, data) => {
    if(result){
      console.log("success");
      console.log(data.row_success + " rows uploaded");
      //custom code
    }else{
      console.log("fail");
      //custom code
    }
```
{% endtab %}

{% tab title="Angular" %}
The **`onImport `**property provides access to the **`result `**and **`data`**variables via the specified callback function.

```javascript
  onData(result: boolean, data: any) {
    if(result) {
      console.log("Sheet uploaded successfully");
      console.log(data.row_success + " rows uploaded");
    }else{
      console.log("There was some problem uploading the sheet");
    }
  }
```
{% endtab %}

{% tab title="Vuejs" %}
The **`onImport `**property provides access to the **`result `**and **`data`**variables.

```javascript
onImport: function (result, data) {    
       if(result){
          console.log("success");
          console.log(data.row_success + " rows uploaded");
          //custom code
      }else{
          console.log("fail");
          //custom code
      }
}
```
{% endtab %}
{% endtabs %}

### 3. Receive Data

Once the code is installed the users will be able to submit their files via the csvbox importer. The raw files uploaded by the users will be available on your dashboard's 'Import' page. The data will also be pushed to your app as per the destination type configuration of your sheet.

#### Sample JSON response for destination Webhook: <a href="sample-response" id="sample-response"></a>

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

Use Import Links to accept files from your users without a website or an app. Create an import page in just a few clicks and share the link with your users—no code required. It is an alternative to the import button that can be set up by adding the integration code (mentioned above.)

After you have created a sheet go to the 'Code' tab on the Edit Sheet page. Below the integration code find the Import Link of the sheet. It will look something like this:

```javascript
https://app.csvbox.io/upload/2gzJa5YO3QPLYK6Bj7Qmq5bpbFqXno?user_id=default123
```

Simply share this link with your users to start collecting spreadsheets.

#### Referencing the user in the Import Links

You can configure the query parameters in the link to identify and match the users with their respective imports. Add up to 5 query parameters with custom user attributes that help you identify the users in your platform. The custom user attributes will be pushed to your destination along with the uploaded data.

**user\_id **is the only custom attribute that is mandatory. Apart from **user\_id, **you can add up to 4 custom attributes in the`&key=value`format. Example:

```javascript
https://app.csvbox.io/upload/2gzJa5YO3QPLYK6Bj7Qmq5bpbFqXno?user_id=1a2b3c4d5e6f&team_id=sales2&isAuthenticated=true&permissionLevel=admin&email=abc@example.com
```
