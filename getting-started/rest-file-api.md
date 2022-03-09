---
description: Automate CSV submissions via REST File API
---

# REST File API

{% hint style="warning" %}
REST File API is under development. The expected launch date is 31 March 2022.
{% endhint %}

The File API lets you accept spreadsheet files programmatically. It is an alternative to the users uploading the files manually, via the Csvbox importer. Files submitted via the REST File API will then be pushed to the data destination as set up in the Csvbox dashboard.

After the data is pushed to the destination, the [import complete webhook ](./#import-complete-webhook)will be triggered as configured in the sheet settings.

{% hint style="info" %}
The spreadsheets submitted via File API will not be [validated](https://help.csvbox.io/validations). The importer will attempt to push the file directly to the destination in the raw form.
{% endhint %}

### Authentication

All REST File API queries require a valid API key. You can find the API key on the **Accounts** page in the Csvbox dashboard.

Include your API key as a `X-Csvbox-Api-Key` header on all API queries.&#x20;

### Endpoint

{% swagger method="post" path="/file" baseUrl="https://api.csvbox.io/1.1" summary="Submits a spreadsheet file" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="file" type="Object" required="true" %}
File object
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-Csvbox-Api-Key" required="true" %}
API Key
{% endswagger-parameter %}

{% swagger-parameter in="body" name="public_file_url" required="true" type="String" %}
The public URL of the spreadsheet that is to be submitted.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sheet" type="Object" required="true" %}
Sheet object
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sheet.license_key" type="String" required="true" %}
Sheet license key
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user" type="Object" %}
Object 

[referencing the user](https://help.csvbox.io/getting-started#referencing-the-user)


{% endswagger-parameter %}

{% swagger-parameter in="body" name="options" type="Object" %}
Object 

[referencing the import options](https://help.csvbox.io/getting-started#additional-options)


{% endswagger-parameter %}

{% swagger-parameter in="body" name="dynamic_columns" type="Object" %}
Object 

[referencing dynamic columns](https://help.csvbox.io/getting-started/dynamic-columns)


{% endswagger-parameter %}

{% swagger-response status="200: OK" description="File submitted" %}
```javascript
HTTP/1.1 200 OK
{
  "import_id": 79418895,
  "license_key":"jhkjsahjkhkjhkjhkjasdasd",
  "sheet_id": 575,
  "sheet_name": "Products Import",
  "destination_type": "webhook",
  "import_starttime": 87987897897,
  "custom_fields": {
    "user_id": "1a2b3c4d5e6f",
    "team_id": "sales2",
    "permissionLevel": "admin"
  },
  "options": {
    "max_rows": 150,
    "language": "de"
  },
  "dynamic_olumns": [
     {
      "column_name": "qualification",
      "display_label": "Highest Qualification",
      "info_hint": "What is your highest educational degree",
      "matching_keywords": "degree, education",
      "type": "text",
      "validators": {
        "min_length": 2,
        "max_length": 50
      },
      "required": true
    },
    {
      "column_name": "experience",
      "display_label": "Work Experience",
      "info_hint": "Years of work experience",
      "matching_keywords": "",
      "type": "number",
      "validators": {
        "min_value": 0,
        "max_value": 100
      },
      "required": false
    }
  ]
}
```
{% endswagger-response %}
{% endswagger %}

#### Example Request

{% tabs %}
{% tab title="curl" %}
```javascript
curl -d '{"file":{"public_file_url":"https: //xyx.com/admin/download-csv/UXOR2MphpEu2sSAIISpY7AKmOIzAKygLNy8eviEr"},"sheet":{"license_key":"jhkjsahjkhkjhkjhkjasdasd"},"user":{"user_id":"1a2b3c4d5e6f","team_id":"sales2","permissionLevel":"admin"},"options":{"max_rows":"150","language":"de"},"dynamic_columns":[{"column_name":"qualification","display_label":"HighestQualification","info_hint":"Whatisyourhighesteducationaldegree","matching_keywords":"degree,   education","type":"text","validators":{"min_length":2,"max_length":50},"required":true},{"column_name":"experience","display_label":"WorkExperience","info_hint":"Yearsofworkexperience","matching_keywords":"","type":"number","validators":{"min_value":0,"max_value":100},"required":false}]}' \
-X POST "https://api.csvbox.io/1.1/file" \
-H "X-Csvbox-Api-Key: {api_key}" \
-H "Content-Type: application/json"
```
{% endtab %}

{% tab title="php" %}
```php
$client = new Rest("api.csvbox.io/1.1/file", $apiKey);

$response = $client->post(
  "file": {
    "public_file_url": "https: //xyx.com/admin/download-csv/UXOR2MphpEu2sSAIISpY7AKmOIzAKygLNy8eviEr"
  },
  "sheet": {
    "license_key": "jhkjsahjkhkjhkjhkjasdasd"
  },
  "user": {
    "user_id": "1a2b3c4d5e6f",
    "team_id": "sales2",
    "permissionLevel": "admin"
  },
  "options": {
    "max_rows": "150",
    "language": "de"
  },
  "dynamic_columns": [
    {
      "column_name": "qualification",
      "display_label": "HighestQualification",
      "info_hint": "Whatisyourhighesteducationaldegree",
      "matching_keywords": "degree,   education",
      "type": "text",
      "validators": {
        "min_length": 2,
        "max_length": 50
      },
      "required": true
    },
    {
      "column_name": "experience",
      "display_label": "WorkExperience",
      "info_hint": "Yearsofworkexperience",
      "matching_keywords": "",
      "type": "number",
      "validators": {
        "min_value": 0,
        "max_value": 100
      },
      "required": false
    }
  ]  
);

```
{% endtab %}
{% endtabs %}

### Rate limits

The REST Admin API supports a limit of 30 requests per minute. This allotment replenishes at a rate of 2 requests per second.&#x20;

Past the limit, the API will return a `429 Too Many Requests` error.

All REST API responses include the `X-Csvbox-File-Api-Call-Limit` header, which shows how many requests the client has made, and the total number allowed per minute.

A `429` response will also include a `Retry-After` header with the number of seconds to wait until retrying your query.

### Status and error codes

All API queries return HTTP status codes that can tell you more about the response.

**401 Unauthorized**

The client doesn’t have correct authentication credentials.

```
HTTP/1.1 401 Unauthorized
{
    "errors": "[API] Invalid API key or access token."
}
```

**402 Import Limit Reached**

The monthly import limit based on the account plan is reached. You can upgrade the plan to increase the import limit.

```
HTTP/1.1 402 Import Limit Reached
{
    "errors": "The account has exceeded the import limit."
}
```

**403 Forbidden**

The server is refusing to respond. This is typically caused if File API is disabled.

```
HTTP/1.1 403 Access Denied
{
    "errors": "User does not have access."
}
```

**404 Not Found**

The referenced sheet was not found.

```
HTTP/1.1 404 Not Found
{
    "errors": "Sheet not found."
}
```

**422 Unprocessable File**

The request body contains file errors. This is typically caused by incorrect file path, invalid file permissions, incorrect file format, corrupt file, file size too large, etc.

```
HTTP/1.1 422 Unprocessable File
{
    "errors": "Invalid file format."
}
```

**429 Too Many Requests**

The client has exceeded the [rate limit](rest-file-api.md#rate-limits).

```
HTTP/1.1 429 Too Many Requests
{
    "errors": "API Rate limit reached. Reduce request rates to resume uninterrupted service."
}
```

**5xx Errors**

An internal error occurred in Csvbox. Report to our team for such errors.

```
HTTP/1.1 500 Internal Server Error
{
    "errors": "An unexpected error occurred."
}
```
