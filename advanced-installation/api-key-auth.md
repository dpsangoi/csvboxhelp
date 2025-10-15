---
description: >-
  Authenticate API requests to CSVBox using a secure header-based scheme that
  validates both your API Key and Secret API Key.
---

# API Key Auth

### Overview

CSVBox requires **two authentication headers** for all protected API requests:

{% hint style="info" %}
WARNING

* Always send requests over **HTTPS**.
* Never include keys in query parameters or expose them in browser-side code.
* Store keys securely in your server environment.
{% endhint %}

***

### Finding Your Keys

1. Log in to [CSVBox Dashboard](https://app.csvbox.io/).
2. Click your profile name → **Profile → API Keys** tab.
3. Copy your API and Secret keys.
4. If keys are missing or compromised, click **Regenerate Key**.

{% hint style="info" %}
Secret keys are shown **only once** when generated. Store them safely in environment variables or a secrets manager.
{% endhint %}

***

### Authentication Flow

1. Client sends a request to a protected endpoint with both headers.
2. CSVBox validates:
   * The API key exists and is active.
   * The Secret key matches the same account.
3. If valid → returns `200 OK` and requested data.
4. If invalid → returns an appropriate error code.

***

### Endpoint

## Verify Credentials API

<mark style="color:green;">`POST`</mark> `https://api.csvbox.io/1.1/auth`

You can verify your credentials using this endpoint.

**Headers**

| Name                    | Value                  |
| ----------------------- | ---------------------- |
| content-type            | `application/json`     |
| x-csvbox-api-key        | \<your-api-key>        |
| x-csvbox-secret-api-key | \<your-secret-api-key> |

**Body**

| Name   | Type   | Description      |
| ------ | ------ | ---------------- |
| `name` | string | Name of the user |
| `age`  | number | Age of the user  |

**Response**

{% tabs %}
{% tab title="200 OK" %}
```json
{
  "message": "successfully authenticated"
}
```
{% endtab %}
{% endtabs %}

#### ❌ Error Responses

| Status                    | Error                        | Example                               |
| ------------------------- | ---------------------------- | ------------------------------------- |
| **400 Bad Request**       | Missing or malformed headers | `{ "errors": "bad_request" }`         |
| **401 Unauthorized**      | Invalid credentials          | `{ "errors": "invalid_credentials" }` |
| **403 Forbidden**         | Account lacks permission     | `{ "errors": "forbidden"}`            |
| **429 Too Many Requests** | Rate limit exceeded          | `{ "errors": "rate_limited"}`         |

***

### Security Best Practices

* Use **HTTPS (TLS)** exclusively.
* Send keys in **headers**, never in URLs.
* Mask secret fields in your UI (`type="password"`).
* Do **not log** raw keys—mask them (e.g., `****abcd`).
* Rotate and revoke keys regularly via dashboard.
*   Store credentials as environment variables:

    ```bash
    CSVBOX_API_KEY=your_api_key
    CSVBOX_SECRET_API_KEY=your_secret_key
    ```
* For browser apps, always proxy API requests through your backend.

***

#### Example Requests

{% tabs %}
{% tab title="cURL" %}
```javascript
curl -i -X GET "https://api.csvbox.io/1.1/auth" \
  -H "Accept: application/json" \
  -H "x-csvbox-api-key: <your-api-key>" \
  -H "x-csvbox-secret-api-key: <your-secret-key>"
```
{% endtab %}

{% tab title="jQuery (for testing)" %}
```javascript
$.ajax({
  url: "https://api.csvbox.io/1.1/auth",
  headers: {
    "x-csvbox-api-key": "<api-key>",
    "x-csvbox-secret-api-key": "<secret-key>"
  },
  success: (data) => console.log("Authenticated:", data),
  error: (xhr) => console.error("Error:", xhr.status, xhr.responseJSON)
});
```
{% endtab %}

{% tab title="PHP" %}
```php
<?php
$ch = curl_init("https://api.csvbox.io/1.1/auth");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  "Accept: application/json",
  "x-csvbox-api-key: " . getenv('CSVBOX_API_KEY'),
  "x-csvbox-secret-api-key: " . getenv('CSVBOX_SECRET_API_KEY')
]);

$response = curl_exec($ch);
$code = curl_getinfo($ch, CURLINFO_HTTP_CODE);
curl_close($ch);

if ($code === 200) {
  echo "Authenticated successfully:\n" . $response;
} else {
  echo "Authentication failed (HTTP $code):\n" . $response;
}
```
{% endtab %}

{% tab title="NodeJS" %}
```javascript
import axios from "axios";

async function testAuth() {
  try {
    const res = await axios.get("https://api.csvbox.io/1.1/auth", {
      headers: {
        "Accept": "application/json",
        "x-csvbox-api-key": process.env.CSVBOX_API_KEY,
        "x-csvbox-secret-api-key": process.env.CSVBOX_SECRET_API_KEY
      },
    });
    console.log("Authenticated:", res.data);
  } catch (err) {
    console.error("Error:", err.response?.data || err.message);
  }
}

testAuth();
```
{% endtab %}
{% endtabs %}

{% hint style="danger" %}
Never expose your secret keys in browser-side code.
{% endhint %}

***

### FAQ

**Can I send only the API key?**\
No. Both headers are required for authentication.

**Can I use query parameters for keys?**\
No. Query-based authentication is disabled for security reasons.

**Where should I store my keys?**\
Store them server-side in environment variables or a secrets manager.

**I lost my secret key. What now?**\
Regenerate it from the **API Keys** page.

***

### Troubleshooting & Support

If authentication fails:

1. Verify exact header names (`x-csvbox-api-key`, `x-csvbox-secret-api-key`).
2. Ensure your account and keys are active.
3. Confirm you’re using **HTTPS**.
4. If still failing, contact support@csvbox.io with your request ID or timestamp.

***

### Summary

| Topic         | Details                                       |
| ------------- | --------------------------------------------- |
| Method        | Header-based (API Key + Secret Key)           |
| Headers       | `x-csvbox-api-key`, `x-csvbox-secret-api-key` |
| Protocol      | HTTPS only                                    |
| Auth Type     | Server-to-server                              |
| Test Endpoint | `GET https://api.csvbox.io/1.1/auth`          |

{% hint style="info" %}
Use this endpoint to verify your integration before making any other CSVBox API calls.
{% endhint %}
