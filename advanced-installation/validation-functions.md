---
description: Validate data with custom Javascript functions.
---

# Validation Functions

{% hint style="info" %}
coming soon
{% endhint %}

If the validations you require are not covered with the in-built [data type validations](../dashboard-settings/validations.md) in CSVbox then you can code your own custom validation functions.

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
Check if a column has duplicate entries

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
