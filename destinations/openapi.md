---
description: >-
  Send your CSV or Excel sheet data directly to any API described by an OpenAPI
  specification.
---

# OpenAPI

## How it works

1.  **Select the destination type as 'OpenAPI'.** Open your sheet, go to **Destination**, and choose **OpenAPI** from the list.<br>

    <figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>
2. **Load the OpenAPI specification.** Paste the OpenAPI Specification URL (a link to the API's spec file) and click Load Specificatio&#x6E;**.** This pulls in the list of available endpoints.
3. **Select the endpoint.** Pick the endpoint you want to send data to (for example, `POST /v1/prices - Create Tiered Price`).
4. **Set the HTTP method.** Choose the method for the request, such as **POST** to create new records.
5. **Choose the authentication type.** Select how the API verifies you (for example, **Bearer Token**) and enter your credentials in the field that appears (e.g. paste your **Bearer Token**).
6. **Test the connection.** Click Test Connection. A green checkmark means your settings are correct.
7. **Map sheet columns to the endpoint fields.** Match each column in your sheet to the matching field expected by the API. You can also map custom attributes.
8.

    <figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>
9. Once set up, your sheet data will be sent to the API endpoint, one request per row.\
   <br>
