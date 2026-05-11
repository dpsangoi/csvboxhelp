---
description: >-
  Automatically split large CSV files into smaller parts for faster, more
  reliable imports with improved browser performance.
---

# Split Large CSV

### Overview

Uploading very large CSV files can cause browser slowdowns, high memory usage, or upload timeouts — especially when files contain thousands of rows.

The **Split Large Files** feature solves this by automatically dividing large CSV files into smaller parts and processing them sequentially behind the scenes.

Each part:

* Preserves the original headers and column structure
* Reuses the same column mappings automatically
* Is processed independently for improved reliability
* Remains grouped under a single parent import for easier tracking

This makes large imports significantly more stable and easier to manage.

***

### When does file splitting activate?

File splitting activates only when **all** of the following conditions are met:

* The uploaded file is a **CSV** file\
  (`.xlsx` Excel files are not currently supported)
* **Split Large Files** is enabled for the sheet
* The uploaded file exceeds the configured **Rows per Import** limit

***

## Admin Configuration

The feature can be enabled per-sheet from:

**Sheet Settings → Import Steps**

***

### 1. Split Large Files

| Setting           | Options  | Default |
| ----------------- | -------- | ------- |
| Split Large Files | Yes / No | No      |

Enable this setting to automatically split large CSV uploads into smaller parts.

When disabled, the entire CSV file is processed as a single upload.

***

### 2. Rows per Import

| Setting         | Type   | Default |
| --------------- | ------ | ------- |
| Rows per Import | Number | 1000    |

Defines the maximum number of rows processed in each part.

#### Example

If a CSV contains **4,500 rows** and the limit is set to **1,000 rows**, CSVBox will process the file in:

* Part 1 → Rows 1–1000
* Part 2 → Rows 1001–2000
* Part 3 → Rows 2001–3000
* Part 4 → Rows 3001–4000
* Part 5 → Rows 4001–4500

#### Choosing the right value

| Smaller Parts                         | Larger Parts                                 |
| ------------------------------------- | -------------------------------------------- |
| Faster processing per upload          | Fewer total parts                            |
| Lower browser memory usage            | Higher memory usage                          |
| Better reliability for large datasets | Faster overall completion for moderate files |

For most use cases, **1,000–5,000 rows per part** works well.

***

### 3. User Confirmation Between Parts

| Setting           | Options                                    | Default |
| ----------------- | ------------------------------------------ | ------- |
| User Confirmation | No / Yes / No, only if there are no errors | No      |

Controls whether users must manually continue between parts.

#### Available Modes

| Mode                            | Behavior                                                                |
| ------------------------------- | ----------------------------------------------------------------------- |
| No                              | All parts upload automatically                                          |
| Yes                             | User must confirm before each next part uploads                         |
| No, only if there are no errors | Upload continues automatically unless a part contains validation errors |

For the smoothest experience, we recommend using **No**.

***

## End User Experience

### Step 1 — Upload a CSV File

The user uploads a CSV file normally through the importer.

If the file exceeds the configured row limit, CSVBox automatically prepares the file for multipart processing.

***

### Step 2 — Split Notification

Before processing begins, the user sees a notification such as:

> Large file detected\
> We'll split this file into smaller parts (X rows each) for smoother processing. Each part will be uploaded automatically, and your column mappings will be reused.

The user can then:

* **Start Upload** — Continue processing
* **Cancel** — Cancel the upload

***

### Step 3 — Map Columns (First Part Only)

The first part behaves exactly like a normal CSVBox import.

The user:

* Maps columns
* Reviews data
* Fixes validation issues if needed
* Submits the import

CSVBox automatically reuses the same mappings for all remaining parts.

The user does **not** need to map columns again.

***

### Step 4 — Automatic Processing of Remaining Parts

After the first part is submitted, remaining parts are processed automatically.

A progress indicator shows overall upload progress.

#### Example

```
Processing (2/5)

2,000 / 5,000 rows processed
```

Depending on the confirmation mode, the user may or may not be prompted between parts.

***

### Step 5 — Import Completion

Once all parts finish processing:

* The multipart upload is marked as completed
* All parts remain grouped under a single parent import
* Users can review part-level details if needed

***

## Viewing Multipart Imports

Multipart uploads appear as a single grouped import in the **All Imports** page.

CSVBox automatically tracks:

* Overall import status
* Number of processed parts
* Row counts
* Failed or partial parts

***

### Multipart Import Statuses

| Status          | Meaning                          |
| --------------- | -------------------------------- |
| Success         | All parts processed successfully |
| Processing      | Upload is still running          |
| Partial Failure | Some parts failed                |
| Failed          | Entire upload failed             |

***

### Viewing Part Details

Opening the import details shows information for each individual part.

| Column    | Description                     |
| --------- | ------------------------------- |
| Part      | Part sequence number            |
| Status    | Success / Failed / Processing   |
| Rows      | Rows processed in that part     |
| Import ID | Individual import reference     |
| Errors    | Validation or processing errors |

***

## Import Limits & Billing

Multipart uploads count as **a single import** toward your plan limits.

For example:

* A 10-part upload = **1 import**
* A 50-part upload = **1 import**

Individual parts are not counted separately.

***

## Reliability & Error Handling

Each part is processed independently for improved stability.

This means:

* A failure in one part does not invalidate already completed parts
* Failed parts can be retried individually
* Successfully processed parts remain intact

***

### If a Part Fails

If a part encounters validation errors or processing failures:

* The multipart upload is marked as **Partial Failure**
* Error details are available for the failed part
* Successfully processed parts remain unaffected

***

### If the Browser is Closed Mid-Upload

If the browser closes before processing completes:

* Completed parts remain saved
* Remaining parts stop processing
* The upload status reflects the completed progress

We recommend keeping the browser open until the upload finishes.

***

## Limitations

### Excel Files Are Not Supported

Currently, multipart processing supports **CSV files only**.

Excel (`.xlsx`) files are processed as a single upload regardless of size.

If needed, convert Excel files to CSV before uploading.

***

### Maximum Parts Per Upload

To ensure reliable processing, a single upload can generate up to **100 parts**.

If the configured row limit would exceed this number, the upload will stop with an error message.

In this case:

* Increase the **Rows per Import** value
* Or split the source CSV manually before uploading

***

## Best Practices

For optimal performance:

* Use CSV files instead of Excel for very large datasets
* Keep row limits between **1,000–5,000**
* Enable automatic uploads when possible
* Use smaller part sizes for slower devices or lower-memory environments

***

## FAQ

### Do all parts use the same column mapping?

Yes. Once the first part is mapped, CSVBox automatically reuses the same mapping for all remaining parts.

### Are parts sent separately to destinations?

Yes. Each part is processed independently and sent separately to the configured destination.

### Can users retry failed parts?

Yes. Failed parts can be retried individually without re-uploading the full file.

### Can I disable this feature for specific users?

No. The feature is configured per sheet, not per user.

If different users require different behavior, create separate sheets with different settings.
