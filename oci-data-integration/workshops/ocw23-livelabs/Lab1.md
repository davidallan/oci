# Create the Object Storage and ADW Data Assets
## **Introduction**
Learn how to create **Data assets** for your source and target data sources used in *Create an OCI Data Integration Workspace*. You will be using **Object Storage** as the source and **Autonomous Data Warehouse** as the target. Data assets can be databases, flat files, and so on.

**Estimated Time**: 10 minutes
### **Objectives**
- Create Object Storage data asset
- Create Autonomous Data Warehouse data asset
##
## Task 1: Create Object Storage data asset
In this workshop, **Oracle Object Storage** serves as the **source data asset** for our data integration tasks. In this step you will create the Object Storage data asset in the Data integration workspace.

1. In the Oracle Cloud Infrastructure Console navigation menu, navigate to **Analytics & AI**. Under Data Lake, click **Data Integration**.

![The content is described above.](images/image.001.png)

1. From the Workspaces page, make sure that you are in the compartment you created for data integration (DI-compartment). Click on your **Workspace** (DI-workspace).

![The content is described above.](images/image.002.png)

1. On your workspace Home page, click **Create Data Asset** from the **Quick Actions tile**.

![The content is described above.](images/image.003.png)

1. The Create Data Asset dialog box appears. Fill in the following:
   1. **Name**: Object\_Storage.
   1. **Description**: you can optionally enter a description about your data asset.
   1. From the **Type** dropdown, select Oracle Object Storage.
   1. Under **Default Connection** Information, you can optionally enter a name and description for the connection or leave the default one.

1. After you complete all the required fields, you can click on **Test Connection** to ensure you've entered the data asset details correctly. A success or failure message displays, indicating whether the test was successful or not. If the test fails, review your connection settings and try again.

![The content is described above.](images/image.004.png)

1. Click **Create**.

![The content is described above.](images/image.005.png)

##
## Task 2: Create Autonomous Data Warehouse data asset
1. In the Oracle Cloud Infrastructure Console navigation menu, navigate to **Analytics & AI**. Under Data Lake, click **Data Integration**.

![The content is described above.](images/image.001.png)

1. From the Workspaces page, make sure that you are in the compartment for data integration (DI-compartment). Click on your **Workspace** (DI-workspace).

![The content is described above.](images/image.002.png)

1. From the workspace home landing page, click **Data Assets**.

![The content is described above.](images/image.006.png)

1. You can see your current existing Data Assets, more specifically the Object Storage. To create a new Data Asset for ADW, click on **Create Data Asset**.

![The content is described above.](images/image.007.png)

1. On the **Create Data Asset** page, for **General Information**, set the following:
   1. **Name**: Data\_Warehouse.
   1. **Identifier**: Auto-generated based on the value you enter for Name.
   1. **Description**: It is optional to give a description for your data asset.
   1. **Type**: Oracle Autonomous Data Warehouse.
   1. Choose the **Upload Wallet** option to provide the login credentials for the ADW
   1. **Wallet File**: Drag and drop or browse to select your wallet file. See the process to download the wallet in *Provision an Autonomous Data Warehouse and download Wallet* under *Setting up the Data Integration prerequisites in OCI*.
   1. Enter your **wallet password**.
   1. **Service Name**: Choose the **low** service of Autonomous Data Warehouse. *Note*: For more information on predefined Database Service Names for Autonomous Data Warehouse, please see the following [link](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/cswgs/autonomous-connect-database-service-names.html#GUID-9747539B-FD46-44F1-8FF8-F5AC650F15BE).

![The content is described above.](images/image.008.png)

1. In the **Connection** section, enter the following:
   1. **Name**: BETA connection
   1. **Description**: Optional (For example, Connect with BETA user)
   1. **User Name**: BETA
   1. **Password**: The password you added for BETA user in *Setting up the Data Integration prerequisites in OCI*.

![The content is described above.](images/image.009.png)

1. After you complete all the required fields, you can click **Test Connection** to ensure you've entered the data asset details correctly. A success or failure message displays, indicating whether the test was successful or not. If the test fails, review your connection settings and try again.

![The content is described above.](images/image.004.png)

1. Click **Create**.

![The content is described above.](images/image.005.png)

**Congratulations!** Now you have created the Data Assets for Autonomous Data Warehouse and Object Storage, in OCI Data Integration.

