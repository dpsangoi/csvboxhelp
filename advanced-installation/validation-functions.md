---
description: Validate data with custom Javascript functions.
---

# Validation Functions

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
Column 5 is mandatory only if the column 4 is not null.

```javascript
//replace "col4" and "col5" with actual column names

if(csvbox.row["col4"] != "" && csvbox.row["col5"] == "") {
  let err = [
  {   
    "column": "col5",
    "message": "Column 5 is mandatory if Column 4 is not empty"
  }];    
  return err;  
}
```
{% endtab %}

{% tab title="Mandatory Column Combination" %}
Either col 2 or col 3 needs to have data.

```javascript
//replace "col2" and "col3" with actual column names

if(csvbox.row["col2"] == "" && csvbox.row["col3"] == ""){
  let err = [
    {   
      "column": "col2",
      "message": "Columns 2 OR 3 needs to have data"
    },
    {
      "column": "col3",
      "message": "Columns 2 OR 3 needs to have data"
    }
  ];    
  return err;
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

#### `csvbox.columns`

This object contains the column metadata (name, type).

```javascript
//Example usage
let column = csvbox.columns['birthdate'];

if(column.type == 'date') {

   // code  
   
}

if(column.isDynamic) {
   
   // this is a dynamic column
   // code  
   
}
```

#### `csvbox.environment`

It contains the [environment variables](environment-variables.md) that are passed during importer initialization.

```javascript
// Example Usage
if(csvbox.environment["user_id"] && csvbox.environment["user_id"] == "abc123") {
 
 // code
 
}
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

{% hint style="info" %}
You can also enter the [Dynamic Column](dynamic-columns.md) names to access them in the Validation Functions.
{% endhint %}

### Example Column Functions

{% tabs %}
{% tab title="Detect Duplicates" %}
Check if a column has duplicate entries.

```javascript
//replace "col4" with actual column name

function findRepeatingIndices(arr) {
  const repeatingIndices = {};
  
  for (let i = 0; i < arr.length; i++) {
    const element = arr[i];
    if (repeatingIndices[element] === undefined) {
      repeatingIndices[element] = [i];
    } else {
      repeatingIndices[element].push(i);
    }
  }
  
  const result = [];
  
  for (const key in repeatingIndices) {
    if (repeatingIndices[key].length > 1) {
      result.push(...repeatingIndices[key]);
    }
  }
  
  return result;
}

const arr = csvbox.column["col4"];
const repeatingIndices = findRepeatingIndices(arr);

let errs = [];

repeatingIndices.forEach(index => {
  errs.push({
    "row_id": (index + 1),
    "column": "col4",
    "message": "Duplicate entry."
  });
});

return errs;
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

#### `csvbox.environment`

It contains the [environment variables](environment-variables.md) that are passed during importer initialization.

```javascript
// Example Usage
if(csvbox.environment["user_id"] && csvbox.environment["user_id"] == "abc123") {
 
 // code
 
}
```

#### `csvbox.columns`

This object contains the column metadata (name, type).

```javascript
//Example usage
let column = csvbox.columns['birthdate'];

if(column.type == 'date') {

   // code  
   
}

if(column.isDynamic) {
   
   // this is a dynamic column
   // code  
   
}
```

{% hint style="info" %}
&#x20;_**console.log(csvbox);**_&#x20;

With this statement, you can print all the available variables in the debugging console.
{% endhint %}

### Error Response JSON Format for Column Functions

CSVbox will expect the Column Function to return an array of errors. Each error should specify the `row_id`, the `column` the error appeared in, and a `message` to be displayed in the UI.

#### JSON Response Schema for Column Functions

<table><thead><tr><th width="40">Parameter</th><th width="93">Type</th><th>Description</th></tr></thead><tbody><tr><td>row_id</td><td>integer</td><td>The row number of the error. Starts with 1.</td></tr><tr><td>column</td><td>string</td><td>The <a href="https://help.csvbox.io/dashboard-settings/sheet-options#column-name">column name </a>of the error. It is case sensitive.</td></tr><tr><td>message</td><td>string</td><td>The message to be displayed to the user on the validation screen of the importer.</td></tr></tbody></table>

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
