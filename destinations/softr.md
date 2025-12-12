---
description: Collect spreadsheets from users and push clean data to Softr database.
---

# Softr

CSVBox allows you to send imported spreadsheet data directly into **Softr Databases**, enabling no-code workflows such as internal tools, portals, directories, and dashboards powered by Softr.

With this destination, every successful CSV import will insert rows into a selected Softr table.

***

### When to use Softr as a Destination

Use the **Softr destination** when you want to:

* Import CSV / Excel data into Softr databases
* Power Softr apps with bulk uploads
* Allow non-technical users to upload structured data
* Replace manual Softr data entry with a guided importer

***

### Configure Softr Destination in CSVBox

Follow the steps below to configure Softr as your data destination.

#### Step 1: Select Softr as Destination

1. Go to **Sheet Settings → Destination**
2. Click **Select Destination**
3. Choose **Softr** from the list

***

#### Step 2: Enter Softr Credentials

Fill in the following required fields:

**API Key**

* Your Softr API Key
* Used to authenticate requests from CSVBox to Softr

**Database ID**

* The ID of the Softr database where data should be inserted
* This identifies the parent database inside Softr

**Table ID**

* The specific table inside the database that will receive the data
* Each imported row becomes a new record in this table

> 💡 How to get Database ID and Table ID from Softr
>
> 1. **log in to Softr**
> 2. Go to **Data → Databases**
> 3. Click on the **database** you want
> 4. Click on the **table** inside that database
> 5. Look at the **browser URL**
>
> You’ll see something like:
>
> https://studio.softr.io/databases/<mark style="color:red;">**ecc84771-ca85-48f2-abc3**</mark>?table=<mark style="color:red;">**ajZqlE5O9KOy1**</mark><br>
>
> Extract the IDs:
>
> **Database ID:&#x20;**<mark style="color:red;">**ecc84771-ca85-48f2-abc3**</mark>
>
> **Table ID:&#x20;**<mark style="color:red;">**ajZqlE5O9KOy1**</mark>

***

#### Step 3: Test Connection

Click **Test Connection** to verify:

* API key validity
* Access to the specified database
* Access to the selected table

A successful test confirms CSVBox can write data to Softr.

***

#### Step 4: Map Columns

Click **Map Columns** to:

* Map CSV / Excel columns to Softr table fields
* Ensure field types are compatible
* Control which columns are sent to Softr

> Column mapping is mandatory before running an import.

***

#### Step 5: Save Configuration

Click **Save** to persist the Softr destination settings.

Your importer is now ready to send data directly into Softr.

***

### How Data Is Sent to Softr

* Each successfully imported row becomes **one record** in the selected Softr table
* Data is sent **after validation** and **after transforms**

***

### Troubleshooting

**Connection test fails**

* Verify API key permissions
* Double-check Database ID and Table ID
* Ensure the table exists and is accessible

**Columns not appearing**

* Revisit **Map Columns**
* Ensure Softr field names and types match incoming data

***

### Notes & Limitations

* Softr destination currently supports **row inserts**
* Large imports may take longer depending on Softr API limits
