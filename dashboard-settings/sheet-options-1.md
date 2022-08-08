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