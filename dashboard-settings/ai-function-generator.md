---
description: >-
  Generate validation rules, transforms, virtual columns, and regex patterns
  using plain-language instructions
---

# AI Function Generator

The **AI Function Generator** in CSVBox helps you create JavaScript functions and regex patterns without writing code manually. Simply describe what you want in plain English, and CSVBox will generate compatible logic for your importer automatically.

AI generation is available across:

* Validation Functions
* Virtual Columns
* Data Transforms
* Regex Column Type

This feature is designed to help you build advanced import logic faster, reduce manual coding, and simplify complex validation or transformation workflows.

***

## How It Works

1. Open a supported editor in CSVBox
2. Click the **Generate** button ✨
3. Describe the logic you want
4. CSVBox generates compatible JavaScript or regex code
5. Review the generated output
6. Insert and save the function

All generated code remains fully editable before saving.

***

## Supported Features

| Feature              | Generates                        |
| -------------------- | -------------------------------- |
| Validation Functions | JavaScript validation logic      |
| Virtual Columns      | JavaScript computed column logic |
| Data Transforms      | JavaScript transformation logic  |
| Regex Column Type    | Regular expression patterns      |

***

## Writing Better Prompts

The quality of the generated output depends heavily on how clearly the requirement is described.

For best results:

* Mention exact column names when possible
* Clearly describe the expected output
* Include formatting requirements
* Add examples for complex logic
* Focus on one task at a time
* Avoid vague instructions

***

## AI Generator for Validation Functions

Use AI to generate validation rules using plain-language descriptions instead of manually writing JavaScript validation logic.

Perfect for:

* Email validation
* Phone number validation
* Date validation
* Required field checks
* Cross-column validation
* Business-specific validation rules

***

### Example Prompts

#### Email Validation

**Prompt**

```
Validate that email addresses contain a valid @ symbol and domain
```

**Expected Behaviour**

* `"user@example.com"` → valid
* `"user@"` → invalid

***

#### Phone Number Validation

**Prompt**

```
Ensure phone numbers contain exactly 10 digits after removing special characters
```

**Expected Behaviour**

* `"(555) 123-4567"` → valid
* `"123-456"` → invalid

***

#### Date Validation

**Prompt**

```
Check that dates are in YYYY-MM-DD format and are not future dates
```

**Expected Behaviour**

* `"2023-12-25"` → valid
* `"12/25/2023"` → invalid

***

#### Cross Column Validation

**Prompt**

```
Ensure end_date is greater than start_date
```

**Expected Behaviour**

* `start_date="2023-01-01", end_date="2023-12-31"` → valid
* `start_date="2023-12-31", end_date="2023-01-01"` → invalid

***

### Validation Prompt Tips

For better validation results:

1. Start with action words such as:
   * validate
   * ensure
   * verify
   * require
   * check
2. Mention exact field names
3. Describe the validation condition clearly
4. Include valid and invalid examples for complex rules
5. Mention how blank or null values should behave

***

## AI Generator for Virtual Columns

Generate computed or derived columns using natural-language instructions.

Instead of manually writing JavaScript logic, describe what the virtual column should calculate or return.

Perfect for:

* Combining fields
* Calculated totals
* Derived statuses
* Formatting dates
* Extracting values
* Building custom labels

***

### Example Prompts

#### Full Name Column

**Prompt**

```
Combine first_name and last_name columns with proper capitalization
```

**Expected Behaviour**

* `"john"` + `"DOE"` → `"John Doe"`

***

#### Total Price Calculation

**Prompt**

```
Multiply quantity and unit_price columns to create total_price
```

**Expected Behaviour**

* `quantity=5, unit_price=10.50` → `52.50`

***

#### Date Formatting

**Prompt**

```
Convert dates from MM/DD/YYYY to Month DD, YYYY format
```

**Expected Behaviour**

* `"12/25/2023"` → `"December 25, 2023"`

***

#### Status Generation

**Prompt**

```
Create a status column based on due_date
```

**Expected Behaviour**

* Past date → `"Overdue"`
* Within 7 days → `"Due Soon"`
* Future date → `"On Track"`

***

### Virtual Column Prompt Tips

1. Mention which fields should be used
2. Describe the expected output clearly
3. Specify formatting rules
4. Include examples for calculated logic
5. Focus on one generated field at a time

***

## AI Generator for Data Transforms

Generate data transformation logic using plain-language instructions.

Use AI to clean, normalize, or reformat imported data automatically.

Perfect for:

* Text normalization
* Formatting cleanup
* Phone number cleanup
* Date conversion
* Value mapping
* Row transformations

***

### Example Prompts

#### Email Standardization

**Prompt**

```
Convert email addresses to lowercase and remove leading or trailing spaces
```

**Expected Behaviour**

* `" John.Doe@Example.COM "` → `"john.doe@example.com"`

***

#### Phone Number Cleanup

**Prompt**

```
Remove all non-numeric characters from phone numbers
```

**Expected Behaviour**

* `"(555) 123-4567"` → `"5551234567"`

***

#### Full Name Generation

**Prompt**

```
Combine first_name and last_name columns with proper capitalization
```

**Expected Behaviour**

* `"john"` + `"DOE"` → `"John Doe"`

***

#### Date Formatting

**Prompt**

```
Convert dates from MM/DD/YYYY format to YYYY-MM-DD
```

**Expected Behaviour**

* `"12/25/2023"` → `"2023-12-25"`

***

### Data Transform Prompt Tips

1. Start with action words like:
   * convert
   * remove
   * replace
   * format
   * normalize
   * combine
2. Specify the target column
3. Clearly describe the final output format
4. Include sample input/output values for complex transforms
5. Keep transformations focused and specific

***

## AI Generator for Regex Patterns

Generate regular expression (regex) patterns using plain-language descriptions.

Instead of manually writing regex syntax, describe the format you want to validate and CSVBox will generate the regex pattern automatically.

Perfect for:

* Email validation
* Phone number formats
* ZIP/postal codes
* Product code validation
* Password rules
* Custom formatting patterns

***

### Example Prompts

#### Phone Number Validation

**Prompt**

```
exactly 10 digits, no spaces or dashes
```

**Generated Pattern**

```regex
/^[\d]{10}$/
```

***

#### Email Validation

**Prompt**

```
valid email format with @ symbol and domain
```

**Generated Pattern**

```regex
/^[^\s@]+@[^\s@]+\.[^\s@]+$/
```

***

#### ZIP Code Validation

**Prompt**

```
5 digit US zip code, optionally followed by hyphen and 4 digits
```

**Generated Pattern**

```regex
/^\d{5}(-\d{4})?$/
```

***

#### Product Code Format

**Prompt**

```
product code starting with 2 uppercase letters followed by exactly 4 digits
```

**Generated Pattern**

```regex
/^[A-Z]{2}\d{4}$/
```

***

## Best Practices

### Keep Prompts Focused

Short, focused prompts produce better results than large multi-step instructions.

Good:

```
Convert SKU values to uppercase
```

Less Effective:

```
Convert SKU values to uppercase, remove spaces, validate duplicates, generate category names, and create status values
```

***

### Use Exact Column Names

Prefer:

```
Combine first_name and last_name
```

Instead of:

```
Combine the user's names
```

***

### Mention Formatting Rules

Examples:

* `YYYY-MM-DD`
* `10 digit phone number`
* `uppercase product code`
* `currency with 2 decimals`

***

### Include Examples for Complex Logic

Adding examples improves accuracy significantly.

Example:

```
Convert dates from MM/DD/YYYY to YYYY-MM-DD. Example: 12/25/2023 → 2023-12-25
```

***

## Testing Generated Code

Always review and test generated code before saving.

Recommended testing steps:

1. Review the generated output
2. Test with sample values
3. Test blank and null values
4. Verify edge cases
5. Confirm expected formatting
6. Ensure only intended fields are modified

***

## Limitations

### Current Limitations

* Generates JavaScript functions and regex patterns only
* External APIs and network requests are not supported
* Browser APIs like localStorage and cookies cannot be used
* Complex multi-step workflows may require multiple functions

***

### Unsupported Operations

The AI cannot:

* Add or remove rows
* Modify your importer schema
* Access external systems
* Call third-party APIs
* Access databases
* Read files outside CSVBox
* Perform actions outside the CSVBox execution environment

***

## Common Issues

### Generation Failed

#### Possible Causes

* Network issue
* Temporary server-side issue
* Prompt too complex
* Prompt too ambiguous

#### Solutions

* Retry after a few seconds
* Simplify the prompt
* Make instructions more specific
* Break large logic into smaller prompts

***

### Generated Output Is Incorrect

#### Possible Causes

* Missing formatting details
* Ambiguous instructions
* Missing edge cases
* Unclear expected output

#### Solutions

* Add input/output examples
* Mention formatting rules explicitly
* Specify null or blank value handling
* Focus on one task at a time

***

## Tips for Better Results

1. Use exact field names whenever possible
2. Keep prompts concise and specific
3. Mention edge cases such as blank values
4. Include examples for complex rules
5. Generate one function at a time
6. Review generated code before saving
7. Test thoroughly before production use

***

## Security and Safety

Generated code runs within the CSVBox execution environment and follows CSVBox security restrictions.

Generated functions cannot:

* access external systems
* make network requests
* access browser storage
* modify importer configuration automatically

All generated code should be reviewed and tested before production use.
