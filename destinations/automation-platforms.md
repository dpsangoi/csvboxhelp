---
description: >-
  Send CSVbox imports to Zapier, n8n, Make, Workato, or any workflow automation
  tool with one universal setup.
---

# Automation Platforms

CSVbox makes it easy to connect your spreadsheet imports with any automation platform.\


Using the **`New Row Import`** trigger, you can send every imported row into your workflows — whether that means adding a contact to Salesforce, storing data in Postgres, or sending a Slack notification.

This guide shows you how to integrate CSVbox with popular tools like **Zapier, Make, n8n, Pipedream, IFTTT, Node-RED, Workato, Tray.io, Airflow, Prefect, Camunda**, and more.

Once connected, each new row uploaded by your users can automatically flow into your databases, CRMs, analytics pipelines, or enterprise systems — without writing custom code for every tool.

***

### 🔑 Core Pattern

1. **Webhook Event (Trigger)**
   * CSVbox sends a webhook on each row import.
   *   Example payload:

       ```json
       [
         {
           "import_id": 79418895,
           "sheet_id": 55,
           "sheet_name": "Products",
           "row_number": 1,
           "total_rows": 1009,
           "env_name": "default", 
           "original_filename": "products01_24.csv",
           "row_data": {
                 "Name": "TP-Link TL-WN822N Wireless N300 High Gain USB Adapter",
                 "SKU": "AS-100221",
                 "Price": "33.00",
                 "Quantity": "3",
                 "Image URL": "https://cdn.shopify.com/s/files/1/1491/9536/products/31jJOj1DS5L_070b4893-b7af-482f-8a15-d40f5e06760d.jpg?v=1521803806"
           },
           "custom_fields": {
             "user_id": "1002"
           }
         }  
       ]
       ```
2. **Automation Platform**
   * Receives this webhook.
   * Executes downstream actions: database insert, CRM update, Slack notification, etc.

***

### ⚙️ Integration Guides (Step by Step)

#### 🔹 1. Zapier

**Steps:**

1. Create a new Zap.
2. Select **Webhooks by Zapier** → _Catch Hook_.
3. Copy webhook URL.
4. In CSVbox Dashboard → Settings → Webhooks → paste the Zapier URL.
5. Perform a test import in CSVbox.
6. Confirm data mapping in Zapier.
7. Add actions (e.g., Google Sheets → Add Row, Salesforce → Create Contact).
8. Turn on Zap.

✅ Each new row import flows into Zapier automations.

***

#### 🔹 2. Make (Integromat)

**Steps:**

1. Create a new Scenario.
2. Add a **Webhook module** → Custom Webhook.
3. Copy webhook URL.
4. Paste it into CSVbox Dashboard → Webhooks.
5. Run scenario (listening mode).
6. Test import in CSVbox → payload appears.
7. Add modules (Sheets, MySQL, Slack, etc.).
8. Save & activate.

***

#### 🔹 3. Pipedream

**Steps:**

1. Create new Workflow.
2. Trigger: **HTTP/Webhook**.
3. Copy webhook URL to CSVbox Dashboard.
4. Test import in CSVbox.
5.  Add Code Step:

    ```js
    export default defineComponent({
      props: { event: { type: "object" } },
      async run({ steps, $ }) {
        console.log("Row Imported:", this.event.data);
      }
    });
    ```
6. Add downstream integrations (DB, CRM, Slack).

***

#### 🔹 4. n8n

**Steps:**

1. Create workflow.
2. Add **Webhook node**.
3. Copy webhook URL to CSVbox Dashboard.
4. Test import → n8n captures payload.
5. Add downstream nodes (Postgres, Slack, HTTP).
6. (Optional) Use CSVbox Node to fetch rows by `import_id`.

***

#### 🔹 5. Node-RED

**Steps:**

1. Add **HTTP In node** → URL `/csvbox`.
2. Add **JSON node** → parse payload.
3.  Add **Function node**:

    ```js
    msg.payload = msg.payload.data;
    return msg;
    ```
4. Connect target nodes (DB, Email, Slack).
5. Deploy and paste URL into CSVbox Dashboard.

***

#### 🔹 6. IFTTT

**Steps:**

1. In IFTTT, create an **Applet**.
2. “If This” → **Webhooks** → Receive a web request (`row_imported`).
3. Copy webhook key/URL.
4. In CSVbox Dashboard → paste URL.
5. “Then That” → pick action (e.g., send email, notification, IoT device).

✅ Lightweight consumer-friendly automations.

***

#### 🔹 7. Activepieces

**Steps:**

1. In Activepieces, create a new Flow.
2. Add **Webhook Trigger**.
3. Copy URL into CSVbox Dashboard.
4. Test import → Activepieces captures row data.
5. Add actions (e.g., Google Sheets, Airtable, APIs).
6. Save & activate.

***

#### 🔹 8. Automatisch

**Steps:**

1. Create a workflow.
2. Trigger → Webhook.
3. Copy webhook URL → paste into CSVbox Dashboard.
4. Import test row → Automatisch captures payload.
5. Add downstream integrations.

***

#### 🔹 9. Huginn

**Steps:**

1. Add **Webhook Agent**.
2. Copy Huginn webhook URL.
3. Paste into CSVbox Dashboard.
4. Test import → Huginn captures JSON.
5. Chain agents (Post Agent → Slack Agent → Email Agent).

***

#### 🔹 10. StackStorm

**Steps:**

1. Create **Webhook sensor** in StackStorm.
2.  Rule example:

    ```yaml
    ---
    name: csvbox.new_row
    trigger: core.st2.webhook
    criteria:
      trigger.body.event: "row_imported"
    action:
      ref: core.local
      parameters:
        cmd: "echo {{trigger.body.data.email}} >> /var/log/csvbox.log"
    ```
3. Test import.

***

#### 🔹 11. Apache Airflow

**Steps:**

1. Setup Flask/Django endpoint to receive CSVbox webhook.
2. Configure CSVbox Dashboard → Webhooks → paste URL.
3. Trigger Airflow DAG with row data.
4.  Example DAG:

    ```python
    from airflow import DAG
    from airflow.operators.python import PythonOperator

    def process_row(**context):
        data = context['dag_run'].conf
        print("Row imported:", data)

    dag = DAG("csvbox_import", start_date="2025-01-01")

    process = PythonOperator(
        task_id="process_row",
        python_callable=process_row,
        dag=dag
    )
    ```

***

#### 🔹 12. Prefect

**Steps:**

1. Setup Prefect Cloud/Server.
2. Create flow with `@flow` decorator.
3. CSVbox webhook triggers a Prefect API call.
4.  Example:

    ```python
    from prefect import flow

    @flow
    def process_row(data: dict):
        print("Row Imported:", data)
    ```
5. Deploy and connect webhook.

***

#### 🔹 13. Kestra

**Steps:**

1. Create a Kestra flow with a **Webhook Trigger**.
2.  Example:

    ```yaml
    id: csvbox_import
    namespace: csvbox
    tasks:
      - id: log
        type: io.kestra.core.tasks.debugs.Log
        message: "{{ trigger.body }}"
    ```
3. Paste Kestra webhook URL into CSVbox Dashboard.

***

#### 🔹 14. Temporal

**Steps:**

1. Define a workflow in Temporal.
2.  Example:

    ```python
    @workflow.defn
    class ImportWorkflow:
        @workflow.run
        async def run(self, row: dict):
            print("Processing:", row)
    ```
3. CSVbox webhook → EventBridge/queue → starts Temporal workflow.

***

#### 🔹 15. Inngest

**Steps:**

1.  In Inngest, define an event handler:

    ```js
    inngest.createFunction(
      { id: "csvbox-row-imported" },
      { event: "csvbox/row.imported" },
      async ({ event }) => {
        console.log("Row:", event.data)
      }
    )
    ```
2. Configure CSVbox webhook to send event payloads to Inngest.

***

#### 🔹 16. Windmill

**Steps:**

1. In Windmill, create a new flow.
2. Trigger → HTTP endpoint.
3. Paste URL into CSVbox Dashboard.
4. Test import → Windmill captures payload.
5. Add code step in Python/JS to process rows.

***

#### 🔹 17. Tray.io

**Steps:**

1. Create a Tray workflow.
2. Add a **Webhook Trigger**.
3. Copy URL into CSVbox Dashboard.
4. Import test row.
5. Add actions (Salesforce, NetSuite, DBs).

***

#### 🔹 18. Workato

**Steps:**

1. Create a Workato recipe.
2. Add **Webhook Trigger**.
3. Copy URL → paste into CSVbox Dashboard.
4. Test import → Workato captures row data.
5. Add enterprise actions (ERP, CRM, HR tools).

***

### 📦 Developer SDK (Optional)

Offer an SDK so dev teams can wire CSVbox directly:

```js
import { Csvbox } from "csvbox-sdk";

const client = new Csvbox({ apiKey: "xxx" });

client.on("row_imported", (row) => {
  console.log("Row Imported:", row);
  // push to CRM, DB, etc.
});
```

***

### ✅ Best Practices

* **Verify webhook signatures** (HMAC secret).
* **Retry failed actions** (add DLQ or retries).
* Store `import_id` + `row_id` for tracking.
* Log every payload for debugging.
* Secure API keys properly.

***

### 🚀 Example End-to-End Flow

**Use Case:**\
“When a customer uploads a new row with email + plan → push to CRM → notify sales on Slack.”

1. CSVbox → Webhook (`row_imported`)
2. n8n workflow → Insert into HubSpot CRM
3. Slack node → “🎉 New Pro plan signup: john@example.com”

***

👉 With this playbook, CSVbox integrates seamlessly with **every automation platform**:

* **Mainstream SaaS automation** → Zapier, Make, Pipedream, IFTTT
* **Open-source low-code** → n8n, Node-RED, Activepieces, Automatisch, Huginn
* **Enterprise iPaaS** → Workato, Tray.io
* **Data orchestration** → Airflow, Prefect, Kestra
* **Developer-first platforms** → Windmill, Temporal, Inngest, StackStorm
* **Business process automation** → Camunda
