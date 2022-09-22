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

## Import Complete Messages

<details>

<summary>Show custom messages when the import is completed</summary>

You can show customized success or failure messages when the import is complete. <img src="../.gitbook/assets/custom messages.jpg" alt="" data-size="original">

The messages can be:

1. **Static** - Any fixed text as per your requirements.
2. **Dynamic** - Provide an API to fetch the message text in real-time. The importer will append metadata (`import_id`, `sheet_id`) to the API as query parameters. This will help determine the context and return relevant messages.

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
