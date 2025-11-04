---
description: Easily import CSV or Excel data directly into your Supabase tables.
---

# Supabase

### 🧭 Overview

The Supabase destination lets you push uploaded spreadsheet data from CSVBox straight into your Supabase database. It’s ideal for SaaS products that already use Supabase as their backend.

***

### ⚙️ Setup Instructions

#### 1. Choose Supabase as the Destination

In your **Sheet Settings**, set **Destination Type** to **Supabase**.

#### 2. Connect Your Database

Provide your Supabase project credentials:

* **Project URL** – found in your Supabase project settings
* **Service Role Key** – available under **Project → API → Service Role**

> 🔒 _CSVBox stores credentials securely and uses them only for insert operations._

#### 3. Set the Target Table Name

Enter the **Table Name** where you want the imported data to be inserted. Ensure that this table already exists in your Supabase database. Click Test Connection to see if it is successful.

#### 4. Map Columns to Fields

Match each column in your CSV or Excel sheet to the corresponding field in your Supabase table.

#### 5. Use Custom Attribute Mapping _(Optional)_

You can also map custom attributes from the CSV to specific fields in your table.

***

### 🚀 Data Flow

Once the setup is complete, every submitted file will automatically insert the processed data into your specified Supabase table — row by row — without any manual intervention.

***

### 🧩 Notes

* Ensure your Supabase table schema matches the uploaded columns (case-sensitive).
* Insert operations use Supabase’s REST API under the hood.
* Bulk uploads are optimized for large CSVs.
* You can combine Supabase with CSVBox features like **validation rules**, **virtual columns**, and **AI Transforms** for advanced workflows.
