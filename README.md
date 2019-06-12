# Different ways to connect to storage in Azure Databricks

The following is a summary of the various ways to connect to [Blob Storage](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blobs-overview) and [Azure Data Lake Gen2](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) from [Azure Databricks](https://docs.azuredatabricks.net/index.html).

|How to connect|Scope of connection|Authentication|Authorization Requirements|Code Sample|Docs/Supported Storage
|---|---|---|---|---|---|
|**Direct connect**|Typicaly SparkSession*|Storage Key|All rights|[Python](notebooks/directconnect_storagekey_py.py), [SQL](notebooks/directconnect_storagekey_sql.sql)|[Blob](https://docs.azuredatabricks.net/spark/latest/data-sources/azure/azure-storage.html#access-azure-blob-storage-directly)
|   |   |OAuth via Service Principal (SP)|SP has **[Storage Blob Data Owner/Contributor/Reader](https://docs.microsoft.com/en-us/azure/storage/common/storage-auth-aad-rbac-portal)** role OR **[ACLs permissions](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-access-control#access-control-lists-on-files-and-directories)** to files/folders|[Python](notebooks/directconnect_oauthsp_py.py), [SQL](notebooks/directconnect_oauthsp_sql.sql)| [ADLS Gen2](https://docs.azuredatabricks.net/spark/latest/data-sources/azure/azure-datalake-gen2.html#access-an-adls-account-directly-with-oauth-2-0-using-the-service-principal)
|   |   |AD Passthrough|SP has **Storage Blob Data Owner/Contributor/Reader** role OR **ACLs permissions** to files/folders|[Python](notebooks/directconnect_adpassthrough_py.py), [SQL](notebooks/directconnect_adpassthrough_sql.sql)| [ADLS Gen2](https://docs.azuredatabricks.net/spark/latest/data-sources/azure/azure-datalake-gen2.html#access-adls-automatically-with-your-aad-credentials)
|**Mount on DBFS**|Databricks Workspace|Storage Key|All rights|[Python](notebooks/mount_storagekey_py.py)|[Blob](https://docs.azuredatabricks.net/spark/latest/data-sources/azure/azure-storage.html#mount-azure-blob-storage-containers-with-dbfs), [ADLS Gen2](https://docs.azuredatabricks.net/spark/latest/data-sources/azure/azure-datalake-gen2.html#access-an-adls-account-directly-using-the-storage-account-access-key)
|   |   |OAuth via Service Principal (SP)|SP has **Storage Blob Data Owner/Contributor/Reader** role OR **ACLs permissions** to files/folders|[Python](notebooks/mount_oauthsp_py.py)| [ADLS Gen2](https://docs.azuredatabricks.net/spark/latest/data-sources/azure/azure-datalake-gen2.html#mount-an-adls-filesystem-to-dbfs-using-a-service-principal-and-oauth-2-0)

**This will depend on where Spark Configuration is set. This is typically set on the SparkSession of the running notebook and therefore scoped to only that specific SparkSession.*