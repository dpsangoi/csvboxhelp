---
description: Bulk add columns to a new sheet by providing the column info in a CSV file.
---

# Bulk Add Columns

CSVbox offers two methods to do this:

<figure><img src="../.gitbook/assets/sleekshot (2).png" alt=""><figcaption></figcaption></figure>

### 1. Using Sample CSV File

Upload any sample CSV or Excel file you already have. We’ll automatically extract the column headers from your file and create corresponding columns in your sheet. Our AI will attempt to detect column types based on the data. You can always review and modify the columns afterward.

### 2. Using Bulk Import Template

If you prefer more control over column setup, use our **predefined CSV template**. Simply download the template, fill it with column info, and upload it back. Columns will be created based on the data you provide. The template supports the following fields:

<table><thead><tr><th width="150">Field</th><th width="453">Description</th><th>Required</th></tr></thead><tbody><tr><td><a href="https://help.csvbox.io/getting-started/sheet-options#column-name">Column Name</a></td><td>Internal name of the column</td><td>✅ Yes</td></tr><tr><td><a href="https://help.csvbox.io/getting-started/sheet-options#display-label">Display Name</a></td><td>Display label for end users</td><td>Optional</td></tr><tr><td><a href="https://help.csvbox.io/getting-started/sheet-options#info-hint">Info Hint</a></td><td>Tooltip/help text for users</td><td>Optional</td></tr><tr><td>C<a href="https://help.csvbox.io/getting-started/sheet-options#column-type">olumn Type</a></td><td>Type of the field (e.g. Text, Number, Date)</td><td>Optional</td></tr><tr><td><a href="https://help.csvbox.io/getting-started/sheet-options#required">Is Required</a></td><td>Should this field be mandatory? (Yes/No)</td><td>Optional</td></tr><tr><td><a href="https://help.csvbox.io/getting-started/sheet-options#matching-keywords">Keywords</a></td><td>Tags to help with auto-mapping</td><td>Optional</td></tr></tbody></table>

**Download Template:**

{% file src="../.gitbook/assets/add-columns-template.csv" %}
Bulk Import Template
{% endfile %}

