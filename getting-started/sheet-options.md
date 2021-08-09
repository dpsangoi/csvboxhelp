---
description: Description of sheet configuration settings
---

# Sheet Options

## Column Name

`required`

The Column Name is the field name key that will be pushed to the data destination.

## Display Label

`optional`

Display Labels will be shown in the header row that the user will see while doing an import. Each Display Label internally maps to a Column Name. While the Display Label will be seen by the users inside the import widget, the corresponding Column Name will be pushed to the destination as the field name. If Display Label is not specified, then the Column Name will be shown to the users by default. This helps you to display a user-friendly label to the users while pushing a column name that your app understands. For example, 'p\_id' can be the Column Name and 'Product ID' can be the Display Label.

## Matching Keywords

{% hint style="warning" %}
coming soon
{% endhint %}

`optional`

You can provide a set of keywords as alternative matching options to help users match column names automatically. For example, let's say you have a column name 'First Name'. If you think a lot of your users might have sheets with columns as 'F\_Name' or simply 'First', then you can add two matching keywords 'F\_Name' and 'First'. The importer will then automatically match columns to the specified keywords to speed up column mapping.

{% hint style="info" %}
CSVBox also deploys an intelligent column mapping algorithm. Based on the historical columns mapped by the users, the importer automatically maps the columns for new uploads to simplify column matching. Even if you do not provide Matching Keywords, the importer will adapt and auto-suggest columns as more users upload sheets.
{% endhint %}

## Column Type

`required`

This option helps you specify the data type of the incoming data and configure relevant validation rules. You can select the column type from the dropdown and set conditions for how the data should be formatted. If the incoming data does not match the column type \(and its validation rules\), then the user will see a relevant error message identifying what the problem is and how to fix it. This ensures that the data is clean and ready to use before it gets pushed to your app.

