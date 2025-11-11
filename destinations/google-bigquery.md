---
description: >-
  Import CSV or Excel data directly into your Google BigQuery tables using
  CSVbox.
---

# Google BigQuery

Follow the steps below to securely connect your BigQuery project and map your columns.

***

#### Step 1: Choose Google BigQuery as Destination

From your sheet’s **Destination Settings** page, select **Google BigQuery** from the “Send Data To” dropdown.

This enables all the necessary fields to configure your BigQuery connection.

***

#### Step 2: Enter Connection Details

You will need to fill in the following fields:

**Project ID**

Enter your Google Cloud **Project ID**.\
You can find this in your Google Cloud Console under **Home → Project Info → Project ID**.

**Dataset ID**

Specify the **Dataset ID** where your target table is located.\
This is the dataset name within your BigQuery project.

**Table Name**

Enter the exact **Table Name** where the data should be inserted.\
Make sure this table already exists in your BigQuery dataset.

***

#### Step 3: Upload JSON Key File

BigQuery requires authentication via a **Service Account Key**.

1. In your Google Cloud Console, go to\
   **IAM & Admin → Service Accounts → Keys → Add Key → Create New Key.**
2. Choose **JSON** as the key type and download the file.
3. In CSVbox, click **Browse**, select your JSON key file, and click **Upload**.

> ⚠️ Only `.json` files are accepted for this field.

This securely connects CSVbox to your BigQuery project.

***

#### Step 4: Test the Connection

After entering your credentials, click the **Test Connection** button.\
CSVbox will attempt to connect to your BigQuery project and validate the configuration.

* ✅ If successful, you’ll see a confirmation message.
* ❌ If there’s an error, double-check your credentials, dataset, or table name.

***

#### Step 5: Map Columns

Once your connection is validated, click **Map Columns** to proceed.\
You’ll be able to map the columns from your CSV file to the corresponding fields in your BigQuery table.

After mapping, all future imports through your CSVbox importer will automatically push data into your specified BigQuery table.

***

#### Notes

* Ensure that the BigQuery table schema matches the data types in your uploaded CSV to avoid type mismatch errors.
* CSVbox uses the **Service Account credentials** only to insert data — no other operations are performed.

***

#### Example Configuration

| Field         | Example Value               |
| ------------- | --------------------------- |
| Project ID    | `data-project-123`          |
| Dataset ID    | `sales_data`                |
| Table Name    | `orders`                    |
| JSON Key File | `bigquery-credentials.json` |

***

#### Troubleshooting

* **Invalid JSON key:** Ensure the key file is not modified and is a valid service account key.
* **Table not found:** Confirm that the specified table exists in the dataset.
* **Permission denied:** Verify that your service account has the `BigQuery Data Editor` role or higher.
