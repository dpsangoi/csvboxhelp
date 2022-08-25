---
description: No code import links to accept files anywhere.
---

# Import Links

Use Import Links to accept files from your users without a website or an app. Create an import page in just a few clicks and share the link with your users—no code required. It is an alternative to the import button that can be set up by adding the integration code.

After you have created a sheet go to the 'Code' tab on the Edit Sheet page. Below the integration code find the Import Link of the sheet. It will look something like this:

```javascript
https://app.csvbox.io/upload/2gzJa5YO3QPLYK6Bj7Qmq5bpbFqXno?user_id=default123
```

Simply share this link with your users to start collecting spreadsheets.

#### Referencing the user in the Import Links

You can configure the query parameters in the link to identify and match the users with their respective imports. Add up to 5 query parameters with custom user attributes that help you identify the users in your platform. The custom user attributes will be pushed to your destination along with the uploaded data.

**user\_id** is the only custom attribute that is mandatory. Apart from **user\_id,** you can add up to 4 custom attributes in the`&key=value`format. Example:

```javascript
https://app.csvbox.io/upload/2gzJa5YO3QPLYK6Bj7Qmq5bpbFqXno?user_id=1a2b3c4d5e6f&team_id=sales2&isAuthenticated=true&permissionLevel=admin&email=abc@example.com
```

#### Activating Import Links

You can activate or deactivate import links via sheet settings. Go to **Sheet Edit** page > **Options** tab > **Import Links** > Select _Activate_ or _Deactivate in the_ dropdown.

<figure><img src="../.gitbook/assets/import links activation (1).jpg" alt=""><figcaption><p>Activate Import Links</p></figcaption></figure>

If the Import Links are deactivated the users will see the following message:

<figure><img src="../.gitbook/assets/disabled.jpg" alt=""><figcaption><p>Import Links disabled</p></figcaption></figure>
