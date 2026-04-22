---
description: >-
  Get visibility into how users interact with CSVbox importer—from opening the
  widget to completing a successful import. Identify drop-offs, understand
  errors, and improve your data import experience.
---

# Import Analytics

{% hint style="info" %}
**Note:** This feature is available on **Pro plans and above**.
{% endhint %}

### What is Import Analytics?

Import Analytics tracks each importer session and shows how users move through the import flow:

* File upload
* Header selection
* Column mapping
* Data validation
* Final submission

You can use this data to understand where users struggle and optimize your importer configuration.

### What can you track?

#### 1. Import Funnel

See how many users reach each step of the import process:

* Importer Opened
* File Selected
* File Parsed
* Header Selected
* Mapping Completed
* Validation Completed
* Submit Succeeded

This helps you quickly identify where users drop off.

#### 2. Completion Rate

Measure how many users successfully complete the import compared to those who start it.

#### 3. Drop-offs

Understand where users abandon the process:

* Before selecting a file
* During header selection
* During mapping
* After validation

This helps pinpoint friction points in your flow.

#### 4. Time Taken per Step

Analyze how long users spend on each step:

* Time to select file
* Time to select header
* Time to complete mapping
* Time for validation
* Total time to complete import

#### 5. Error Insights

Identify the most common issues users face:

* File parsing errors
* Header selection issues
* Mapping errors
* Validation failures
* Destination/API errors

#### 6. Session Logs

View individual import sessions with details such as:

* Start time
* Final outcome (success, failed, incomplete)
* Last step reached
* Number of rows processed
* Error counts
* Total time taken

This is useful for debugging specific user issues.

### How to access Import Analytics

1. Go to your CSVbox Dashboard
2. Select your Sheet
3. Open the **Analytics** tab

You can filter data by date range to analyze recent or historical imports.

### Privacy & Data Handling

Import Analytics is designed to be privacy-safe.

Analytics **does not store**:

* Uploaded files
* Row data or cell values

It only tracks:

* Step-level events
* Counts and durations
* Error categories and codes

### How to use Import Analytics effectively

#### Improve onboarding

If many users drop off early, consider:

* Simplifying instructions
* Providing sample files
* Improving file format guidance

#### Optimize header selection

If users spend too long selecting headers:

* Ensure clean file templates
* Improve header row detection
* Add instructions for users

#### Fix mapping issues

If mapping drop-offs are high:

* Use clearer column names
* Reduce required fields where possible
* Enable better defaults

#### Reduce validation failures

If validation errors are common:

* Review validation rules
* Provide better error messages
* Offer clearer data requirements

#### Debug failed imports

Use session logs to:

* Inspect failed submissions
* Identify API/destination issues
* Reproduce and fix problems quickly

### Notes

* Analytics data is aggregated per sheet
* Sessions are automatically tracked—no setup required
* Abandoned sessions are detected after a period of inactivity



Import Analytics helps you move from guessing to understanding—so you can continuously improve your data import experience.
