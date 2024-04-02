---
description: Automate CSV submissions via REST File API
---

# REST File API

The File API lets you accept spreadsheet files programmatically. It is an alternative to the users uploading the files manually, via the Csvbox importer. Files submitted via the REST File API will then be pushed to the data destination as set up in the Csvbox dashboard.

#### Simple File API Request

```javascript
curl --location --request POST 'https://api.csvbox.io/1.1/file' \
--header 'x-csvbox-api-key: CSBxRLHgIZv3bqMlrJiVKXhKwtcHSv' \
--header 'Content-Type: application/json' \
--data-raw '{
    "import": {
        "public_file_url": "https: //some-domain.com/file/3434as.csv",
        "sheet_license_key": "jhkjsahjkhkjhkjhkjasdasd",
        "user": {
            "user_id": "1a2b3c4d5e6f",           
        },
         "options": {           
            "has_header": 1
        }    
}'
```

After the data is pushed to the destination, the [import complete webhook ](../getting-started/3.-receive-data.md#import-complete-webhook)can be triggered as configured in the sheet settings.

{% hint style="warning" %}
The spreadsheet data submitted via File API will not be [validated](https://help.csvbox.io/validations) based on the rules configured in the sheet settings. The importer will attempt to push the data directly to the destination in the raw form.
{% endhint %}

{% hint style="warning" %}
The columns in the file should be arranged in the same order as configured in the sheet template.
{% endhint %}

### Authentication

All REST File API queries require a valid API key. You can find the API key on the **Accounts** page in the Csvbox dashboard.

Include your API key as a `x-csvbox-api-key` header on all API queries.&#x20;

### Endpoint

## Submits a spreadsheet file

<mark style="color:green;">`POST`</mark> `https://api.csvbox.io/1.1/file`

#### Headers

| Name                                               | Type   | Description      |
| -------------------------------------------------- | ------ | ---------------- |
| x-csvbox-api-key<mark style="color:red;">\*</mark> | String | API Key          |
| content-type<mark style="color:red;">\*</mark>     | String | application/json |

#### Request Body

| Name                                                         | Type   | Description                                                                                  |
| ------------------------------------------------------------ | ------ | -------------------------------------------------------------------------------------------- |
| import.public\_file\_url<mark style="color:red;">\*</mark>   | String | The public URL of the spreadsheet that is to be submitted.                                   |
| import.sheet\_license\_key<mark style="color:red;">\*</mark> | String | Sheet license key                                                                            |
| import<mark style="color:red;">\*</mark>                     | Object | Import file data                                                                             |
| import.user                                                  | Object | Object [referencing the user](https://help.csvbox.io/getting-started#referencing-the-user)   |
| import.options                                               | Object | Object [referencing the import options](rest-file-api.md#additional-options)                 |
| import.dynamic\_columns                                      | Object | Object [referencing dynamic columns](https://help.csvbox.io/getting-started/dynamic-columns) |

{% tabs %}
{% tab title="200: OK File submitted" %}
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
    "has_header": 1
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
{% endtab %}
{% endtabs %}

#### Example Request

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'https://api.csvbox.io/1.1/file' \
--header 'x-csvbox-api-key: CSBxRLHgIZv3bqMlrJiVKXhKwtcHSv' \
--header 'Content-Type: application/json' \
--data-raw '{
    "import": {
        "public_file_url": "https: //some-domain.com/admin/download-csv/UXOR2MphpEu2sSAIISpY7AKmOIzAKygLNy8eviEr",
        "sheet_license_key": "jhkjsahjkhkjhkjhkjasdasd",
        "user": {
            "user_id": "1a2b3c4d5e6f",
            "team_id": "sales2",
            "permissionLevel": "admin"
        },
        "options": {
            "max_rows": 150,
            "has_header": 1
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
    }'
```
{% endtab %}

{% tab title="jQuery" %}
```javascript
var settings = {
  "url": "https://api.csvbox.io/1.1/file",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "x-csvbox-api-key": "CSBxRLHgIZv3bqMlrJiVKXhKwtcHSv",
    "Content-Type": "application/json"
  },
  "data": "{\r\n    \"import\": {\r\n        \"public_file_url\": \"https: //some-domain.com/admin/download-csv/UXOR2MphpEu2sSAIISpY7AKmOIzAKygLNy8eviEr\",\r\n        \"sheet_license_key\": \"jhkjsahjkhkjhkjhkjasdasd\",\r\n        \"user\": {\r\n            \"user_id\": \"1a2b3c4d5e6f\",\r\n            \"team_id\": \"sales2\",\r\n            \"permissionLevel\": \"admin\"\r\n        },\r\n        \"options\": {\r\n            \"max_rows\": 150,\r\n            \"has_header\": \"1\"\r\n        },\r\n        \"dynamic_columns\": [\r\n            {\r\n                \"column_name\": \"qualification\",\r\n                \"display_label\": \"HighestQualification\",\r\n                \"info_hint\": \"Whatisyourhighesteducationaldegree\",\r\n                \"matching_keywords\": \"degree,   education\",\r\n                \"type\": \"text\",\r\n                \"validators\": {\r\n                    \"min_length\": 2,\r\n                    \"max_length\": 50\r\n                },\r\n                \"required\": true\r\n            },\r\n            {\r\n                \"column_name\": \"experience\",\r\n                \"display_label\": \"WorkExperience\",\r\n                \"info_hint\": \"Yearsofworkexperience\",\r\n                \"matching_keywords\": \"\",\r\n                \"type\": \"number\",\r\n                \"validators\": {\r\n                    \"min_value\": 0,\r\n                    \"max_value\": 100\r\n                },\r\n                \"required\": false\r\n            }\r\n        ]\r\n    }",
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```
{% endtab %}

{% tab title="PHP" %}
```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://api.csvbox.io/1.1/file',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "import": {
        "public_file_url": "https: //some-domain.com/admin/download-csv/UXOR2MphpEu2sSAIISpY7AKmOIzAKygLNy8eviEr",
        "sheet_license_key": "jhkjsahjkhkjhkjhkjasdasd",
        "user": {
            "user_id": "1a2b3c4d5e6f",
            "team_id": "sales2",
            "permissionLevel": "admin"
        },
        "options": {
            "max_rows": 150,
            "has_header": 1
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
    }',
  CURLOPT_HTTPHEADER => array(
    'x-csvbox-api-key: CSBxRLHgIZv3bqMlrJiVKXhKwtcHSv',
    'Content-Type: application/json'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

```
{% endtab %}

{% tab title="NodeJS" %}
```javascript
var axios = require('axios');
var data = '{\r\n    "import": {\r\n        "public_file_url": "https: //some-domain.com/admin/download-csv/UXOR2MphpEu2sSAIISpY7AKmOIzAKygLNy8eviEr",\r\n        "sheet_license_key": "jhkjsahjkhkjhkjhkjasdasd",\r\n        "user": {\r\n            "user_id": "1a2b3c4d5e6f",\r\n            "team_id": "sales2",\r\n            "permissionLevel": "admin"\r\n        },\r\n        "options": {\r\n            "max_rows": 150,\r\n            "has_header": "1"\r\n        },\r\n        "dynamic_columns": [\r\n            {\r\n                "column_name": "qualification",\r\n                "display_label": "HighestQualification",\r\n                "info_hint": "Whatisyourhighesteducationaldegree",\r\n                "matching_keywords": "degree,   education",\r\n                "type": "text",\r\n                "validators": {\r\n                    "min_length": 2,\r\n                    "max_length": 50\r\n                },\r\n                "required": true\r\n            },\r\n            {\r\n                "column_name": "experience",\r\n                "display_label": "WorkExperience",\r\n                "info_hint": "Yearsofworkexperience",\r\n                "matching_keywords": "",\r\n                "type": "number",\r\n                "validators": {\r\n                    "min_value": 0,\r\n                    "max_value": 100\r\n                },\r\n                "required": false\r\n            }\r\n        ]\r\n    }';

var config = {
  method: 'post',
  url: 'https://api.csvbox.io/1.1/file',
  headers: { 
    'x-csvbox-api-key': 'CSBxRLHgIZv3bqMlrJiVKXhKwtcHSv', 
    'Content-Type': 'application/json'
  },
  data : data
};

axios(config)
.then(function (response) {
  console.log(JSON.stringify(response.data));
})
.catch(function (error) {
  console.log(error);
});

```
{% endtab %}
{% endtabs %}

### Rate limits

The REST Admin API supports a limit of 30 requests per minute. This allotment replenishes at a rate of 2 requests per second.&#x20;

Past the limit, the API will return a `429 Too Many Requests` error.

All REST API responses include the x`-csvbox-file-api-call-limit` header, which shows how many requests the client has made, and the total number allowed per minute.

A `429` response will also include a `retry-after` header with the number of seconds to wait until retrying your query.

### Status and error codes

All API queries return HTTP status codes that can tell you more about the response.

**401 Unauthorized**

The client doesn’t have the correct authentication credentials.

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

### Options

Here is the list of additional configuration options available with the File API.

#### max\_rows

<table><thead><tr><th width="150"></th><th></th><th data-hidden></th></tr></thead><tbody><tr><td>Type</td><td>Integer</td><td></td></tr><tr><td>Default</td><td>Null</td><td></td></tr><tr><td>Description</td><td>The maximum number of rows to import.</td><td></td></tr></tbody></table>

#### has\_header

<table><thead><tr><th width="150"></th><th></th><th data-hidden></th></tr></thead><tbody><tr><td>Type</td><td>Boolean</td><td></td></tr><tr><td>Default</td><td>0</td><td></td></tr><tr><td>Description</td><td><p>Specify whether the file contains a header row.<br><br>Acceptable values are:</p><p><strong>0</strong> (no header)</p><p><strong>1</strong> (has a header row)</p></td><td></td></tr></tbody></table>

