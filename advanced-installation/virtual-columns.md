---
description: Create new columns by applying custom data transformation logic.
---

# Virtual Columns

{% hint style="warning" %}
Beta version coming soon
{% endhint %}

**Virtual Columns** are one of CSVbox’s most powerful data transformation tools.&#x20;

You can run small snippets of JavaScript that can **re-format**, **correct**, **validate**, and **enrich** incoming data during a data import.

Super useful if you need to process your data, do calculations, merge things together, etc before receiving it at your end.

### How it works

1. For any sheet, add a virtual column via CSVbox dashboard.
2. Attach a Javascript snippet to the virtual column.
3. When users upload a CSV file, the Javascript will run to populate data in the virtual column.
4. Data from the uploaded CSV as well as the virtual column will be pushed to the data destination.

#### Example

{% tabs %}
{% tab title="Merge" %}
Merge data from the _first\_name_ and the _last\_name_ columns into a new virtual column named _full\_name_.

Here is the attached Javascript for the _full\_name_ virtual column:

```javascript
try
{  	
	return csvbox.row["first_name"] + ' ' + csvbox.row["first_name"];
}
catch(err)
{  
  	return 'error: ' + err.name + ' | ' + err.message;
}
```
{% endtab %}

{% tab title="Reformat" %}
Normalize the incoming order\_date into UTC format.

```javascript
try
{  	const date = new Date(csvbox.row["order_date"]);

	return date.toUTCString();
}
catch(err)
{  
  	return 'error: ' + err.name + ' | ' + err.message;
}
```
{% endtab %}
{% endtabs %}

