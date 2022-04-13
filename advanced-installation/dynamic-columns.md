---
description: Add new columns to the template at run-time.
---

# Dynamic Columns

Consider a scenario where you cannot have a fixed template for collecting data. The columns in the data model depend on the end user's preferences and/or some other criteria.&#x20;

For such cases, csvbox provides the flexibility to add unique **dynamic columns** for each import at run-time.

### Basic Installation

You can configure **dynamic columns** via the installation code.

Here's a basic configuration that adds 2 dynamic columns **qualification** and **experience**.&#x20;

{% tabs %}
{% tab title="Javascript" %}
Pass the dynamic columns that you want to add as an array input parameter to the**`setDynamicColumns()`**method while initializing the importer.

```javascript
importer.setDynamicColumns([
         {
          "column_name" : "qualification"        
         },
         {
          "column_name": "experience"         
          }
])
```

Basic installation steps are available [here](../getting-started/#2.-install-code).
{% endtab %}

{% tab title="React" %}
Pass the dynamic columns as an object to the **`dynamicColumns`**property of the **`CSVBoxButton`** component.&#x20;

```javascript
  dynamicColumns={[
               {
                 "column_name" : "qualification"        
               },
               {
                  "column_name": "experience"         
              }
  ]}
```

Basic installation steps are available [here](../getting-started/#2.-install-code).
{% endtab %}

{% tab title="Angular" %}
Add `[dynamicColumns]="dynamicColumns"` to the existing template.&#x20;

```
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
```

Then pass the dynamic columns as an object to the**`dynamicColumns`**property of the AppComponent. Example:

```javascript
  dynamicColumns=[
               {
                 column_name : "qualification"        
               },
               {
                  column_name: "experience"         
              }
  ]
```

Basic installation steps are available [here](../getting-started/#2.-install-code).
{% endtab %}

{% tab title="Vuejs" %}
Add `:dynamicColumns="dynamicColumns"` to the existing template.&#x20;

```
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
```

Pass the dynamic columns as an object to the**`dynamicColumns`**property of the**`CSVBoxButton`** component. Example:

```javascript
  dynamicColumns: [
               {
                 column_name : "qualification"        
               },
               {
                  column_name: "experience"         
              }
  ]
```

Basic installation steps are available [here](../getting-started/#2.-install-code).
{% endtab %}
{% endtabs %}

Dynamic columns will be visible in the importer along with the other regular columns.

<img src="../.gitbook/assets/Dynamic Columns.jpg" alt="Dynamic Columns" data-size="original">

### **Advanced Configuration**

Dynamic columns can be configured by passing additional**`<key>: <value>`**pairs to the array input parameter of the**`setDynamicColumns()`**method.

Here is an example illustrating more configuration options.

{% tabs %}
{% tab title="Javascript" %}
```javascript
 importer.setDynamicColumns([
         {
          "column_name" : "qualification",
          "display_label": "Highest Qualification",
          "info_hint": "What is your highest educational degree",
          "matching_keywords": "degree, education",
          "type": "text",
          "validators": 
            {          	
              "min_length": 2,
              "max_length": 50
            },
          "required": true
        },
        {
          "column_name": "experience",
          "display_label": "Work Experience",
          "info_hint": "Years of work experience",
          "matching_keywords": "",
          "type": "number",
          "validators": 
            {          	
              "min_value": 0,
              "max_value": 100
            },
          "required": false
        },
        {
          "column_name": "gender",
          "display_label": "Gender",
          "info_hint": "",
          "matching_keywords": "",
          "type": "list",
          "validators": 
            {          	
              "values": [
                              {"value": "m", "display_label": "male"},
                              {"value": "f", "display_label": "female"} 
                        ],
              "case_sensitive": false
            },
          "required": true
        }
])
```
{% endtab %}

{% tab title="React" %}
```javascript
  dynamicColumns={[
         {
          "column_name" : "qualification",
          "display_label": "Highest Qualification",
          "info_hint": "What is your highest educational degree",
          "matching_keywords": "degree, education",
          "type": "text",
          "validators": 
          {          	
            "min_length": 2,
            "max_length": 50
          },
          "required": true
    },
 {
          "column_name": "experience",
          "display_label": "Work Experience",
          "info_hint": "Years of work experience",
          "matching_keywords": "",
          "type": "number",
          "validators": 
          {          	
            "min_value": 0,
            "max_value": 100
          },
          "required": false
    },
    {
          "column_name": "gender",
          "display_label": "Gender",
          "info_hint": "",
          "matching_keywords": "",
          "type": "list",
          "validators": 
          {          	
            "values": [
                            {"value": "m", "display_label": "male"},
                            {"value": "f", "display_label": "female"} 
                      ],
            "case_sensitive": false
          },
          "required": true
    }
]}
```
{% endtab %}

{% tab title="Angular" %}
```javascript
  dynamicColumns=[
         {
          column_name : "qualification",
          display_label: "Highest Qualification",
          info_hint: "What is your highest educational degree",
          matching_keywords: "degree, education",
          type: "text",
          validators": 
          {          	
            min_length: 2,
            max_length: 50
          },
          required: true
    },
 {
          column_name: "experience",
          display_label: "Work Experience",
          info_hint: "Years of work experience",
          matching_keywords: "",
          type: "number",
          "validators: 
          {          	
            min_value: 0,
            max_value: 100
          },
          required: false
    },
    {
          column_name: "gender",
          display_label: "Gender",
          info_hint: "",
          matching_keywords: "",
          type: "list",
          validators: 
          {          	
            values: [
                            {value: "m", display_label: "male"},
                            {value: "f", display_label: "female"} 
                      ],
            case_sensitive: false
          },
          required: true
    }
]
```
{% endtab %}

{% tab title="Vuejs" %}
```javascript
  dynamicColumns: [
         {
          column_name : "qualification",
          display_label: "Highest Qualification",
          info_hint: "What is your highest educational degree",
          matching_keywords: "degree, education",
          type: "text",
          validators": 
          {          	
            min_length: 2,
            max_length: 50
          },
          required: true
    },
 {
          column_name: "experience",
          display_label: "Work Experience",
          info_hint: "Years of work experience",
          matching_keywords: "",
          type: "number",
          "validators: 
          {          	
            min_value: 0,
            max_value: 100
          },
          required: false
    },
    {
          column_name: "gender",
          display_label: "Gender",
          info_hint: "",
          matching_keywords: "",
          type: "list",
          validators: 
          {          	
            values: [
                            {value: "m", display_label: "male"},
                            {value: "f", display_label: "female"} 
                      ],
            case_sensitive: false
          },
          required: true
    }
]
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**column\_name** is the only key that is mandatory for adding a dynamic column.
{% endhint %}

#### Configuration Options

| Key                                                                                                   | Description                                                                                                                                                                                                 |
| ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [column\_name](../dashboard-settings/sheet-options.md#column-name) <mark style="color:red;">\*</mark> | It is the column name that will be pushed to the data destination.                                                                                                                                          |
| [display\_label](../dashboard-settings/sheet-options.md#display-label)                                | The user-friendly column label that the users will see in the importer.                                                                                                                                     |
| [info\_hint](../dashboard-settings/sheet-options.md#info-hint)                                        | Info Hints are help tooltips that will get displayed when the users hover the mouse over the Display Label (or click it) in the importer.                                                                   |
| [matching\_keywords](../dashboard-settings/sheet-options.md#matching-keywords)                        | Comma-separated set of keywords as alternative matching options to help users match column names automatically.                                                                                             |
| [type](../dashboard-settings/sheet-options.md#column-type)                                            | It specifies the data type of the incoming data. Possible values are: **text**, **number**, **email**, **date**, **boolean**, **regex**, **ip**, **url**, **credit\_card**, **phone\_number** and **list**. |
| validators                                                                                            | The validation rules for the data based on the column type. Validator options are mentioned below.                                                                                                          |
| [required](../dashboard-settings/sheet-options.md#required)                                           | It indicates whether a column is mandatory.                                                                                                                                                                 |

#### Validator options

| Column Type   | Validators                                                                        | Example                                                                                                                                                                                                                                                                                         |
| ------------- | --------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| text          | <ol><li><strong>min_length</strong></li><li><strong>max_length</strong></li></ol> | <p>"min_length": 2,</p><p>"max_length": 50</p>                                                                                                                                                                                                                                                  |
| number        | <ol><li><strong>min_value</strong></li><li><strong>max_value</strong></li></ol>   | <p>"min_value": -2,</p><p>"max_value": 100</p>                                                                                                                                                                                                                                                  |
| email         | -                                                                                 |                                                                                                                                                                                                                                                                                                 |
| date          | <ol><li><strong>format</strong></li></ol>                                         | "format": “MM/DD/YYYY”                                                                                                                                                                                                                                                                          |
| boolean       | -                                                                                 |                                                                                                                                                                                                                                                                                                 |
| regex         | <ol><li><strong>expression</strong></li></ol>                                     | <p>"expression": "^[\\w-\\.]+@([\\w-]+\\.)+[\\w-]{2,4}$"</p><p></p><p><em>Note: The special characters in the expression need to be escaped. You may use a tool like</em> <a href="https://www.freeformatter.com/javascript-escape.html#ad-output"><em>this</em> </a><em>for escaping.</em></p> |
| ip            | <ol><li><strong>version</strong></li></ol>                                        | "version": “ipv4”                                                                                                                                                                                                                                                                               |
| url           | -                                                                                 |                                                                                                                                                                                                                                                                                                 |
| credit\_card  | -                                                                                 |                                                                                                                                                                                                                                                                                                 |
| phone\_number | -                                                                                 |                                                                                                                                                                                                                                                                                                 |
| list          | <ol><li><strong>values</strong></li><li><strong>case_sensitive</strong></li></ol> | <p>"values": [</p><p>{"value": "m", "display_label": "male"},</p><p>{"value": "f", "display_label": "female"}, </p><p>],</p><p>"case_sensitive": false</p>                                                                                                                                      |

### **Receiving Dynamic Data**

The data from the dynamic columns is available in the data destinations along with the data from the regular columns. Currently, **** dynamic columns are supported by the following destinations only:

1. [API/Webhook](../destinations/#webhook)
2. [Amazon S3](../destinations/#amazon-s3)

#### API/Webhook Data Destination

In the API response JSON object, the dynamic data will be displayed inside the **\_dynamic\_data** object as shown below. The **\_dynamic\_data** object will be visible only if the dynamic columns are configured for the import. In the example below check lines 12 and 31.

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
          "_dynamic_data":{
		"qualification": "MBA",
		"experience": "3"
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
           "_dynamic_data":{
		"qualification": "MA",
		"experience": "6"
           }
        },
    "custom_fields": {
      "user_id": "1002"
    }
  },
]

```

#### S3 Data Destination

In the AWS S3 file store, the dynamic columns will be added as new columns in the uploaded file.

****
