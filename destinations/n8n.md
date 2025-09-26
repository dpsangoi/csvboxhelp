---
description: Push user spreadsheet data to n8n.
---

# n8n

{% hint style="info" %}
coming soon
{% endhint %}

\
This allows you to directly connect your CSVbox imports to any of the apps supported by n8n without needing a webhook setup. With this integration, you can build workflows like:

* Save imported rows into a database (MySQL, Postgres, MongoDB, etc.)
* Send imported data to Slack, Teams, or Discord
* Trigger downstream API calls automatically
* Push leads into your CRM or marketing tools

***

### Step 1: Enable n8n as a Destination in CSVbox

1. Go to your [CSVbox Dashboard](https://dashboard.csvbox.io/).
2. Open the **Sheet Settings** for the sheet you want to integrate.
3. Navigate to the **Destinations** tab.
4. Click on **Add Destination** → select **n8n**.
5. Click on **Connect n8n** button. This will redirect you to n8n connections page.
6. Connect n8n with your csvbox.io account by providing the API Key and API Secret Key. These keys can be found on the **Accounts** page of your csvbox dashboard.
7. Save the destination.

***

### Step 2: Configure CSVbox Node in n8n

1. Open your **n8n Editor** (Cloud or Self-hosted).
2. Create a new workflow.
3. Add the **CSVbox node**.
4. Under **Credentials**, select CSVbox account.
5. Select the **Trigger** type:
   * **Import New Row** → Fires whenever new data is imported in CSVbox
6. Choose the **Sheet Name** from the dropdown list.

***

### Step 3: Add Processing Nodes

Now connect the CSVbox node to other nodes:

* **Database Nodes** → Store imported data in MySQL, Postgres, MongoDB
* **Messaging Nodes** → Send Slack or Teams alerts
* **Spreadsheet Nodes** → Save to Google Sheets, Airtable
* **HTTP Node** → Call custom APIs with imported data

***

### Example Workflow

A simple flow could be:

**CSVbox Node (trigger)** → **Google Sheets Node** → **Slack Notification Node**

This setup automatically saves imported data into a Google Sheet and then posts a confirmation message to Slack.

### Error Handling

* If the connected nodes succeed, the workflow continues normally.
* If there’s a failure (e.g. database timeout), n8n will show the error in **Executions → Error Log**.
* You can use n8n’s **Error Workflow** feature for retries or notifications.

***

### Alternative: Webhook Node

If you don’t want to use the official CSVbox node, you can still integrate using n8n’s **Webhook node**:

1. Add a **Webhook node** in n8n.
2. Copy the generated webhook URL.
3. Add this URL as a **Webhook destination** in CSVbox.
4. On each import, CSVbox will `POST` validated rows to this webhook.
