# Document Metadata Fields

Document Metadata Fields let a sheet capture details straight from an uploaded file itself, instead of asking the person uploading to type them in. A field like `Author`, `Invoice Number`, or a fixed label can be filled in automatically the moment a file is uploaded, and it shows up alongside the rest of the imported data as a regular column.

Up to 20 of these can be configured per sheet, each sourced a different way depending on what kind of information is needed. Configuration is stored on `Sheet.pdf_metadata_config`; extraction is handled by `App\Services\PdfMetadataExtractor`, called from `AnalyzeController`.

### Why Use Document Metadata Fields

* **Invoices & receipts** — capture the invoice number or vendor name straight from the document, instead of asking the uploader to re-type it into a form field.
* **Applications & forms** — tag every submission with who authored the file or what it's titled, useful for sorting and follow-up later.
* **Batch labeling** — stamp every import from a particular source or partner with a fixed label, so downstream reports can filter by it.

#### Field Sources

Each Document Metadata Field is filled in one of three ways:

**Static Value**

A fixed value typed in once. It applies to every upload processed through this sheet — useful for labels and tags that never change.

_Example: `Batch Label` = "Q3 Vendor Import"_

**Native Document Property**

Most documents quietly carry their own properties, such as who created them or what they're titled. This source reads that value straight from the file.

_Example: `Author` = whoever created the PDF or Word document_

**Document Key-Value (Smart Match)**

Give the field a name to look for — like `Invoice Number` — and CSVbox finds the value printed next to that label on the page.

_Example: field name `Invoice Number` finds "INV-4471" on the page_

### Supported File Types

| File Type               | Static Value | Native Document Property | Document Key-Value |
| ----------------------- | ------------ | ------------------------ | ------------------ |
| PDF                     | Yes          | Yes                      | Yes                |
| Word document (`.docx`) | Yes          | Yes                      | Yes                |
| Image (`.jpg`, `.png`)  | Yes          | —                        | Yes                |

> **Note:** If a value can't be found for a field, it is simply left blank for that upload. This never blocks or fails the import — the rest of the file still comes through normally.

### Enabling Document Metadata Fields

1. Open the sheet to configure and go to `Import Steps` > `File Upload`.
2. Scroll to the **Document Metadata Fields** section.
3. Add a field and give it a name — this becomes the column name people will see once data is imported.
4. Choose how it should be filled in: **Static Value**, **Native Document Property**, or **Document Key-Value**, and provide whatever it needs (a value to use, or a label to look for).
5. Repeat for each detail to capture, then click **Save Metadata Fields**.

> **Note:** Up to 20 metadata fields are allowed per sheet, and each field name must be unique.

From that point on, every matching upload gets these fields filled in automatically — no extra steps for the person uploading.

#### Example

A sheet set up to receive vendor invoices, with three metadata fields configured, processing an upload named `invoice_4471.pdf`:

| Field            | Source                   | Value Captured   |
| ---------------- | ------------------------ | ---------------- |
| `Batch Label`    | Static Value             | Q3 Vendor Import |
| `Author`         | Native Document Property | J. Alvarez       |
| `Invoice Number` | Document Key-Value       | INV-4471         |

All three values are captured the moment the file is uploaded — nobody had to type any of them in. This happens automatically as part of processing the file, with no extra wait for the person uploading.
