---
description: >-
  Extract structured tables from PDFs, images, and documents with simple,
  transparent pricing
---

# AI Document Import

CSVBox allows you to import tabular data from PDFs, images, and documents using AI-powered extraction. This feature is designed to make unstructured data import-ready in just a few steps while keeping pricing predictable and usage fully transparent.

***

### How to enable AI Document Import

You can enable this feature directly within your sheet configuration:

**Sheet Settings → Import Steps → File Upload → Enable AI Document Import**

Once enabled, users will be able to upload documents (PDFs, images, DOCX) during the import flow.

***

### Data privacy & security

Your documents are processed using secure external AI services for table extraction.

* Your uploaded documents are **not used to train or improve any public AI models**
* The service guarantees your data is **not used for any purpose other than processing your request**
* Files are handled securely and processed only for extraction

***

### What is a “document page”?

A **page** is the unit used for billing document processing.

* PDF → each page = 1 page
* Images (JPG, PNG, WEBP, etc.) → each image = 1 page
* DOCX → processed as pages based on document layout

Note: DOCX page counts are estimated based on document structure.

***

### Monthly included pages

Each plan includes a fixed number of document pages per billing cycle:

| Plan    | Included pages / month |
| ------- | ---------------------- |
| Sandbox | 5 pages                |
| Startup | 50 pages               |
| Pro     | 500 pages              |
| Growth  | 1,000 pages            |
| Plus    | 3,000 pages            |

* Limits reset every billing cycle
* Unused pages do not roll over

***

### Extra pages (credits)

If you exceed your monthly included pages:

* Additional pages cost **$0.03 per page**
* Charges are deducted from your prepaid credit balance

***

### What are credits?

Credits are a prepaid balance used for document processing.

* You can top up anytime via the **Plans page**
* Credits are used only after your included pages are exhausted
* Credits are stored as a monetary balance (USD)

Example:

* $10 ≈ 333 pages
* $25 ≈ 833 pages

***

### How usage is calculated

When you process documents, pages are consumed in this order:

1. Included monthly pages
2. Credit balance
3. If both are exhausted → processing is blocked

***

### Selecting the correct table

Many documents contain multiple tables. CSVBox gives you full control:

* All detected tables are shown in a preview
* You can review each table visually
* You select the exact table you want to import

This ensures accurate imports even from complex or multi-section documents.

***

### Example usage

You are on the Pro plan (500 pages/month)

You process 600 pages in a month:

* 500 pages → included
* 100 pages → credits

Cost:

* 100 × $0.03 = **$3.00**

***

### When will I be charged?

A page is charged when it is successfully sent for AI processing.

You are not charged when:

* file upload fails
* file is unsupported
* document cannot be read before processing starts

***

### Failed or low-quality results

In some cases:

* no tables are detected
* extraction quality is not usable

These pages are still charged because AI processing has already been performed.

***

### Partial processing

If processing stops midway:

* only successfully processed pages are charged

Example:

* 20-page document
* 12 pages processed before failure
* you are charged for 12 pages only

***

### Retries

* Manual retry → charged again
* System retry (internal failure) → not double-charged

***

### What happens when I run out of pages?

* You will receive an **email alert when you reach 90% of your usage**
* Once your included pages and credits are exhausted:
  * document processing will be blocked
  * you will be prompted to add credits

***

### Adding credits

You can add credits anytime from the **Plans page**:

1. Go to the Plans page
2. Choose a credit amount
3. Complete payment

Credits are applied instantly after successful payment.

***

### Viewing your usage

You can monitor usage from your dashboard:

* Included pages used and remaining
* Credit balance
* Pages processed this cycle
* Recent document processing activity

***

### Billing cycle

* Included pages reset every billing cycle
* Your billing cycle depends on your subscription start date
* Credit balance does not reset and carries forward

***

### Important notes

* Charges are based on pages processed, not successful extraction
* Each image counts as one page
* Credits are used only after included pages are exhausted
* CSV and Excel imports are not affected by this pricing

***

### FAQ

**Do unused pages roll over?**\
No, included pages reset every billing cycle.

**Do credits expire?**\
No, credits remain in your account until used.

**Can I get a refund for failed extraction?**\
If a failure is caused by a system issue, contact support and we’ll review it.

**Are CSV/Excel imports charged?**\
No, only document-based imports (PDF, images, DOCX) are counted.

**Can I increase my included pages?**\
Yes, upgrade your plan to get a higher monthly allowance.
