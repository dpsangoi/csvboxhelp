---
description: Bulk edit the dataset before pushing it to your system.
---

# Data Transforms

{% hint style="warning" %}
Coming Soon
{% endhint %}

The **Data Transforms** feature in CSVbox empowers you to modify and manipulate the data before it is uploaded to your app. Using JavaScript, you can apply custom transformations to reshape, sanitize, or enhance your data in real-time. Whether you need to perform simple tasks like capitalizing text or formatting dates, or handle complex business logic, Data Transforms gives you full control to customize your dataset to meet your app's specific needs.

<figure><img src="../.gitbook/assets/Data Transform.png" alt=""><figcaption><p>Data Trasforms</p></figcaption></figure>

## How it works

When a CSV file is uploaded, CSVbox parses the data and applies your transformation logic row-by-row or cell-by-cell. The JavaScript function you write defines how each row or field should be transformed. Once the transformation is complete, the modified data is passed to the next stage for validation.

### Adding Data Transforms <a href="#adding-virtual-columns" id="adding-virtual-columns"></a>

1. Go to the edit sheet page > **Data Transforms** tab >  Click **Add Transforms** button.
2. Add Transform **Name**.
3. Add the **Columns you need for** the transform.
4. Provide **Javascript** code.
5. Attach **Dependent** Libraries (optional).
6. Click **Save**.

### Examples

{% tabs %}
{% tab title="Example 1" %}
Capitalizing Text Fields:

```javascript
//loop and capitalize each value

for(let i=0; i < csvbox.column["first_name"].length; i++)
{
    csvbox.column["first_name"][i] = csvbox.column["first_name"].toUpperCase();
}
```
{% endtab %}
{% endtabs %}

### Dependencies

In the Trasnforms Javascript snippet, you can utilize an external library that is hosted via a CDN. You can also call any external API endpoint to fetch real-time data. Simply add the library script tag and/or any custom scripts to the 'Dependencies' section and start using it in the main Javascript snippet.

### Variables in the Transform

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
csvbox.import["row_number"] //current row number starting with 1
```

{% hint style="info" %}
&#x20;_**console.log(csvbox);**_&#x20;

With this statement, you can print all the available variables in the debugging console.
{% endhint %}

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

* **Data Validation**: Use Data Transforms to validate incoming data and correct common issues, like missing or incorrectly formatted fields.
* **Error Handling**: Incorporate error-handling logic into your JavaScript code to avoid disruptions in the upload process due to malformed data.
* **Optimize Performance**: Keep your transformation code efficient, especially when working with large datasets, to ensure smooth uploads.

## Conclusion

With Data Transforms, you have the flexibility to clean, format, and manipulate data in real-time as it's uploaded through CSVbox. Whether you need to perform simple formatting tasks or implement complex business logic, Data Transforms can help you streamline your data handling processes and ensure that your datasets are always consistent and accurate.

