---
description: Description of select sheet configuration settings
---

# Sheet Options

## Show Error Text

<details>

<summary>Display the import fail error messages back to the end-users.</summary>

<img src="../.gitbook/assets/error option.jpg" alt="" data-size="original">

To see the errors, the users will have to click the 'See Errors' button on the import complete screen.

<img src="../.gitbook/assets/errorlist.jpg" alt="" data-size="original">

</details>

## Export Button

<details>

<summary>Export validation errors in Excel</summary>

With this option, you can enable/disable the **Export** button on the verify data screen. Your users can export data to Excel while keeping the error highlighting and error messages. This helps to resolve the errors in the Excel sheet and quickly re-upload the file in CSVbox.

![](<../.gitbook/assets/Export settings.jpg>)

<img src="../.gitbook/assets/Export button.jpg" alt="" data-size="original">

![](../.gitbook/assets/Excel1.png)

</details>

## Server & Data Location

<details>

<summary>Select the geographic location of the servers &#x26; database for the user data.</summary>

Data residency refers to where the data is stored in a geographical location. The location is important usually for regulatory or policy reasons.

You have the option to select the storage location of the data uploaded by your users.

Go to **Edit Sheets** > **Options** > **Privacy & Security** section > Select the location from the dropdown.

<img src="../.gitbook/assets/locations.png" alt="" data-size="original">

The US is the default location. The other option is Europe (Germany.)

The data uploaded by the users will then pass through servers and get stored in the database situated in the selected location only.

Note, that you also have the option to not store the data at all.

The long-lived data about the import and the user files is not covered under the selected location. It mainly consists of supplementary log data helpful for troubleshooting and analyzing the import processes. This data does not include any original data from inside the user files.\
\
The image below shows how the data will flow if you select Europe as the data residency location.

<img src="../.gitbook/assets/data flow location (1).svg" alt="" data-size="original">

</details>

## Domain Authorization

<details>

<summary>Run the importer on select domains only</summary>

You can provide a list of authorized _domains/sub-domains_ for embedding the importer. The embedded importer will work on the whitelisted domains only.

Go to **Edit Sheets** > **Options** > **Authorized Domains** > Add the domain/subdomains

![](../.gitbook/assets/domains.jpg)

* If you do not whitelist any domain, then the importer embed will work on all the domains. This is the default configuration.
*   You can use the "\*" wildcard prefix to include any subdomain. A few examples:

    | Text              | Valid                        | Invalid                              |
    | ----------------- | ---------------------------- | ------------------------------------ |
    | exampleco.com     | exampleco.com                | www.exampleco.com, app.exampleco.com |
    | www.exampleco.com | www.exampleco.com            | exampleco.com, app.exampleco.com     |
    | app.exampleco.com | app.exampleco.com            | exampleco.com, www.exampleco.com     |
    | \*.exampleco.com  | all exampleco.com subdomains |                                      |

If a domain fails validation then the user will see the error screen as below:![](../.gitbook/assets/udo.jpg)

</details>

## File Delete Policy

<details>

<summary><strong>Managing User Data Storage in CSVbox</strong></summary>

You have the option to either enable or disable the storage of the user uploaded data in CSVbox. This decision can be made based on privacy preferences or specific sheet requirements.

<img src="../.gitbook/assets/image (16).png" alt="" data-size="original">

* **Do not store the file**: By enabling this option, the user-uploaded data will not be stored in the CSVbox datastore.
* **Store data**: Data will be stored on CSVbox storage. It will be auto deleted after one month.

</details>

## Import Complete Messages

<details>

<summary>Show custom messages when the import is completed</summary>

You can show customized success or failure messages when the import is complete. <img src="../.gitbook/assets/custom messages.jpg" alt="" data-size="original">

The messages can be:

1. **Static** - Any fixed text as per your requirements.
2. **Dynamic** - Provide an API to fetch the message text in real-time. The importer will append metadata (`import_id`, `sheet_id`) to the API as query parameters. This will help determine the context and return relevant messages.

</details>

## Resubmit Button

<details>

<summary>1-click to resubmit the same CSV file again</summary>

With this option, you can show or hide the Resubmit button on the Import Success screen.

The Resubmit button triggers a new import pushing the same file with the same import configuration.

This is useful during testing and debugging. You don't have to upload the file, match columns and confirm data for importing the file. Simply click the Resubmit button and push the file to the same destination.

![](<../.gitbook/assets/resubmit button.jpg>)



</details>

## Importer Dialog Size

<details>

<summary>Control the size of the import dialog box for large screens</summary>

Based on your import data structure (# of columns) you can pick between two import dialog sizes:

1.  Medium

    <figure><img src="../.gitbook/assets/medium_screen.jpg" alt=""><figcaption><p>Medium size</p></figcaption></figure>
2.  Large

    <figure><img src="../.gitbook/assets/large_screen.jpg" alt=""><figcaption><p>Large size</p></figcaption></figure>

To change the size go to sheet settings > display > Importer Dialog Size

![](<../.gitbook/assets/select size.jpg>)

Note: The dialog size configuration will be applicable for large (desktop) screens only. For smaller screens the dialog will always occupy the entire screen.

</details>

## Worksheet Selection

<details>

<summary>Allow users to select a worksheet for upload</summary>

There can be a case where the uploaded Excel file contains multiple worksheets. You can allow the users to select a worksheet for upload.

To activate worksheet selection go to sheet settings > display > File Upload > Select '**Yes**' for **Allow Worksheet Selection** option.

<img src="../.gitbook/assets/multi selection.jpg" alt="" data-size="original">

If the **Allow Worksheet Selection** option is set to '**No**' then the first worksheet will be picked up by default.

</details>

## Custom Redirect URL

<details>

<summary>Redirect end users to any page after successful import</summary>

You have the ability to specify a custom URL for redirection upon successful import completion. This enhancement is designed to provide greater flexibility and streamline your workflow by directing users to a specific page immediately after the successful import.

![](../.gitbook/assets/redirect_url.jpg)



</details>

## Show File Upload Box

<details>

<summary>Enable / Disable the ability to upload spreadsheet files</summary>

There can be a case where you need to disable user file uploads to allow only copy-pasting of the data in CSVbox. In such cases, you can hide the File Upload Box and only show the users the Copy-Paste data option.

To hide the File Upload Box go to sheet settings > display > File Upload > Select '**No**' for '**Show File Upload Box?**' option.

</details>

## Import Description

<details>

<summary>Allow users to provide a name/description of the file they are uploading</summary>

Enable users to input a name or a description for their uploaded files. File names like "contacts.csv" or "Import 123.xlsx" lack context. More descriptive labels such as "Texas Customers" or "Parts from 2022 Catalog" enhance the clarity and utility of the import.

The description input box will be visible if enabled after the user selects the file.\
\
&#x20;<img src="../.gitbook/assets/file_description (1).png" alt="" data-size="original">

The description will be pushed along with the row data at the end destination. The data will be available in the **import\_description** property:

```
    "import_id": 79418895,
    "sheet_id": 575,
    "sheet_name": "Products234248",
    "import_description": "Product Catalogue Jan 2024", 
    "env_name": "default", 
    "destination_type": "webhook",
```

The following destinations are supported:

1. API/Webhook
2. Zapier
3. [Data at Client](../getting-started/3.-receive-data.md#data-on-the-client-side)
4. [Import Complete Webhook](../getting-started/3.-receive-data.md#import-complete-webhook)

To enable the description input box:

Go to Sheet Settings > Display Tab > Select 'File Upload' Page > Go to 'Show import description' option > Select 'Yes'

![](../.gitbook/assets/import_description_option.jpg)

By default his feature is turned OFF.

A minimum of 3 characters and a maximum of 100 characters is required.&#x20;



</details>

