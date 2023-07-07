---
description: Validate data with custom Javascript functions.
---

# Validation Functions

{% hint style="info" %}
coming soon
{% endhint %}

If the validations you require are not covered with the in-built [data type validations](../dashboard-settings/validations.md) in CSVbox then you can code your own custom validation functions in Javascript.

There are two types of Validation Functions: 1. Row Functions 2. Column Functions.

**Row Functions** run validation on each row of data and return an error message (if any) for the user. These functions run at the beginning of the "validate" step and then also when a row data is updated during the "validate" step. An example use case for Row Function is if you want to mark a cell as "mandatory" based on a specific value in another cell in the same row.

**Column Functions** run validation on a set of selected columns when the user clicks the Submit button on the "validate" step. These are best used in cases where entire column data is required for validation. For example, say you want to find duplicate entries in a column. You could grab all the values in the column, find duplicate values, and display the message to the user.

<figure><img src="../.gitbook/assets/Validation Functions.svg" alt=""><figcaption><p>Validation Functions</p></figcaption></figure>

## Row Functions

### Adding Row Functions

* Go to the edit sheet page > **Columns** tab > Click **Add Functions** button.
* Add **Function Name**.
* Select **Row** under Function Type.
* Provide **Javascript** code.
* Click **Save**.

<figure><img src="../.gitbook/assets/row function.jpg" alt=""><figcaption><p>Adding Row Functions</p></figcaption></figure>

### Example Row Functions

{% tabs %}
{% tab title="Dependent Columns" %}
Column 2 is mandatory only if column 1 is not null.

```javascript
//check if Contribution is not Null AND then Currency is Null
if(csvbox.row["Contribution"] != null && csvbox.row["Currency"] == null)
{
  //error message
  let err = [
  {   
    "column": "Currency",
    "message": "Please select a value."
  }];    
  return err;  
}
else
{   
  return  null;
}
```
{% endtab %}
{% endtabs %}

### Variables in the Row Function

You have access to data variables included in the **`csvbox`** object. The following data is available:

#### `csvbox.row`

It contains row data. Each cell in the row can be accessed by providing the column name. Examples:

```javascript
csvbox.row["first_name"]
csvbox.row["order_id"]
csvbox.row["price"]
```

{% hint style="warning" %}
The column name must exist on the sheet or an error will be thrown.
{% endhint %}

#### `csvbox.user`

It contains the [custom user attributes](../getting-started/2.-install-code.md#referencing-the-user) defined while initializing the importer. Examples:

```javascript
csvbox.user["user_id"]
csvbox.user["team_id"]
csvbox.user["isAuthenticated"]
```

#### `csvbox.import`

This refers to the current import-specific data. The following data is available:

```javascript
csvbox.import["sheet_id"]
csvbox.import["sheet_name"]
csvbox.import["original_filename"]
csvbox.import["import_start_time"]
csvbox.import["destination_type"]
csvbox.import["total_rows"]
csvbox.import["row_number"] //current row number starting with 1
```

{% hint style="info" %}
&#x20;_**console.log(csvbox);**_&#x20;

With this statement, you can print all the available variables in the debugging console,
{% endhint %}

### Error Response JSON Format for Row Functions

CSVbox will expect the Row Function to return an array of errors. Each error should specify the `column` the error appeared in, and a `message` to be displayed in the UI.

#### JSON Response Schema

<table><thead><tr><th width="132.33333333333331">Parameter</th><th width="93">Type</th><th>Description</th></tr></thead><tbody><tr><td>column</td><td>string</td><td>The <a href="https://help.csvbox.io/dashboard-settings/sheet-options#column-name">column name </a>of the error. It is case sensitive.</td></tr><tr><td>message</td><td>string</td><td>The message that is to be displayed to the user on the validation screen of the importer.</td></tr></tbody></table>

#### Example Row Function JSON Response

```json
[
  {
    "column": "employee_id",
    "message": "Invalid Emp ID"
  },
  {   
    "column": "dept",
    "message": "Department does not exist"
  },
  {   
    "column": "employee_name",
    "message": "Employee's name has changed"
  }
]
```

## Column Functions

### Adding Column Functions

* Go to the edit sheet page > **Columns** tab > Click **Add Functions** button.
* Add **Function Name**.
* Select **Column** under Function Type.
* Add the Columns you need in the function.
* Provide **Javascript** code.
* Attach **Dependent** libraries (optional).
* Click **Save**.

<figure><img src="../.gitbook/assets/column function add.png" alt=""><figcaption><p>Adding Column Functions</p></figcaption></figure>

### Example Column Functions

{% tabs %}
{% tab title="Finding Duplicates" %}
Check if a column has duplicate entries.

```javascript
var duplicates = [];

csvbox.column["Email"].filter(function(yourArray, index) {
 if(yourArray == 2){
   duplicates.push({
    "row_id": index,
    "column": "Email",
    "message": "Duplicate entry."
  });
 }
});

return duplicates;
```
{% endtab %}
{% endtabs %}

### Dependencies

In the Column Function Javascript snippet, you can utilize an external library that is hosted via a CDN. You can also call any external API endpoint to fetch real-time data. Simply add the library script tag and/or any custom scripts to the 'Dependencies' section and start using it in the main Javascript snippet.

### Variables in the Column Function

You have access to data variables included in the **`csvbox`** object. The following data is available:

#### `csvbox.column`

It contains the entire column data. Each cell in the column can be accessed by providing the column name and the row number. The row number starts with 1. Examples:

```javascript
csvbox.column["first_name"][1]
csvbox.column["order_id"][12]
csvbox.column["price"][10001]
```

{% hint style="warning" %}
Only the selected columns will be available in the Column Function.
{% endhint %}

#### `csvbox.user`

It contains the [custom user attributes](../getting-started/2.-install-code.md#referencing-the-user) defined while initializing the importer. Examples:

```javascript
csvbox.user["user_id"]
csvbox.user["team_id"]
csvbox.user["isAuthenticated"]
```

#### `csvbox.import`

This refers to the current import-specific data. The following data is available:

```javascript
csvbox.import["sheet_id"]
csvbox.import["sheet_name"]
csvbox.import["original_filename"]
csvbox.import["import_start_time"]
csvbox.import["destination_type"]
csvbox.import["total_rows"]
csvbox.import["row_number"] //current row number starting with 1
```

{% hint style="info" %}
&#x20;_**console.log(csvbox);**_&#x20;

With this statement, you can print all the available variables in the debugging console.
{% endhint %}

### Error Response JSON Format for Column Functions

CSVbox will expect the Column Function to return an array of errors. Each error should specify the `row_id`, the `column` the error appeared in, and a `message` to be displayed in the UI.

#### JSON Response Schema for Column Functions

<table><thead><tr><th width="132.33333333333331">Parameter</th><th width="93">Type</th><th>Description</th></tr></thead><tbody><tr><td>row_id</td><td>integer</td><td>The row number of the error. Starts with 1.</td></tr><tr><td>column</td><td>string</td><td>The <a href="https://help.csvbox.io/dashboard-settings/sheet-options#column-name">column name </a>of the error. It is case sensitive.</td></tr><tr><td>message</td><td>string</td><td>The message to be displayed to the user on the validation screen of the importer.</td></tr></tbody></table>

#### Example Column Function JSON Response

```json
[
  {
    "row_id": 1,
    "column": "employee_id",
    "message": "Invalid Emp ID"
  },
  {
    "row_id": 2,
    "column": "dept",
    "message": "Department does not exist"
  },
  {
    "row_id": 3,
    "column": "employee_name",
    "message": "Employee's name has changed"
  }
]
```
