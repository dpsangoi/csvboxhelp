---
description: Validate data at your server, report back errors for correction.
---

# Server Side Validation

Consider a case where you want to validate the incoming data against your business rules. This could be as simple as verifying if the user ID is found in the database or something more complex that involves custom logic. Here you want the validation to be done at your server end and relay back errors if any.

With CSVbox you have the option of server-side validation of the submitted data and returning back the errors. Then the users can fix the errors and re-submit the data.

### How it Works

<figure><img src="../.gitbook/assets/External Validation (1).svg" alt=""><figcaption><p>Server Side Validation</p></figcaption></figure>

#### 1. Activate Server Side Validation via Sheet Settings.

Go to Edit Sheet > Select Destination Tab > Enable Server Side Validation

<div align="left"><figure><img src="../.gitbook/assets/server-side button.jpg" alt=""><figcaption><p>Activate Server Side Validation</p></figcaption></figure></div>

{% hint style="warning" %}
The External Validation option is available only for the [API data destination](../destinations/#api-webhook).
{% endhint %}

#### 2. The users upload and submit the spreadsheet.

The users upload the spreadsheet, map columns, verify data, and then submit.

#### 3. The CSVbox importer pushes the data to the API endpoint configured by you.

The importer will send the spreadsheet data via POST requests with JSON values to your API endpoint. The request schema is available [here](https://help.csvbox.io/destinations#sample-json-post-to-your-api).

#### 4. Your app can then processes the data and validate it against the business rules.

Case 1: Validation is successful - no errors found. Your API returns a **`200`** HTTP response code. The success screen is displayed to the user.

<figure><img src="../.gitbook/assets/image (2) (2).png" alt=""><figcaption><p>Success Screen</p></figcaption></figure>

Case 2: Validation failed - one or more errors found. Your API returns **`211`** HTTP response code along with the validation errors in JSON format. The error response JSON format is mentioned [here](server-side-validation.md#validation-error-json-response-format).

{% hint style="info" %}
It is mandatory for your API to return **`211`** HTTP response status code to instruct the CSVbox importer that there are one or more server-side validation errors.
{% endhint %}

{% hint style="warning" %}
To view the results screen be sure to configure the CSVbox Result Page Settings. Go to Sheet Settings > Display > Results Page > Set **Closing the import dialog box** to **Do not close on import complete**

![](<../.gitbook/assets/do not close.jpg>)
{% endhint %}

#### 5. Validation Fail Screen is displayed to the user.

If there are one or more server-side validation errors then the users will see the Fail Screen with a button to view the errors.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption><p>Fail Screen with View Errors Button</p></figcaption></figure>

#### 6. Users can view the validation errors.

Clicking on the Errors button will take the users to the Verify Data screen with all the server-side errors displayed.

<figure><img src="../.gitbook/assets/sleekshot.png" alt=""><figcaption></figcaption></figure>

#### 7. After fixing the errors, the users can re-submit the data.

On re-submitting the data, the process will repeat. The importer will push the data to your API endpoint via POST requests and look for errors in the response.

{% hint style="info" %}
Each re-submit will be treated as a fresh import having a new **`Import_Id`**.
{% endhint %}

To allow the users to re-submit all the rows again (instead of error rows only) select the 'All Rows' option as shown below:

<div align="left"><figure><img src="../.gitbook/assets/ssv.png" alt="" width="326"><figcaption><p>Re-submit All Rows</p></figcaption></figure></div>

### Error Types

CSVBox server-side validation now supports three error types:

* **table** (new): Show high-level/common errors that apply to the entire upload. Renders as a dismissible alert above the grid.
* **row** (new): Show errors that apply to a whole row, not a specific cell. Renders as a red badge on the row number; clicking it opens a pop-up with the message.
* **cell** (existing): The previous behavior; highlights an individual cell with an inline message. In this documentation we now refer to these as “cell errors.”

**UI behavior**

* **Table errors** appear in a prominent alert banner above the grid until dismissed or replaced by a subsequent validation run.
* **Row errors** highlight the row index with a red badge. Clicking the badge opens a pop-over containing your `message` and a Close button.
* **Cell errors** continue to highlight individual cells with inline messages as before.

<figure><img src="../.gitbook/assets/sse errors.png" alt=""><figcaption></figcaption></figure>

\
**When to use each type**

* **table**: Missing required columns, inconsistent file format, duplicate file, or any condition that makes the whole dataset invalid.
* **row**: Cross-field checks within the same row (e.g., “End Date must be after Start Date”), referential issues that aren’t tied to a single column, or row-level business rules.
* **cell**: Format/length/pattern errors, disallowed values, or any validation that is clearly attributable to one column.

### Response Format JSON

CSVbox will expect the validation endpoint to return an array of error objects.

**Fields**

<table><thead><tr><th width="132.33333333333331">Parameter</th><th width="93">Type</th><th>Description</th></tr></thead><tbody><tr><td>type</td><td>string</td><td><code>"table" | "row" | "cell"</code>. Defaults to <code>"cell"</code>. (Optional)</td></tr><tr><td>row_id</td><td>integer</td><td>The row number of the error. Starts with 1. (required for <code>row</code> and <code>cell</code>)</td></tr><tr><td>column</td><td>string</td><td>The CSVbox <a href="https://help.csvbox.io/dashboard-settings/sheet-options#column-name">column name </a> (i.e., the field you mapped), not the user’s original header.. It is case sensitive. (required for <code>cell</code>)</td></tr><tr><td>message</td><td>string</td><td>String to display to the user. Basic HTML line breaks like <code>&#x3C;br></code> are supported.</td></tr></tbody></table>

#### Example payload

```json
[
  {
    "type": "table",
    "message": "Missing address.<br>Missing department.<br>Resubmit."
  },
  {
    "type": "cell",
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
  },
  {
    "type": "row",
    "row_id": 3,
    "message": "Cannot add this row"
  }
]
```

You can mix **table**, **row**, and **cell** errors in the same response.

### Additional Attributes in the Client Data Object

When **Server-Side Validation (SSV)** is enabled, the data object received at the client (after submission) includes additional attributes to help you handle validation states programmatically.

<table><thead><tr><th width="197.20001220703125">Attribute</th><th>Description</th></tr></thead><tbody><tr><td><strong>ssv_enabled</strong></td><td>Indicates whether Server-Side Validation is active for the current sheet.</td></tr><tr><td><strong>ssv_fail</strong></td><td>Set to <strong>true</strong> only when the server returns a <strong>211 response code</strong>, meaning the import failed due to SSV errors.</td></tr><tr><td><strong>ssv_row_fail</strong></td><td>Number of rows that failed during server-side validation.</td></tr><tr><td><strong>ssv_table_error</strong></td><td>True if a table-level validation error was returned by the server.</td></tr></tbody></table>

These attributes allow you to detect and respond to validation outcomes—such as displaying custom messages, logging failed rows, or triggering retry logic—directly from your client application.

**Example Response Object**

```json
{
  destination_type: "apiwebhook",
  env_name: "default", 
  import_description: "",
  import_endtime: 1762774689,
  import_id: 12859532,
  import_starttime: 1762774686,
  import_status: "success",
  original_filename: "emp.csv",
  raw_file: "https://app.csvbox.io/download-rawfile/1-FIIeyMflK9OvAX1EMjncCTlMasuG5Vil35LQNHAQ",
  row_count: 5,
  row_fail: 0,
  row_success: 5,
  sheet_id: 1058,
  sheet_name: "Customer onboarding",
  ssv_enabled: 1,
  ssv_fail: 1,
  ssv_row_fail: 3,
  ssv_table_error: 1
}

```

In this example:

* **ssv\_enabled** confirms that SSV is active.
* **ssv\_fail** is `true` because the server responded with a **211** code.
* **ssv\_row\_fail** specifies the number of failed rows.
* **ssv\_table\_error** is `false`, meaning the issue was at the row level rather than a table-level error.

