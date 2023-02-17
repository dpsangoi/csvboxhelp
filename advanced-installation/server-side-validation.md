---
description: Validate data at your server, report back errors for correction.
---

# Server Side Validation

{% hint style="warning" %}
coming soon
{% endhint %}

Consider a case where you want to validate the incoming data against business rules. This could be as simple as verifying if the user ID is found in the database or something more complex that involves complex logic. Here you want the validation to be done at your server end and relay back errors if any. The users can fix the errors and re-submit the data.

### How it Works

<figure><img src="../.gitbook/assets/External Validation (1).svg" alt=""><figcaption><p>Server Side Validation</p></figcaption></figure>

#### 1. Activate Server Side Validation via Sheet Settings.

Go to Edit Sheet > Select Destination Tab > Enable Server Side validation

&#x20;![](<../.gitbook/assets/external validation.png>)

{% hint style="warning" %}
The External Validation option is available only for the API data destination.
{% endhint %}

#### 2. The users upload and submit the spreadsheet.

#### 3. The CSVbox importer pushes the data to the API endpoint configured by you.

The spreadsheet file data will be sent via POST requests with JSON values to the supplied endpoint. The request schema is available [here](https://help.csvbox.io/destinations#sample-json-post-to-your-api).

#### 4. Your app can then processes the data and validate it against the business rules.

Case 1: Validation is successful - no errors found. Your API returns a **`200`** HTTP response code. The success screen is displayed to the user.

Case 2: Validation failed - one or more errors found. Your API returns **`211`** HTTP response code along with the validation errors in JSON format. The error response JSON format is mentioned [here](server-side-validation.md#validation-error-json-response-format).

{% hint style="info" %}
It is mandatory for your API to return **`211`** HTTP response status code to instruct the CSVbox importer that there are one or more server-side validation errors.
{% endhint %}

#### 5. Validation Fail Screen is displayed to the user.

#### 6. Users can view the validation errors.

#### 7. After fixing the errors, the users re-submit the data.



### Validation Error Response JSON Format

CSVbox will expect the API endpoint to return an array of errors. Each error should specify the `row_id`, the `column` the error appeared in, and a `message` to be displayed in the UI.

#### JSON Response Schema

| Parameter | Type    | Description                                                                                          |
| --------- | ------- | ---------------------------------------------------------------------------------------------------- |
| row\_id   | integer | The row number of the error. Starts with 1.                                                          |
| column    | string  | The [column name ](https://help.csvbox.io/dashboard-settings/sheet-options#column-name)of the error. |
| message   | string  | The message to be displayed to the user on the validation screen of the importer.                    |

#### JSON Response Example

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

{% hint style="info" %}
The Server Side Validation is an invite-only beta feature.
{% endhint %}
