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

#### 2. The user submits the spreadsheet as usual.

#### 3. The importer pushes the data to the API endpoint configured by you.

#### 4. Your app processes the data.

1. Case 1: Validation success, no errors found. Your API returns a **`200`** response code. The success screen is displayed to the user.
2. Case 2: Validation failed, one or more errors found. Your API returns **`211`** response code along with data on the validation errors.

#### 5. Validation Fail Screen is displayed to the user.

#### 6. Users can view the validation errors.

#### 7. After fixing the errors, the users re-submit the data.



### Validation Error JSON Response Format

```
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
