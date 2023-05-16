# Create a Data Loader task, two Data Flows, Integration tasks and a SQL task
## **Introduction**
Learn how to create a **Data Loader task**, **two Data Flows** along with **Integration tasks** and a **SQL task** in OCI Data Integration. The use-case for each of these data integration tasks is detailed in the associated workshop task.

**Estimated Time**: 30 mins
### **Objectives**
- Create an OCI Data Integration project
- Create a Data Loader task
- Create two Data Flows
- Create Integration tasks
- Create a SQL task
## **Task 1: Create an OCI Data Integration project**
In Oracle Cloud Infrastructure Data Integration, a **project** is the container for design-time resources, such as tasks or data flows and pipelines.

1. In the Oracle Cloud Infrastructure Console navigation menu, navigate to **Analytics & AI**. Under Data Lake, click **Data Integration**.

![The content is described above.](images/image.010.png)

1. From the Workspaces page, make sure that you are in the compartment for data integration (DI-compartment). Click on your **Workspace** (DI-workspace).

![The content is described above.](images/image.011.png)

1. On your workspace home page, click **Open tab** (plus icon) in the tab bar and then select **Projects**.

![The content is described above.](images/image.012.png)

1. On the Projects page, click **Create Project**.

![The content is described above.](images/image.013.png)

1. On the Create Project page, enter DI\_Workshop for **Name** and an optional **Description**, and then click **Create**.

![The content is described above.](images/image.014.png)

1. You are now in the **Project Details** page for DI\_Workshop project.

![The content is described above.](images/image.015.png)
## **Task 2: Create a Data Loader task**
A **Data Loader task** helps you load diverse data set into data lakes, data marts, and data warehouses. A data loader task takes a source data entity, applies transformations (optional), and then loads the transformed data into a new target data entity, or updates an existing data entity. A data loader task supports transformations at the metadata and data levels.

In this step of the Workshop, you will create a Data Loader task that will load Orders data from **REVENUE.csv** source file. You will then fill up the null values for the Source Order Number and rename the Order Time zone field, and finally load data to **REVENUE\_TARGET** table in Autonomous Data Warehouse. The Data Loader task will also create the target table on the Autonomous Data Warehouse.

1. From your Workspace home page of OCI Data Integration, click **Open tab** (plus icon), and then select **Projects**.

![The content is described above.](images/image.016.png)

1. On the **Projects** page, select the project you have been working on for this workshop, DI\_Workshop.

![The content is described above.](images/image.017.png)

1. On the DI\_Workshop **Project Details** page, from the submenu, click **Tasks**.

![The content is described above.](images/image.018.png)

1. Click **Create Task**, and then select **Data Loader**.

![The content is described above.](images/image.019.png)

1. On the **Create Data Loader Task** page that pops up, for **Name**, enter Load Revenue Data into Data Warehouse.

![The content is described above.](images/image.020.png)

1. In the **Source** section, click **Select**.

![The content is described above.](images/image.021.png)

1. In the **Select Source** page that pops up, select the following values:
   1. **Data Asset**: Object\_Storage.
   1. **Connection**: Default Connection.
   1. **Compartment**: DI-compartment (the Compartment in which you have the bucket where you uploaded your REVENUE.CSV file in *Setting up the Data Integration prerequisites in OCI*).
   1. **Schema**: DI-bucket (the Object Storage bucket where you uploaded your REVENUE.CSV file in *Setting up the Data Integration prerequisites in OCI*).
   1. **Data Entity**: Click Browse by Name and then select **REVENUE.csv**.
   1. **File Type**: Set to **CSV**. Then leave the default settings as-is in all the remaining fields.
   1. Click **Select**.

![The content is described above.](images/image.022.png)

1. In the **Configure Transformations** section, click **Configure**.

![The content is described above.](images/image.023.png)

1. The Configure Transformations panel opens, showing the metadata information of the data entity and its attributes. You can also view sample data in the **Data** tab.

![The content is described above.](images/image.024.png)

1. Click **Data** to navigate to the Data tab, then locate and select **SRC\_ORDER\_NUMBER**. A panel displays, showing the **Data Profile** and the **Attribute Profile** for SRC\_ORDER\_NUMBER. Null Data Percent for SRC\_ORDER\_NUMBER is at 100%.

![The content is described above.](images/image.025.png)

1. From the **transformations icon** (three dots) for SRC\_ORDER\_NUMBER, select **Null Fill Up**.

![The content is described above.](images/image.026.png)

1. In the **Null Fill Up dialog**, do the following:
   1. Enter Not Available in the **Replace by String** field.
   1. Do **not** select Keep Source Attributes.
   1. Leave the **Name** and **Data Type** as-is.
   1. Click **Apply**.

![The content is described above.](images/image.027.png)

1. After the **Data** tab refreshes, use the horizontal scrollbar to scroll to the end of the dataset where the updated **SRC\_ORDER\_NUMBER** column is. Notice the values for SRC\_ORDER\_NUMBER have been replaced by the Not Available string.

![The content is described above.](images/image.028.png)

1. In the Data tab, look for attribute **ORDER\_DTIME2\_TIMEZONE** by scrolling to the right. Click on the **transformation icon** (three dots) for ORDER\_DTIME2\_TIMEZONE, and then select **Rename**.

![The content is described above.](images/image.029.png)

1. In the **Rename** dialog box, enter a new name for the attribute ORDER\_DTIME2\_TIMEZONE. For this workshop, enter **ORDER\_TIMEZONE** then click **Apply**.

![The content is described above.](images/image.030.png)

1. Click the **Transformations** icon next to the data entity name.

![The content is described above.](images/image.031.png)

1. You can **review the list of transformations** that are applied to the source dataset. If you would want to remove a transformation, you could click the X icon next to a transformed attribute name. For now close the Configure Transformations panel, click **OK**.

![The content is described above.](images/image.032.png)

1. The number of transformation rules applied is shown in the **Configure Transformations** section.

![The content is described above.](images/image.033.png)

1. In the **Target section**, select the **Create New Entity** check box, and then click Select.

![The content is described above.](images/image.034.png)

1. In the **Select Target** page, select the following values:
   1. **Data Asset**: Data\_Warehouse
   1. **Connection**: Beta Connection
   1. **Schema**: BETA
   1. **Data Entity**: Enter REVENUE\_TARGET for the new entity you're going to create
   1. Under **Staging Location**, select the Object\_Storage data asset
   1. Select the Default connection for Object Storage
   1. Select the DI-compartment name
   1. Select the DI-bucket
   1. Click **Select** to complete selecting the target.

![The content is described above.](images/image.035.png)

1. The Target section in the Data Loader Task now displays your selections for the target. Click **Save and Close**.

![The content is described above.](images/image.036.png)
## **Task 3: Create a Data Flow - 1**
A **data flow** is a logical diagram representing the flow of data from source data assets, such as a database or flat file, to target data assets, such as a data lake or data warehouse. The flow of data from source to target can undergo a series of transformations to aggregate, cleanse, and shape the data. Data engineers and ETL developers can then analyze or gather insights and use that data to make impactful business decisions.

You will create a data flow to ingest data from **two source files**, containing Customers (CUSTOMERS.json) and Orders (REVENUE.csv) information. The data from the files will go through a process of transformations and filtering based on the order status and country code of the customers, and in the end will be loaded to CUSTOMERS\_TARGET table in Autonomous Data Warehouse.

1. From the **Project Details** page for DI\_Workshop project, click on **Data Flows** from the submenu.

![The content is described above.](images/image.037.png)

1. Click **Create Data Flow**.

![The content is described above.](images/image.038.png)

1. The data flow designer opens in a new tab. In the Properties panel, for **Name** enter Load Customers and Revenue Data, then click **Save**. *Note*: Be sure to save often during design time!

On the left side of the canvas, you can find the data flow operators which represent input sources, output targets, and transformations that can be used. The Shaping Operators currently available are Filter, Join, Expression, Aggregate, Distinct, Sort, Union, Minus, Intersect, Split and Lookup Operator. From the Operators panel, you can drag and drop operators onto the canvas to design a data flow. Then use the Properties panel to configure the properties for each operator. For more details on Data Flow Operators, please see the following [link](https://docs.oracle.com/en-us/iaas/data-integration/using/using-operators.htm).

![The content is described above.](images/image.039.png)

1. You will add the **Source operator**. You add source operators to identify the data entities to use for the data flow. From the Operators panel on the left, **drag and drop a Source operator** onto the canvas.

![The content is described above.](images/image.040.png)

1. On the canvas, select **SOURCE\_1 operator**. The Properties panel now displays the details for this operator.

![The content is described above.](images/image.041.png)

1. In the **Details** tab from Properties panel, click Select next to each of the following options to make your selections:
   1. For **Data Asset**, select Object\_Storage.
   1. For **Connection**, select Default Connection.![The content is described above.](images/image.042.png)
   1. For **Schema**, select your **compartment** and then your **bucket**. For the purposes of this workshop, Object Storage serves as the source data asset, this is why you select your bucket here.![The content is described above.](images/image.043.png)
   1. For **Data Entity**, click on **Browse by name**. Select CUSTOMERS.json and then choose **JSON** for the file type.![The content is described above.](images/image.044.png)![The content is described above.](images/image.045.png)

In the end, the details for the source operator should look like this:

![The content is described above.](images/image.046.png)

1. When you complete your selections for **SOURCE\_1**, the operator name becomes **CUSTOMERS\_JSON**, reflecting your data entity selection. In the Identifier field, rename the source operator to **CUSTOMERS**.

![The content is described above.](images/image.047.png)

1. You will now drag and drop onto the data flow canvas another **source operator**.

![The content is described above.](images/image.048.png)

1. On the canvas, select the **new source operator**. The Properties panel now displays the details for this operator.

![The content is described above.](images/image.049.png)

1. You will now fill in the details for this source, in **Properties** panel:
   1. For **Data Asset**, select Object\_Storage.
   1. For **Connection**, select Default Connection.![The content is described above.](images/image.042.png)
   1. For **Schema**, select your **compartment** and then your **bucket**. For the purposes of this workshop, Object Storage serves as the source data asset, this is why you select your bucket here.
   1. For **Data Entity**, click on **Browse by name**. Select REVENUE.csv and then choose **CSV** for the file type. Accept the default values for the remaining items.![The content is described above.](images/image.050.png)

In the end, your details for this new source operator should look like this:![The content is described above.](images/image.051.png)

1. When you complete your selections for **SOURCE\_1**, the operator name becomes **REVENUE\_CSV**, reflecting your data entity selection. In the Identifier field, rename the source operator to **REVENUE**. *Note*: Be sure to save often during design time!

![The content is described above.](images/image.052.png)

1. While you still have the **REVENUE** operator selected, click on **Attributes** tab in Properties panel. In the Attributes tab, you can view the data entity's attributes and apply **exclude** or **rename** rules to the attributes from their respective **actions icon** (three dots). You can also use the **filter** icon on the Name or Type column to apply one or more filters on the attributes to be excluded.

![The content is described above.](images/image.053.png)

1. While you still have the **REVENUE** operator selected, click on **Data** tab in Properties panel. In the Data tab, you can view a sampling of data from the source data entity. Scroll to the right and click on field REVENUE\_CSV.CURRENCY to view the **data profile**.

![The content is described above.](images/image.054.png)

1. Click on the **Validation** tab from the Properties bar. Here you can check for warnings or errors with the configuration of the source operators. The warning with the message "Complete your data flow by connecting the operators input and output ports. Remove any unused operators from the canvas." will appear, to warn us that the operators in the data flow should be connected to other operators, for the data to flow from one node to the other. Also, the data flow must include at least one source operator and one target operator to be valid.

![The content is described above.](images/image.055.png)

1. You will now **filter your source data**. The **Filter operator** produces a subset of data from an upstream operator based on a condition. From the Operators panel, drag and drop a Filter operator onto the canvas.

![The content is described above.](images/image.056.png)

1. Connect **REVENUE** source operator to **FILTER\_1** operator:
   1. Place your cursor on REVENUE.
   1. Click the connector circle at the side of REVENUE.![The content is described above.](images/image.057.png)
   1. Drag and drop the connector to FILTER\_1.![The content is described above.](images/image.058.png)
1. Click on **FILTER\_1** on the Data Flow canvas.

![The content is described above.](images/image.059.png)

1. In the Properties panel of FILTER\_1, click **Create** for **Filter Condition**.

![The content is described above.](images/image.060.png)

1. You will now add your **filter condition**:
   1. In the Create Filter Condition panel, enter STA in the Incoming attributes search field.
   1. Double-click or drag and drop **ORDER\_STATUS** to add it to the filter condition editor.![The content is described above.](images/image.061.png)
   1. In the condition editor, enter ='1-Booked', so your condition looks like the following: FILTER\_1.REVENUE\_CSV.ORDER\_STATUS='1-Booked'
   1. Click **Create**.![The content is described above.](images/image.062.png)
1. The details for **FILTER\_1 operator** should now look like this: *Note*: Be sure to save often during design time!

![The content is described above.](images/image.063.png)

1. From the Operators panel, drag and drop a new **Filter operator** onto the canvas after CUSTOMERS. **Connect CUSTOMERS to FILTER\_2**.

![The content is described above.](images/image.064.png)

1. In the Properties panel of FILTER\_2, click **Create** for **Filter Condition**.

![The content is described above.](images/image.065.png)

1. You will now add your **filter condition** for **FILTER\_2**:
   1. In the Create Filter Condition panel, enter COU in the Incoming attributes search field.
   1. Double-click **COUNTRY\_CODE** to add it to the Filter condition editor.
   1. Enter ='US', so your condition looks like the following: FILTER\_2.CUSTOMERS\_JSON.COUNTRY\_CODE='US'
   1. Click **Create**.

![The content is described above.](images/image.066.png)

1. The details for **FILTER\_2 operator** should now look like this:

![The content is described above.](images/image.067.png)

1. You will now work on the **Data Transformation** part of your Data Flow. In the **Properties** panel for FILTER\_2, click the **Data** tab. All data rows and attributes are displayed. You can use the vertical scrollbar to scroll the rows, and the horizontal scrollbar to scroll the attributes.

![The content is described above.](images/image.068.png)

1. In the **Filter by pattern** search field, enter STATE\*. The number of attributes in the table are filtered. Only those attributes that match the pattern are displayed.

![The content is described above.](images/image.069.png)

1. Click the **transformations icon** (three dots) for FILTER\_2.CUSTOMERS\_JSON.STATE\_PROVINCE, and then select **Change Case**.

![The content is described above.](images/image.070.png)

1. In the **Change Case** dialog:
   1. From the **Type** drop-down, select **UPPER**.
   1. Do **not** select the check box Keep Source Attributes
   1. Leave the **Name** as-is.
   1. Click **Apply**.

![The content is described above.](images/image.071.png)

1. An **Expression operator** is added to the data flow. In the Properties panel, the Details tab is now in focus, showing the expression details. You can see the generated expression, UPPER(EXPRESSION\_1.CUSTOMERS\_JSON.STATE\_PROVINCE), in the Expressions table.

![The content is described above.](images/image.072.png)

1. With the new **EXPRESSION\_1** operator selected in the data flow, in the Properties panel, change the name in Identifier to **CHANGE\_CASE**. *Note*: Be sure to save often during design time!

![The content is described above.](images/image.073.png)

1. Click the **Data** tab, and then use the horizontal scrollbar to scroll to the end. **EXPRESSION\_1.STATE\_PROVINCE** is added to the end of the dataset. You can preview the transformed data for EXPRESSION\_1.STATE\_PROVINCE in the Data tab.

![The content is described above.](images/image.074.png)

1. From the Operators panel, drag and drop a **new Expression** operator onto the canvas after **CHANGE\_CASE** operator. **Connect CHANGE\_CASE to the new Expression**.

![The content is described above.](images/image.075.png)

1. With **EXPRESSION\_1** selected, in the Properties panel, change the **Identifier** to **CONCAT\_FULL\_NAME** and then click **Add Expression** button in the Expressions table.

![The content is described above.](images/image.076.png)

1. In the **Add Expression** panel:
   1. Rename the expression to FULLNAME in the **Identifier** field.
   1. Keep **Data Type** as VARCHAR.
   1. Set **Length** to 200.
   1. Under Expression Builder, switch from the Incoming list to the **Functions list**.
   1. In the **filter by name search field**, enter CON. Then locate CONCAT under String. You can either search for CONCAT in the functions list yourself, or enter CON to use the auto-complete functionality
   1. Enter

**CONCAT**(CONCAT(EXPRESSION\_1.CUSTOMERS\_JSON.FIRST\_NAME, ' '),EXPRESSION\_1.CUSTOMERS\_JSON.LAST\_NAME)

in the **expression box**. You can also highlight a function's placeholders and then double-click or drag and drop attributes from the Incoming list to create an expression.

1. Click **Add**.

![The content is described above.](images/image.077.png)

1. The new expression is now listed in the **Expression operator**. You can add as many expressions as you want. *Note*: Be sure to save often during design time!

![The content is described above.](images/image.078.png)

1. After you apply filters and transformations, you can join the source data entities using a unique customer identifier, and then load the data into a target data entity. To join the data from expression **CONCAT\_FULL\_NAME** with the data from **FILTER\_1**, drag and drop a **Join operator** from the Operators panel onto the canvas next to CONCAT\_FULL\_NAME and FILTER\_1. Connect CONCAT\_FULL\_NAME to JOIN\_1 and then connect FILTER\_1 to JOIN\_1.

![The content is described above.](images/image.079.png)

1. Select the **JOIN\_1** operator. **Inner Join** as the join type is selected by default. In the Details tab of the Properties panel, click **Create** next to **Join Condition**.

![The content is described above.](images/image.080.png)

1. In the **Create Join Condition panel**:
   1. Enter CUST in the filter by name search field.
   1. You want to join the entities using CUST\_ID and CUST\_KEY. In the editor, enter

**JOIN\_1\_1**.CUSTOMERS\_JSON.CUST\_ID=JOIN\_1\_2.REVENUE\_CSV.CUST\_KEY

1. Click **Create**.

![The content is described above.](images/image.081.png)

1. Your **Join operator properties** should now look like this:

![The content is described above.](images/image.082.png)

1. From the Operators panel, drag and drop a **Target operator** onto the canvas. Connect JOIN\_1 to TARGET\_1. *Note*: Be sure to save often during design time!

![The content is described above.](images/image.083.png)

1. Select **TARGET\_1** operator on the canvas. The details for this operator are now displayed in the **Properties** bar.

![The content is described above.](images/image.084.png)

1. In the **Details** tab of the Properties panel complete the fields accordingly:
   1. Leave the default value for **Integration Strategy** as **Insert**.
   1. For **Data Asset**, select Data\_Warehouse.
   1. For **Connection**, select Beta Connection.
   1. For **Schema**, select BETA.
   1. For **Data Entity**, select CUSTOMERS\_TARGET.![The content is described above.](images/image.085.png)
   1. For **Staging Location**, select the **Object Storage data asset**, its **default connection** and your **compartment**. Then for **Schema**, select the **Object Storage bucket** that you created before importing the sample data in *Setting up the Data Integration prerequisites in OCI*. Click **Select**.![The content is described above.](images/image.086.png)
1. The properties details for **CUSTOMERS\_TARGET operator** should now look like this:

![The content is described above.](images/image.087.png)

1. To review the Attributes mapping, click the **Map tab**. By default, all attributes are **mapped by name**. For example, CUST\_ID from JOIN\_1 maps to CUST\_ID in the target data entity.

![The content is described above.](images/image.088.png)

1. To manually map attributes that are not yet mapped, click the **All** drop-down in the Target attributes table, and then select **Attributes not mapped**. You can do the same in the Source attributes table (for the incoming fields). You can see that there is one attribute that is not mapped, more specifically attribute FULL\_NAME from target.

![The content is described above.](images/image.089.png)

1. Now drag and drop **FULLNAME** under Source attributes to **FULL\_NAME** under Target attributes. All attributes from target are now mapped.

![The content is described above.](images/image.090.png)

1. Click **View Rules** to filter and view the applied Rules.

![The content is described above.](images/image.091.png)![The content is described above.](images/image.092.png)

1. You have now completed the data flow. Click on **Validate** to see the validation output. There shouldn't be any warnings or errors.

![The content is described above.](images/image.093.png)

1. To save the data flow, click **Save**.

![The content is described above.](images/image.094.png)
## **Task 4: Create a Data Flow - 2**
To further explore the capabilities of Data Flows in OCI Data Integration, you will now create **a new Data Flow** with different transformation rules.

This Data Flow will load data from **multiple source files** containing Employees data using File Patterns functionality in OCI Data Integration. After, you will do transformations on the Employees data and later load the data in **multiple target tables**, based on the region of the employees. Two target tables will be loaded: one for employees from **West and Midwest region** and one for employees from **Northeast and South region**. We will take advantage of the **Split operator** in OCI Data Integration Data Flows.

1. From the Project Details page for DI\_Workshop project, click on **Data Flows** from the submenu.

![The content is described above.](images/image.037.png)

1. Click **Create Data Flow**.

![The content is described above.](images/image.095.png)

1. The data flow designer opens in a new tab. In the **Properties panel**, for **Name**, enter Load Employees by Region, and click **Save**.

![The content is described above.](images/image.096.png)![The content is described above.](images/image.097.png)

1. You will add your **Source operator**. You add source operators to identify the data entities to use for the data flow. From the Operators panel on the left, drag and drop a Source operator onto the canvas.

![The content is described above.](images/image.098.png)

1. On the canvas, select **SOURCE\_1** operator. The Properties panel now displays the details for this operator.

![The content is described above.](images/image.099.png)

1. In the **Details** tab, click Select next to each of the following options to make your selections:
   1. For **Identifier**, rename to EMPLOYEES\_SOURCE\_FILES.
   1. For **Data Asset**, select Object\_Storage.
   1. For **Connection**, select Default Connection.
   1. For **Schema**, select your **compartment** and then your **bucket**. For the purposes of this tutorial, **Object Storage** serves as the source data asset, this is why you select your bucket here.![The content is described above.](images/image.099.png)
   1. For **Data Entity**, click on **Select** and then on **Browse by Pattern**.![The content is described above.](images/image.100.png)

Write the file pattern EMPLOYEES\_\* and click **Search**. All files from your Object Storage bucket that are found which match this pattern are now displayed: there are three files for employees. Click on **Select Pattern**.![The content is described above.](images/image.101.png)

For **File Type**, choose **CSV** and leave the defaults for the other fields that appear. Click **Select**.![The content is described above.](images/image.102.png)

In the end, your details for the source operator should look like this.![The content is described above.](images/image.103.png)

1. Drag and drop a **Distinct operator** on the data flow canvas. We use the distinct operator to return distinct rows with unique values. Connect **EMPLOYEES\_SOURCE\_FILES** source to the **DISTINCT\_1** operator. *Note*: Be sure to save often during design time!

![The content is described above.](images/image.104.png)

1. Drag and drop an **Expression operator** on the data flow canvas. Connect the **DISTINCT\_1** operator to the new **Expression** operator.

![The content is described above.](images/image.105.png)

1. In the Properties panel for **EXPRESSION\_1** operator, rename the Identifier to **TRANSFORM\_DATAYPES**.

![The content is described above.](images/image.106.png)

1. You will now add a **new expression**. Still in the Properties panel, click on **Add Expression**.

![The content is described above.](images/image.107.png)

1. In the **Add Expression** panel:
   1. **Rename** the expression to BIRTH\_DATE in the Identifier field.
   1. Change **Data Type** to DATE.
   1. Enter

**TO\_DATE**(EXPRESSION\_1.EMPLOYEES\_SOURCE\_FILES.Date\_of\_Birth, 'MM/dd/yyyy')

in the **expression** box.

1. This function will covert the **STRING** value of birth date from the source files to a **DATE** data type value, in the specified format. You can also find this function in **Functions** tab, under **Date/Time** section and select it from there. Attributes can be added from **Incoming** tab, by highlighting a function's placeholders and then double-click or drag and drop attributes from the Incoming list to create an expression.
   1. Click **Add**.

![The content is described above.](images/image.108.png)

1. Your expression for **BIRTH\_DATE** is now displayed. Click again on **Add Expression** to add a new one.

![The content is described above.](images/image.109.png)

1. In the **Add Expression** panel:
   1. **Rename** the expression to YEAR\_OF\_JOINING in the Identifier field.
   1. Change **Data Type** to NUMERIC.
   1. Enter

**TO\_NUMBER**(EXPRESSION\_1.EMPLOYEES\_SOURCE\_FILES.Year\_of\_Joining)

in the **expression** box. This function will transform your string value of year of joining from the files to a number value.

1. Click **Add**.

![The content is described above.](images/image.110.png)

1. The expressions for the **TRANSFORM\_DATAYPES** operator should now look like this:

![The content is described above.](images/image.111.png)

1. Drag and drop an **Expression operator** on the data flow canvas. Connect the **TRANSFORM\_DATAYPES** operator to the new **Expression** operator. *Note*: Be sure to save often during design time!

![The content is described above.](images/image.112.png)

1. In the Properties panel for the new **EXPRESSION\_1 operator**, change the Identifier to **EMPLOYEE\_AGE\_AND\_PHONE**.

![The content is described above.](images/image.113.png)

1. You will now add a new expression. Still in the Properties panel, click on **Add Expression**.

![The content is described above.](images/image.114.png)

1. In the **Add Expression** panel:
   1. **Rename** the expression to EMPLOYEE\_AGE in the Identifier field.
   1. Change **Data Type** to NUMERIC.
   1. Enter

**CASE** **WHEN** DAYOFYEAR(CURRENT\_DATE)>=DAYOFYEAR(EXPRESSION\_1.TRANSFORM\_DATAYPES.BIRTH\_DATE) **THEN** TRUNC(**YEAR**(CURRENT\_DATE)-**YEAR**(EXPRESSION\_1.TRANSFORM\_DATAYPES.BIRTH\_DATE)) **ELSE** TRUNC(**YEAR**(CURRENT\_DATE)-**YEAR**(EXPRESSION\_1.TRANSFORM\_DATAYPES.BIRTH\_DATE)-1) **END**

in the **expression** box. This function will calculate the age of the employee, by doing a minus between the current date and his birth date. CASE WHEN function returns the value for which a condition is met.

*Note*: In case the attributes in the expression don't get automatically highlighted, please replace them, by highlighting in the expression's placeholders and then double-click or drag and drop attributes from the Incoming list.

1. Click **Add**.

![The content is described above.](images/image.115.png)

1. You will now add a new expression in the same operator. Still in the Properties panel, click on **Add Expression**.

![The content is described above.](images/image.116.png)

1. In the **Add Expression** panel:
   1. **Rename** the expression to PHONE\_NO in the Identifier field.
   1. Leave **Data Type** as VARCHAR.
   1. Enter

COALESCE(EXPRESSION\_1.EMPLOYEES\_SOURCE\_FILES.Phone\_No,'Phone Number Not Available')

in the **expression** box This function will fill in the null values for phone number with string Phone Number Not Available.

1. Click **Add**.

![The content is described above.](images/image.117.png)

1. The two expressions you defined for this operator are now displayed. Click on **Attributes** tab. *Note*: Be sure to save often during design time!

![The content is described above.](images/image.118.png)

1. Check the following two fields: **EMPLOYEES\_SOURCE\_FILES.Age\_in\_Yrs**, **EMPLOYEES\_SOURCE\_FILES.Year\_of\_Joining**. We will exclude these fields from this operator.

![The content is described above.](images/image.119.png)

1. Click on **Actions** and then on **Exclude by selection**.

![The content is described above.](images/image.120.png)

1. The fields are now excluded. Click on **View Rules** to see the rules you defined.

![The content is described above.](images/image.121.png)

1. Click on **Data** tab of the **EMPLOYEE\_AGE\_AND\_PHONE** operator.

![The content is described above.](images/image.122.png)

1. Scroll to the right until you get to the attribute **EMPLOYEE\_AGE\_AND\_PHONE.EMPLOYEES\_SOURCE\_FILES.Region**. Click on it and a **Data Profile** window will appear. You can observe that there is employee data from four regions: Northeast, West, South, Midwest. In this data flow you will split the employee data into two target tables based on the **region**: one target table for employees from **Northeast and South** region (table named EMPLOYEES\_NORTHEAST\_SOUTH) and one target table for employees from **West and Midwest** region (table named EMPLOYEES\_WEST\_MIDWEST).

![The content is described above.](images/image.123.png)

1. Drag and drop a **Split operator** on the data flow canvas. Connect the **EMPLOYEE\_AGE\_AND\_PHONE operator** to the new **Split operator**. Use the split operator to divide one source of input data into two or more output ports based on split conditions that are evaluated in a sequence. Each split condition has an output port. Data that satisfies a condition is directed to the corresponding output port. *Note*: Be sure to save often during design time!

![The content is described above.](images/image.124.png)

1. In the **Properties** bar of the Split Operator, we will leave the default **Identifier** (**SPLIT\_1**) and **Match** option (**First matching condition** means that data that matches the first condition should be removed from further processing by other conditions).

![The content is described above.](images/image.125.png)

1. Still in Properties bar of the Split Operator, click on **Add Condition** in **Split Conditions section**.

![The content is described above.](images/image.126.png)

1. In **Add Split Condition** page:
   1. Enter **Identifier** WEST\_MIDWEST\_REGION.
   1. For **Condition** enter

**SPLIT\_1**.EMPLOYEES\_SOURCE\_FILES.Region **IN** ('Midwest','West')

1. Click **Add**.

![The content is described above.](images/image.127.png)

1. The first split condition you defined is now displayed. The Split operator properties should look like this:

![The content is described above.](images/image.128.png)

1. Still in Properties bar of the Split Operator, click on **Add Condition** in **Split Conditions section** to add a new split condition.

![The content is described above.](images/image.129.png)

1. In **Add Split Condition** page:
   1. Enter **Identifier** NORTHEAST\_SOUTH\_REGION.
   1. For **Condition** enter

**SPLIT\_1**.EMPLOYEES\_SOURCE\_FILES.Region **IN** ('Northeast','South')

1. Click **Add**.

![The content is described above.](images/image.130.png)

1. The split conditions that you defined are now displayed. After the conditions in the split operator are evaluated during run-time, data that does not meet the condition is directed to the **Unmatched** output port.

![The content is described above.](images/image.131.png)

1. Drag and drop a **target operator**. Connect the **WEST\_MIDWEST\_REGION** output of the Split operator to the **TARGET\_1** operator. *Note*: Be sure to save often during design time!

![The content is described above.](images/image.132.png)

1. In the properties for **TARGET\_1** operator:
   1. Change to **Merge Integration Strategy**.
   1. For **Data Asset**, select Data\_Warehouse.
   1. For **Connection**, select Beta connection.
   1. For **Schema**, select Beta.
   1. For **Data Entity**, select EMPLOYEES\_WEST\_MIDWEST (this target table was created with the SQL script from *Setting up the Data Integration prerequisites in Oracle Cloud Infrastructure* that you ran on the Autonomous Data Warehouse).
   1. For **Staging Location**, select your **Object Storage bucket** (DI-bucket).
   1. **Merge Key** will automatically get populated with the primary key name of the table, from the database.

![The content is described above.](images/image.133.png)

1. Go to **Map** tab of the **EMPLOYEES\_WEST\_MIDWEST** target operator. There are 3 attributes that were not mapped automatically in the target.

![The content is described above.](images/image.134.png)

1. **Manually map** the **E\_Mail** attribute from source to **EMAIL** attribute from target, with drag and drop.

![The content is described above.](images/image.135.png)

1. You will use **mapping by pattern** to map the two remaining unmapped attributes. This maps inbound attributes to target attributes based on simple, user-defined regex rules. Click on **Actions** button and then on **Map by pattern**.

![The content is described above.](images/image.136.png)

1. In the **Map by pattern** page that pops up:
   1. For **Source Pattern**, use \*\_S\_NAME.
   1. For **Target Pattern**, use $1S\_NAME.
   1. Click on **Preview Mapping**. In the table, the mapping for FATHERS\_NAME and MOTHERS\_NAME attributes is now displayed.
   1. Click on **Map**.

*Note:* For more information on how to use **Mapping by pattern**, please see the following [link](https://docs.oracle.com/en-us/iaas/data-integration/using/using-operators.htm#operator-target), section Target Operator, **Mapping attributes**.

![The content is described above.](images/image.137.png)

1. The attribute mapping for the **EMPLOYEES\_WEST\_MIDWEST target table** is now complete. *Note*: Be sure to save often during design time!

![The content is described above.](images/image.138.png)

1. Drag and drop **another target operator**. Connect the **NORTHEAST\_SOUTH\_REGION output port** of the Split operator to the **TARGET\_1 operator**. In Properties tab of the new target operator:
   1. Change to **Merge Integration Strategy**.
   1. For **Data Asset**, select Data\_Warehouse.
   1. For **Connection**, select Beta connection.
   1. For **Schema**, select Beta.
   1. For **Data Entity**, select EMPLOYEES\_NORTHEAST\_SOUTH (this target table was created with the SQL script from *Setting up the Data Integration prerequisites in OCI* that you ran on the Autonomous Data Warehouse).
   1. For **Staging Location**, select your **Object Storage bucket** (DI-bucket)
   1. **Merge Key** will automatically get populated with the primary key name of the table, from the database.

**Make sure you also map all of the columns, same as in steps 38, 39 and 40.**

![The content is described above.](images/image.139.png)

1. The design of the Data Flow is now ready. Click on **Validate**. The Validation panel lets you know if any warnings or errors were detected. *Note*: If any warnings or errors are found, select an issue and it'll take you to the operator that caused it, to investigate further. Warnings that might be displayed should not cause the task to fail.

![The content is described above.](images/image.140.png)

1. Click on **Save and Close**.

![The content is described above.](images/image.141.png)

**Task 5: Create Integration Tasks**

**Integration tasks** in OCI Data Integration let you take your data flow design and choose the parameter values you want to use at runtime. With the help of Integration Tasks, you can create multiple Tasks with distinct configurations for the same Data Flow. You will create Integration tasks for the two Data Flows you created in the previous steps.

1. From your Workspace home page of OCI Data Integration, click **Open tab** (plus icon), and then select **Projects**.

![The content is described above.](images/image.142.png)

1. On the **Projects** page, select the project you have been working on for this workshop, DI\_Workshop.

![The content is described above.](images/image.143.png)

1. On the DI\_Workshop **Project Details** page, from the submenu, click **Tasks**.

![The content is described above.](images/image.144.png)

1. Click **Create Task**, and then select **Integration**.

![The content is described above.](images/image.145.png)

1. The **Create Integration Task** page opens in a new tab. On this page:
   1. Change the **Name** to Load Customers Lab and enter an optional **Description**. The value in the **Identifier** field is auto-generated based on the value you enter for Name.![The content is described above.](images/image.146.png)
   1. In the Data Flow section, click Select.![The content is described above.](images/image.147.png)
   1. In the **Select a Data Flow** panel, select Load Customers and Revenue Data, and then click Select.![The content is described above.](images/image.148.png)
   1. The Data Flow will be **validated** after the selection and the result should be displayed as **Successful**.
   1. Click **Create and Close**.

![The content is described above.](images/image.149.png)

1. From the DI\_Workshop project section **Tasks**, you will now create an Integration Task for your second Data Flow. Click **Create Task** and then select **Integration**.

![The content is described above.](images/image.145.png)

1. The **Create Integration Task** page opens in a new tab. On this page:
   1. Change the **Name** to Load Employees by Regions and enter the optional **Description**. The value in the **Identifier** field is auto-generated based on the value you enter for Name.
   1. In the Data Flow section, click Select. In the **Select a Data Flow** panel, select Load Employees by Region, and then click Select.
   1. The Data Flow will be **validated**.
   1. Click **Create and Close**.

![The content is described above.](images/image.150.png)

**Task 6: Create a SQL task**

A **SQL task** lets you run a SQL stored procedure in pipeline. You create a SQL task by selecting a stored procedure that exists in the data source that's associated with a data asset already created in your workspace. The variables defined in a stored procedure are exposed as input, output, and in-out parameters in a SQL task.

When you create a SQL task, you can configure values for **input parameters** only. If input parameters are configured in a SQL task, you can **override the default values** when you configure the SQL task in a pipeline, and when you run a pipeline that includes the SQL task.

The SQL task that you create will write inside a statistics table on the Autonomous Data Warehouse (DWH\_LOAD\_STATS) the successful/ unsuccessful result of a Pipeline task run based on input parameter from the pipeline, but also the pipeline name and task run key. This SQL task will be included in a Pipeline in *Create an Application, a Pipeline and publish tasks*. To understand better the SQL stored procedure, please check the OCIDI\_RESULT procedure statement from the SQL script you downloaded and ran on Autonomous Data Warehouse in *Setting up the Data Integration prerequisites in OCI*. Any user interested in seeing the successful/ unsuccessful result of the Data Integration Pipeline along with the pipeline name and task run key will be able to either do it in the database by querying the DWH\_LOAD\_STATS table, or by checking the result in the Data Integration Application from OCI Console.

1. From your Workspace home page in OCI Data Integration, click **Open tab** (plus icon), and then select **Projects**.

![The content is described above.](images/image.151.png)

1. On the **Projects** page, select the project you have been working on for this workshop, DI\_Workshop.

![The content is described above.](images/image.143.png)

1. On the DI\_Workshop **project details** page, from the submenu, click **Tasks**.

![The content is described above.](images/image.144.png)

1. Click **Create Task**, and then select **SQL**.

![The content is described above.](images/image.152.png)

1. On the **Create SQL Task** page, enter:
   1. Name: Use Procedure DWH Load Stats. *Note*: The Identifier field is a system-generated value based on what you enter for Name. You can change the value, but after you save the task, you cannot change the value again.
   1. **Description** (optional).
   1. Project **DI\_Workshop** is auto-populated because we're creating this task from project details page.

![The content is described above.](images/image.153.png)

1. In the **SQL** section, click **Select**.

![The content is described above.](images/image.154.png)

1. In the **Select SQL** page:
   1. **Data Asset**: Data\_Warehouse.
   1. **Connection**: Choose the Beta Connection.
   1. **Schema**: BETA schema on your ADW.
   1. **Stored Procedure**: Choose the OCIDI\_RESULT procedure. *Note*: The OCIDI\_RESULT procedure was created in the Autonomous Data Warehouse during "Setting up the Data Integration prerequisites in OCI." It writes into DWH\_LOAD\_STATS target table a new entry in case of success or failure.

![The content is described above.](images/image.155.png)

1. **Review** the list selections for the SQL task, then click **Done**.

![The content is described above.](images/image.156.png)

1. In the **Configure Parameters** section, click **Configure** to view or configure values for the stored procedure parameters.

![The content is described above.](images/image.157.png)

1. In the **Configure Stored Procedure Parameters** page, review the list of parameters in the stored procedure. Only **input parameters** can be configured. You can see here the input parameters **IN\_DI\_RESULT** and **PIPELINE\_NAME\_TASK\_RUN** from the procedure you're using.
   1. In the row of the input parameter value for IN\_DI\_RESULT, click **Configure**.![The content is described above.](images/image.158.png)
   1. In the Edit Parameter panel, enter value **SUCCESS** (without any apostrophes) for that input parameter and click Save Changes.![The content is described above.](images/image.159.png)
   1. In the row of the input parameter value for PIPELINE\_NAME\_TASK\_RUN, click **Configure**.![The content is described above.](images/image.160.png)
   1. In the Edit Parameter panel, enter value **DEFAULT** (without any apostrophes) for that input parameter and click Save Changes.![The content is described above.](images/image.161.png)
   1. Click **Done**.![The content is described above.](images/image.162.png)
1. In the **Validate Task** section, click **Validate** to check for errors and warnings in the configured parameter values. When validation is completed, a **Successful** message should appear near Validation.

![The content is described above.](images/image.163.png)

1. Click **Save and Close**.

![The content is described above.](images/image.164.png)

**Congratulations!** You created the Data Flows, Integration tasks, Data Loader task and SQL tasks in OCI Data Integration.

