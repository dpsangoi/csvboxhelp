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

## Info Hint

`optional`

Info Hints are help tooltips that will get displayed when the users hover the mouse over the Column Name \(or click it\) in the importer. They are useful to convey additional information about the Column.

![Info Hint](../.gitbook/assets/infohints.png)

## Matching Keywords

`optional`

You can provide a set of keywords as alternative matching options to help users match column names automatically. For example, let's say you have a column name 'First Name'. If you think a lot of your users might have sheets with columns as 'F\_Name' or simply 'First', then you can add two matching keywords 'F\_Name' and 'First'. The importer will then automatically match columns to the specified keywords to speed up column mapping.

{% hint style="info" %}
CSVBox also deploys an intelligent column mapping algorithm. Based on the historical columns mapped by the users, the importer automatically maps the columns for new uploads to simplify column matching. Even if you do not provide Matching Keywords, the importer will adapt and auto-suggest columns as more sheets get uploaded.
{% endhint %}

## Column Type

`required`

This option helps you specify the data type of the incoming data and configure relevant validation rules. You can select the column type from the dropdown and set conditions for how the data should be formatted. If the incoming data does not match the column type \(and its validation rules\), then the user will see a relevant error message identifying what the problem is and how to fix it. This ensures that the data is clean and ready to use before it gets pushed to your app.

## Required

`optional`

The Required checkbox indicates whether a column is mandatory. If the Required checkbox is ticked, then the importer will validate the column for missing/empty data. If any cell in the column is found to be empty then the user will be shown a relevant error message.

