---
description: Bulk edit the dataset before pushing it to your system.
---

# Data Transforms

The **Data Transforms** feature in CSVbox empowers you to modify and manipulate the data before it is uploaded to your app. Using JavaScript, you can apply custom transformations to reshape, sanitize, or enhance your data in real-time. Whether you need to perform simple tasks like capitalizing text or formatting dates, or handle complex business logic, Data Transforms gives you full control to customize your dataset to meet your app's specific needs.

<figure><img src="../.gitbook/assets/Data Transforms.png" alt=""><figcaption><p>Data Trasforms</p></figcaption></figure>

## How it works

When a CSV file is uploaded, CSVbox parses the data and applies your transformation logic row-by-row or column cell-by-cell. The JavaScript function you write defines how each row or field should be transformed. Once the transformation is complete, the modified data is passed to the next stage for validation.\
\
There are two main types of Data Transforms available in CSVbox: **Row Transforms** and **Column Transforms**.

* **Row Transforms** apply transformation logic row-by-row, processing each row individually from top to bottom. These are especially useful when the transformation of one cell depends on the values of other cells within the same row. For instance, if you need to combine data from multiple cells into a single cell, or if a calculation requires input from different columns within the same row, Row Transforms are ideal. This approach allows you to apply logic dynamically based on relationships within each row of data.
* **Column Transforms** operate on a single column or a set of selected columns, applying transformations to all entries in the specified columns at once. These transforms are most effective when you need to analyze or modify data across the entire column rather than row-by-row. For example, if you're looking to identify duplicate entries in a column and replace each duplicate with a unique identifier, a Column Transform can help by analyzing all values in that column collectively before applying changes. This approach is efficient for transformations that rely on examining the column as a whole, such as sorting, aggregating, or deduplication tasks.

Using these two transformation types, you can precisely target and manipulate your data based on your application's requirements, whether you need to perform intra-row calculations or make adjustments to column-wide data sets.

{% hint style="warning" %}
Selecting **Column Transforms** can impact importer performance, as the entire column dataset is loaded into memory for processing. This means that, especially with large datasets, using Column Transforms may slow down the import process. For optimal performance, consider using Row Transforms for operations that do not require analyzing the entire column, reserving Column Transforms for cases where column-wide data processing is essential, such as deduplication or aggregation tasks.
{% endhint %}

## Row Transforms <a href="#adding-virtual-columns" id="adding-virtual-columns"></a>

### Adding Row Data Transforms <a href="#adding-virtual-columns" id="adding-virtual-columns"></a>

1. Go to the edit sheet page > **Data Transforms** tab >  Click **Add Transforms** button.
2. Add Transform **Name**.
3. Select **Transform Type** as **Row**.
4. Provide **Javascript** code.
5. Attach **Dependent** Libraries (optional).
6. Click **Save**.

### Row Transform Examples

{% tabs %}
{% tab title="Append text " %}
Append a constant to the cell value.

{% code overflow="wrap" %}
```javascript
csvbox.row["serial_number"] = csvbox.row["serial_number"] + '_' + csvbox.user["user_id"];
  
  return csvbox;
```
{% endcode %}
{% endtab %}

{% tab title="Normalize dates" %}
Normalize date value into US format.

{% code overflow="wrap" %}
```javascript
function normalizeToUSFormat(dateString) {
  // Create a new Date object by parsing the input date string
  const date = new Date(dateString);

  // Check if the Date object is valid
  if (isNaN(date.getTime())) {  
    console.log("Invalid date format.");
    return dateString;
  }

  // Get month, day, and year
  const month = String(date.getMonth() + 1).padStart(2, '0');
  const day = String(date.getDate()).padStart(2, '0');
  const year = date.getFullYear();

  // Return the date in MM/DD/YYYY format
  return `${month}/${day}/${year}`;
}

// Example usage
  csvbox.row["date_of_birth"] = normalizeToUSFormat(csvbox.row["date_of_birth"]);
 
  return csvbox;
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Variables in the Row Transform

You have access to data variables included in the **`csvbox`** object. The following data is available:

#### `csvbox.row`

It contains row data. Each cell in the row can be accessed by providing the column name. Examples:

```javascript
csvbox.row["first_name"]
csvbox.row["order_id"]
csvbox.row["price"]
```

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

if(column.isUnmapped) {
   
   // this is a unmapped column
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

With this statement, you can print all the available variables in the debugging console.
{% endhint %}

## Column Transforms <a href="#adding-virtual-columns" id="adding-virtual-columns"></a>

### Adding Column Data Transforms <a href="#adding-virtual-columns" id="adding-virtual-columns"></a>

1. Go to the edit sheet page > **Data Transforms** tab >  Click **Add Transforms** button.
2. Add Transform **Name**.
3. Add the **Columns you need for** the transform.
4. Provide **Javascript** code.
5. Attach **Dependent** Libraries (optional).
6. Click **Save**.

### Column Transform Examples

{% tabs %}
{% tab title="Example 1" %}
Capitalizing Text Fields:

```javascript
//loop and capitalize each value

for(let i=0; i < csvbox.column["first_name"].length; i++)
{
    csvbox.column["first_name"][i] = csvbox.column["first_name"][i].toUpperCase();
}

// return the updated data set
return csvbox;
```
{% endtab %}
{% endtabs %}

### Variables in the Column Transform

You have access to data variables included in the **`csvbox`** object. The following data is available:

#### `csvbox.column`

It contains the entire column data. Each cell in the column can be accessed by providing the column name and the row number. The row number starts with 1. Examples:

```javascript
csvbox.column["first_name"][1]
csvbox.column["order_id"][12]
csvbox.column["price"][10001]
```

{% hint style="warning" %}
Only the selected columns will be available in the Transform javascript.
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

if(column.isUnmapped) {
   
   // this is a unmapped column
   // code  
   
}
```

#### _**console.log(csvbox);**_&#x20;

{% hint style="info" %}
With this statement, you can print all the available variables in the debugging console.
{% endhint %}

### Dependencies

In the Transforms Javascript snippet, you can utilize an external library hosted via a CDN. You can also call any external API endpoint to fetch real-time data. Add the library script tag and/or any custom scripts to the 'Dependencies' section and use it in the main Javascript snippet.

## **Execution Time**

Every Data Transform can now run at **one of two stages** in the import pipeline:

* **Pre Data Validation** (default)
* **Post Data Validation**

This gives you full control over _when_ your transform runs during the import workflow.

#### **1. Pre-Validation Data Transform**

Runs **immediately after column mapping** and **before Data Validation**.

Use this for:

* Cleaning or normalizing user input
* Converting formats (dates, numbers, booleans)
* Combining or splitting fields
* Setting defaults
* Preparing data that validators depend on

Example:\
Convert a string such as `" 23.4500 "` into a clean numeric value before your validation rules run.

#### **2. Post-Validation Data Transform**

Runs **only if there are no validation errors**, and just before pushing data to the final destination.

Use this for:

* Final formatting
* Destination-specific transformations
* Generating or enriching fields **only when the row is already valid**
* Preparing computed values needed only for storage

Example:\
If you need to generate a `slug`, `UUID`, or apply pricing markup _after_ all validations pass.

#### **Where to Configure Execution Time**

When creating or editing a Data Transform:

1. Open **Sheet Settings → Data Transforms**.
2. Select your existing transform or create a new one.
3. Choose the desired **Execution Time**:
   * **Pre Data Validation**
   * **Post Data Validation**
4. Save your changes.

## Key Features

* **JavaScript-Powered**: Write custom JavaScript code to perform operations on your data. With access to native JavaScript methods, you can implement transformations ranging from basic modifications to complex logic.
* **Real-Time Execution**: Your transformations are applied as the file is uploaded, ensuring that the data is processed and adjusted before it enters your app.
* **Versatile**: Use Data Transforms to handle a wide range of operations, such as:
  * Modifying string data (e.g., capitalizing text, trimming spaces)
  * Formatting dates
  * Performing calculations, such as currency conversions
  * Validating and cleaning up data
  * Applying conditional logic to data fields
* **Error Handling**: You can include custom error handling in your JavaScript to manage issues gracefully without disrupting the upload process.

## Best Practices

* **Error Handling**: Incorporate error-handling logic into your JavaScript code to avoid disruptions in the upload process due to malformed data.
* **Optimize Performance**: Keep your transformation code efficient, especially when working with large datasets, to ensure smooth uploads.

## Conclusion

With Data Transforms, you have the flexibility to clean, format, and manipulate data in real-time as it's uploaded through CSVbox. Whether you need to perform simple formatting tasks or implement complex business logic, Data Transforms can help you streamline your data handling processes and ensure that your datasets are always consistent and accurate.

