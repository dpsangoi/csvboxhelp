---
description: Validate data with custom Javascript functions.
---

# Validation Functions

{% hint style="info" %}
coming soon
{% endhint %}

If the validations you require are not covered with the in-built [data type validations](../dashboard-settings/validations.md) in CSVbox then you can code your own custom validation functions.

There are two types of Validation Functions: 1. Row Functions 2. Column Functions.

**Row Functions** run validation on each row of data and return an error message (if any) for the user. These functions run at the beginning of the "validate" step and then also when a row data is updated during the "validate" step. An example use case for Row Function is if you want to mark a cell as required based on a specific value in another cell in the same row.

**Column Functions** run validation on a set of selected columns when the user clicks the Submit button on the "validate" step. These are best used in cases where entire column data is required for validation. For example, say you want to find duplicate entries in a column. You could grab all the values in the column, find duplicate values, and display the message to the user.

<figure><img src="../.gitbook/assets/Validation Functions.svg" alt=""><figcaption><p>Validation Functions</p></figcaption></figure>



