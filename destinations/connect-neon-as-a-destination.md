---
description: >-
  Push your CSV files and Excel sheets directly into your Neon (serverless
  Postgres) database.
---

# Connect Neon as a Destination

## How it works

1. **Select the destination type as 'Neon'.** Open your sheet, go to **Destination**, and choose **Neon** from the list.\
   <img src="../.gitbook/assets/image (38).png" alt="" data-size="original">
2. **Connect your Neon database.** Enter your Neon credentials (enter the host, database name, user, and password). You can copy this from your Neon project dashboard under **Connection Details**.\
   ![](<../.gitbook/assets/image (39).png>)&#x20;
3. **Specify the table name.** Enter the name of the table where you want the data to be pushed.
4. **Map sheet columns to table columns.** Match each column in your sheet to the matching column in your Neon table. You can also map custom attributes to table columns.
5. Once set up, your CSV data will be appended directly to the Neon table.<br>
