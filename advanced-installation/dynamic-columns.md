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
      [imported]="imported.bind(this)">
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
          "default_value": "Masters",  
          "position": 2,
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
          "position": 4,
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
          "default_value": "Masters",
          "position": 2,
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
          "position": 4,
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
     column_name: "qualification",
     display_label: "Highest Qualification",
     info_hint: "What is your highest educational degree",
     matching_keywords: "degree, education",
     type: "text",
     validators: 
     {            
       min_length: 2,
       max_length: 50
     },
     default_value: "Masters",  
     position: 2,
     required: true
  },
  {
     column_name: "experience",
     display_label: "Work Experience",
     info_hint: "Years of work experience",
     matching_keywords: "",
     type: "number",
     validators: 
     {            
       min_value: 0,
       max_value: 100
     },
     position: 4,
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
  ];
```
{% endtab %}

{% tab title="Vuejs" %}
```javascript
 dynamicColumns: [
  {
   column_name: "qualification",
   display_label: "Highest Qualification",
   info_hint: "What is your highest educational degree",
   matching_keywords: "degree, education",
   type: "text",
   validators: 
   {            
     min_length: 2,
     max_length: 50
   },
   default_value: "Masters",
   position: 2,
   required: true
},
{
   column_name: "experience",
   display_label: "Work Experience",
   info_hint: "Years of work experience",
   matching_keywords: "",
   type: "number",
   validators: 
   {            
     min_value: 0,
     max_value: 100
   },
   position: 4,
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

<table><thead><tr><th width="321.0208971718002">Key</th><th>Description</th></tr></thead><tbody><tr><td><a href="../dashboard-settings/sheet-options.md#column-name">column_name</a> <mark style="color:red;">*</mark></td><td>It is the column name that will be pushed to the data destination.</td></tr><tr><td><a href="../dashboard-settings/sheet-options.md#display-label">display_label</a></td><td>The user-friendly column label that the users will see in the importer.</td></tr><tr><td><a href="../dashboard-settings/sheet-options.md#info-hint">info_hint</a></td><td>Info Hints are help tooltips that will get displayed when the users hover the mouse over the Display Label (or click it) in the importer.</td></tr><tr><td><a href="../dashboard-settings/sheet-options.md#matching-keywords">matching_keywords</a></td><td>Comma-separated set of keywords as alternative matching options to help users match column names automatically. </td></tr><tr><td><a href="../dashboard-settings/sheet-options.md#column-type">type</a></td><td>It specifies the data type of the incoming data. Possible values are: <strong>text</strong>, <strong>number</strong>, <strong>email</strong>, <strong>date</strong>, <strong>boolean</strong>, <strong>regex</strong>, <strong>ip</strong>, <strong>url</strong>, <strong>credit_card</strong>, <strong>phone_number, currency, list, dependent_list, dynamic_list, dependent_dynamic_list, multiselect_list,</strong> and <strong>multiselect_dynamic_list.</strong></td></tr><tr><td><a href="dynamic-columns.md#validator-options">validators</a></td><td>The validation rules for the data based on the column type. Validator options are mentioned below.</td></tr><tr><td><a href="../dashboard-settings/sheet-options.md#default-value">default_value</a></td><td>A default filler value for the column in case the incoming data is blank.</td></tr><tr><td><a href="../dashboard-settings/sheet-options.md#required">required</a></td><td>It indicates whether a column is mandatory.</td></tr><tr><td><a href="dynamic-columns.md#column-position">position</a></td><td>It defines the display index of the column. Starts from 1.</td></tr><tr><td><a href="../dashboard-settings/sheet-options.md#read-only">read_only</a></td><td>If configured to <strong>true</strong> then the users will not be able to edit the data of this column. The default value is <strong>false</strong>.</td></tr></tbody></table>

#### Validator options

<table><thead><tr><th width="150">Column Type</th><th width="150">Validators</th><th>Example</th></tr></thead><tbody><tr><td>text</td><td><ol><li><strong>min_length</strong></li><li><strong>max_length</strong></li></ol></td><td><p>"min_length": 2,</p><p>"max_length": 50</p></td></tr><tr><td>number</td><td><ol><li><strong>min_value</strong></li><li><strong>max_value</strong></li><li><strong>number_type</strong><br><strong>-</strong> Valid values: "any", "integer"<br>- Default: "any" </li><li><strong>allow_commas</strong><br><strong>-</strong> Valid values: true, false<br>- Default: false</li></ol></td><td><p>"min_value": -2,</p><p>"max_value": 100,<br>"number_type": "integer",<br>"allow_commas": true</p></td></tr><tr><td>email</td><td>-</td><td></td></tr><tr><td>date</td><td><ol><li><strong>format</strong></li></ol></td><td>"format": ["MM/DD/YYYY", "MM.DD.YYYY", "MM-DD-YYYY"]</td></tr><tr><td>boolean</td><td>-</td><td></td></tr><tr><td>regex</td><td><ol><li><strong>expression</strong></li></ol></td><td><p>"expression": "^[\\w-\\.]+@([\\w-]+\\.)+[\\w-]{2,4}$"</p><p></p><p><em>Note: The special characters in the expression need to be escaped. You may use a tool like</em> <a href="https://www.freeformatter.com/javascript-escape.html#ad-output"><em>this</em> </a><em>for escaping.</em></p></td></tr><tr><td>ip</td><td><ol><li><strong>version</strong></li></ol></td><td>"version": “ipv4”</td></tr><tr><td>url</td><td>-</td><td></td></tr><tr><td>credit_card</td><td>-</td><td></td></tr><tr><td>phone_number</td><td><ol><li><strong>country_code</strong></li></ol></td><td>"country_code": "de"</td></tr><tr><td>currency</td><td><ol><li><strong>symbol</strong></li><li><strong>require_symbol</strong></li><li><strong>allow_space_after_symbol</strong></li><li><strong>symbol_after_digits</strong></li><li><strong>allow_negatives</strong></li><li><strong>parens_for_negatives</strong></li><li><strong>negative_sign_before_digits</strong></li><li><strong>negative_sign_after_digits</strong></li><li><strong>thousands_separato</strong></li><li><strong>decimal_separator</strong></li><li><strong>allow_decimal</strong></li><li><strong>require_decimal</strong></li><li><strong>digits_after_decima</strong></li><li><strong>allow_space_after_digits</strong></li></ol><p><strong>Note:</strong> The array <code>digits_after_decimal</code> is filled with the exact number of digits allowed not a range, for example a range 1 to 3 will be given as [1, 2, 3].</p></td><td><p>"symbol": "$", </p><p>"require_symbol": false,</p><p>"allow_space_after_symbol": false, "symbol_after_digits": false, "allow_negatives": true, "parens_for_negatives": false, "negative_sign_before_digits": false,</p><p>"negative_sign_after_digits": false,</p><p>"thousands_separator": ",", "decimal_separator": ".", "allow_decimal": true, "require_decimal": false, "digits_after_decimal": 2, "allow_space_after_digits": false</p></td></tr><tr><td>list</td><td><ol><li><p><strong>values</strong></p><ul><li><strong>value</strong></li><li><strong>display_label</strong> (optional)</li><li><p><strong>dependents</strong> (optional)</p><ul><li><strong>value</strong></li><li><strong>display_label</strong></li></ul></li></ul></li><li><strong>case_sensitive</strong></li><li><strong>other_values</strong> (Optional. Default is false)</li></ol></td><td><p>"values": [ </p><p>{"value": "USA", "display_label": "USA", "dependents": [ {"value": "ny", "display_label": "New York"}, {"value": "ch", "display_label": "Chicago"}, {"value": "se", "display_label": "Seatle"}, {"value": "mi", "display_label": "Miami"} ]}, {"value": "Canada", "display_label": "Canada", "dependents": [ {"value": "to", "display_label": "Toronto"}, {"value": "va", "display_label": "Vancouver"}<br>]}</p><p>],</p><p>"case_sensitive": false,<br>"other_values": false</p></td></tr><tr><td>dependent_list</td><td><ol><li><strong>primary_column</strong></li></ol></td><td>"primary_column": "countries"</td></tr><tr><td>dynamic_list</td><td><ol><li><strong>source_url</strong></li><li><strong>request_method</strong></li><li><strong>request_headers</strong></li><li><strong>custom_user_attributes</strong> (Optional. Default is true)</li><li><strong>other_values</strong> (Optional. Default is false)</li></ol></td><td><p>"source_url": "https://api.myapp.com/countries",<br>"request_method": "POST",</p><p>"request_headers": [</p><p>{"key": "Content-Type", "value": "application/json"},</p><p>{"key": "X-Access-Token", "value": "71ab1d73a4d1319b260e9a0sdbdbc1c"}</p><p>],<br>custom_user_attributes: true,<br>"other_values": false</p></td></tr><tr><td>dependent_dynamic_list</td><td><ol><li><strong>primary_column</strong></li></ol></td><td>"primary_column": "countries"</td></tr><tr><td>multiselect_list</td><td><ol><li><strong>values</strong></li><li><strong>delimiter</strong> (Optional. Default is comma ",")</li><li><strong>case_sensitive</strong></li><li><strong>other_values</strong> (Optional. Default is false)</li></ol></td><td><p>"values": ["Red", "Green", "Blue"],</p><p>"delimiter": ".",<br>"case_sensitive": false,<br>"other_values": false</p></td></tr><tr><td>multiselect_dynamic_list</td><td><ol><li><strong>source_url</strong></li><li><strong>request_method</strong></li><li><strong>request_headers</strong></li><li><strong>delimiter</strong> (Optional. Default is comma ",")</li><li><strong>other_values</strong> (Optional. Default is false)</li></ol></td><td><p>"source_url": "https://api.myapp.com/colors",<br>"request_method": "POST",</p><p>"request_headers": [</p><p>{"key": "Content-Type", "value": "application/json"},</p><p>{"key": "X-Access-Token", "value": "71ab1d73a4d1319b260e9a0sdbdbc1c"}</p><p>],<br>"delimiter": ".",<br>"other_values": false</p></td></tr></tbody></table>

#### **Column Position**

In general, the dynamic columns are displayed only after the regular columns.

The `position`parameter helps to re-order the position of the dynamic columns and get them displayed before or in between the regular columns.&#x20;

The `position` value starts from 1 indicating the first position in the final column list. It is an optional parameter while defining the dynamic columns.

### **Receiving Dynamic Data**

The data from the dynamic columns is available in the data destinations along with the data from the regular columns. Currently, dynamic columns are supported by the following destinations only:

1. [None](../destinations/#none)
2. [API/Webhook](../destinations/#webhook)
3. [Amazon S3](../destinations/#amazon-s3)

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

