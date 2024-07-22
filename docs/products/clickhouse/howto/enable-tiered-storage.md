---
title: Enable tiered storage in Aiven for ClickHouse®
sidebar_label: Enable tiered storage
---

Enable the [Aiven for ClickHouse® tiered storage feature](/docs/products/clickhouse/concepts/clickhouse-tiered-storage) on your project and activate it for specific tables.

### Limitations

-   You can enable tiered storage on the Aiven tenant
    (in non-[BYOC](/docs/platform/concepts/byoc) environments) if your Aiven for
    ClickHouse service is hosted on Azure, AWS, or GCP.
-   When
    [enabled](/docs/products/clickhouse/howto/enable-tiered-storage), the tiered
    storage feature cannot be deactivated.

    :::tip
    As a workaround, you can create a table (without enabling tiered
    storage on it) and copy the data from the original table (with the
    tiered storage
    [enabled](/docs/products/clickhouse/howto/enable-tiered-storage)) to the new table.
    As soon as the data is copied to the
    new table, you can remove the original table.
    :::

-   With the tiered storage feature
    [activated](/docs/products/clickhouse/howto/enable-tiered-storage), it's
    not possible to connect to an external existing
    object storage or cloud storage bucket.

### Tools

To activate tiered storage, use SQL and an SQL client (for example, the
ClickHouse CLI client).

## Prerequisites

-   You have an Aiven organization and at least one project.
-   You have a command line tool
    ([ClickHouse client](/docs/products/clickhouse/howto/connect-with-clickhouse-cli)) installed.
-   All maintenance updates are applied on your service (check in Aiven
    Console: your service's page > **Service settings** > **Service
    management** > **Maintenance updates**).

## Activate tiered storage on a table

When you have tiered storage activated on your project, you can
enable it on your tables, both new and existing ones. You can
use either SQL or [Aiven Console](https://console.aiven.io).

### Activate in Aiven Console

1. Log in to [Aiven Console](https://console.aiven.io), and go to your organization,
   in **Project** > **Service**.
1. On the **Overview** page of your service, select **Databases and tables** from the sidebar.
1. In the **Databases and tables** view, find a table on which to activate tiered
   storage, and select **Activate tiered storage** from the **Actions** menu (**...**).
1. In the **Activate tiered storage** window, confirm activating
   tiered storage on the table and understand the impact by selecting **Activate**.

### Activate with SQL

1. [Connect to your Aiven for ClickHouse service](/docs/products/clickhouse/howto/list-connect-to-service)
   using, for example, the ClickHouse client (CLI).
1. To activate the tiered storage feature on a specific table,
   set `storage_policy` to `tiered` on this table by executing the following SQL statement:

   ```bash
   ALTER TABLE database-name.table-name MODIFY SETTING storage_policy = 'tiered'
   ```

Tiered storage is activated on your table and data in this table is now
distributed between two tiers: SSD and object storage.

You can check if tiered storage is now supported (**Active** / **Inactive**) on
your table in [Aiven Console](https://console.aiven.io) > **Databases & Tables** >
**Databases lists** > Your database > Your table > **Tiered storage** column.

## What's next

- [Configure data retention thresholds for tiered storage](/docs/products/clickhouse/howto/configure-tiered-storage)
- [Check data volume distribution between different disks](/docs/products/clickhouse/howto/check-data-tiered-storage)

## Related pages

- [About tiered storage in Aiven for ClickHouse](/docs/products/clickhouse/concepts/clickhouse-tiered-storage)
- [Transfer data between SSD and object storage](/docs/products/clickhouse/howto/transfer-data-tiered-storage)
