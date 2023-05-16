# Create an Application, a Pipeline and publish tasks
## **Introduction**
Learn how to create an OCI Data Integration **application**, **publish tasks** into the application and create a Data Integration **pipeline** which calls the published tasks.

The Pipeline you will create will orchestrate the execution of all of the tasks you created and published in *Create a Data Loader task, two Data Flows, Integration tasks and a SQL task*. It will load and transform Customers, Revenues and Employees data and populate a statistics table in the Autonomous Data Warehouse with the success/error result of the Pipeline, along with the pipeline name and task run key.

**Estimated Time**: 30 minutes
### **Objectives**
- Create an Application
- Publish tasks to Application
- Creating a Pipeline which calls the published tasks
- Creating a Pipeline Task
- Publish the Pipeline Task

Collapse All Tasks
## **Task 1: Create an Application**
In OCI Data Integration, an **Application** is a container for published tasks, data flows, and their dependencies. You can run published tasks in an Application for testing, or roll them out into production.

1. In the Oracle Cloud Infrastructure Console navigation menu, navigate to **Analytics & AI**. Under Data Lake, click **Data Integration**.

![The content is described above.](images/image.165.png)

1. From the Workspaces page, make sure that you are in the compartment you created for data integration (DI-compartment). Click on your **Workspace** (DI-workspace).

![The content is described above.](images/image.166.png)

1. On the workspace Home page, in the **Quick Actions tile**, click **Create Application**.

![The content is described above.](images/image.167.png)

1. On the Applications page, enter Workshop Application for **Name**. You can optionally give a short **Description** for your application, then click **Create**.

![The content is described above.](images/image.168.png)

1. The **Application Details page** for Workshop Application opens in a new tab.

![The content is described above.](images/image.169.png)
## **Task 2: Publish tasks to Application**
In Oracle Cloud Infrastructure Data Integration, a **Task** is a design-time resource that specifies a set of actions to perform on data. You create tasks from a project details or folder details page. You then publish the tasks into an Application to test or roll out into production.

You will publish into the Workshop Application all of the tasks that you have created in *Create a Data Loader task, two Data Flows, Integration tasks and a SQL task*.

1. From the Application Details you are currently in, click on **Open tab** (plus icon) in the tab bar and select **Projects**.

![The content is described above.](images/image.170.png)

1. Select your DI\_Workshop project from the projects list.

![The content is described above.](images/image.171.png)

1. In the **Tasks** list, **check all of the four tasks** you created in *Create a Data Loader task, two Data Flows, Integration tasks and a SQL task*.

![The content is described above.](images/image.172.png)

1. Click on **Publish to Application** button.

![The content is described above.](images/image.173.png)

1. In the Publish to Application dialog, select Workshop Application and then click **Publish**.

*Note*: You can modify the tasks or edit the data flow without impacting the published task. This enables you to test a version of your data flow, while working on some new changes.

![The content is described above.](images/image.174.png)

1. You can now go to your Workshop Application to see your published task. On your workspace Home page, click **Open tab** (plus icon) in the tab bar, select **Applications**.

![The content is described above.](images/image.175.png)

1. Select you Workshop Application from the list of applications.

![The content is described above.](images/image.176.png)

1. From the landing page of Workshop Application, click on **Patches**. A patch contains updates to published tasks in an Application. When you publish a task to an Application or unpublish a task, a patch is created in the Application. If you publish a group of tasks at the same time, only one patch is created. You should now see the patch that was created for the tasks you are publishing, with the status **In Progress**.

![The content is described above.](images/image.177.png)

1. Click on the **Refresh** button for Patches. After a short time, the status of the patch should be displayed as **Success**.

![The content is described above.](images/image.178.png)

1. Click on **Tasks** tab under Details. You can now see the **list of published tasks** inside your Workshop Application.

![The content is described above.](images/image.179.png)
## **Task 3: Create a Pipeline**
A **pipeline** is a set of tasks connected **in a sequence** or **in parallel** to facilitate data processing. It manages and orchestrates the execution of a set of related tasks and processes. The pipeline functionality in Oracle Cloud Infrastructure Data Integration helps write complex data pipelines using published tasks from any application, and you can add data loader, integration or SQL tasks. You can create pipelines quickly using a designer similar to the Data Flow designer.

The Pipeline you will create in this step will orchestrate the execution of all of the tasks you created and published in this Workshop until now. The pipeline will begin with the **parallel execution** of the LOAD\_CUSTOMERS\_LAB **Integration Task** and LOAD\_REVENUE\_DATA\_INTO\_DATA\_WAREHOUSE **Data Loader task**. After the successful execution of these two tasks, the LOAD\_EMPLOYEES\_BY\_REGIONS **Integration Task** will be executed in sequence. Then, an **Expression operator** will add a new field that is populated with the Pipeline name and Task run key **system parameters of the pipeline**. The following **SQL task** step will get success/error input configured in the pipeline and the system parameters expression as the **Input parameters**. It will load this information in the Autonomous Data Warehouse, according to the SQL stored procedure logic.

Any user interested in seeing the successful/ unsuccessful result of the Data Integration Pipeline along with the pipeline name and task run key will be able to either do it in the database by querying the DWH\_LOAD\_STATS table, or by checking the result in the Data Integration Application from OCI Console.

1. From the OCI Data Integration Workspace home page, click on **Open tab** (plus icon) in the tab bar and select **Projects**.

![The content is described above.](images/image.180.png)

1. Select your DI\_Workshop project from the projects list.

![The content is described above.](images/image.181.png)

1. Select **Pipelines** section under project Details tab.

![The content is described above.](images/image.182.png)

1. Click on **Create Pipeline**.

![The content is described above.](images/image.183.png)

1. The **canvas for designing the Pipeline** is now displayed. The **start and end operators** are already added by default to the canvas. You will start by renaming the Pipeline. Under Properties for the Pipeline, on Details section, currently the name is New Pipeline. **Rename** to Load DWH Pipeline.

![The content is described above.](images/image.184.png)

1. Click on **Save** button. The title of the pipeline will change to the pipeline name you have just added.

![The content is described above.](images/image.185.png)

1. To add a task, you will drag and drop a task operator from the Operators Panel. Start with the drag and drop of an **Integration task**. Connect **START\_1** operator to the **Integration task** you added.

![The content is described above.](images/image.186.png)

1. In the Properties tab for **INTEGRATION\_TASK\_1**, Details section, click on Select to choose a published Integration task from your Application.

![The content is described above.](images/image.187.png)

1. A page pops up with the selections for the **Integration Task**:
   1. The **Compartment** with your OCI Data Integration resources is already selected.
   1. The **Workspace** you are currently working in is already selected.
   1. For **Application**, make sure you select the Workshop Application.
   1. Under **Integration Task**, check the Load Customers Lab task.
   1. Click **Select**.

![The content is described above.](images/image.188.png)

1. In the properties bar, the **Integration Task** Load Customers Lab is now selected. The Identifier has automatically changed with the name of Integration Task you selected. For Incoming Link Condition, leave the default option of **Always run**. *Note*: Be sure to save often during design time!

![The content is described above.](images/image.189.png)

1. Drag and drop a **Data Loader** component into the Pipeline canvas. We want this task to be run **in parallel** with the Integration task we have just defined, so connect **START\_1** operator with the **Data Loader task operator**.

![The content is described above.](images/image.190.png)

1. On the Properties tab for **DATA\_LOADER\_TASK\_1**, Details section, click on Select to choose a **published Data Loader task from your Application**.

![The content is described above.](images/image.191.png)

1. A page pops up with the selections for the **Data Loader Task**:
   1. The **Compartment** with your OCI Data Integration resources is already selected.
   1. The **Workspace** you are currently working in is already selected.
   1. For **Application**, make sure you select the Workshop Application.
   1. Under **Data Loader Task**, check the Load Revenue Data into Data Warehouse task.
   1. Click **Select**.

![The content is described above.](images/image.192.png)

1. In the properties bar, the **Data Loader Task** Load Revenue Data into Data Warehouse is now selected. The Identifier has automatically changed with the name of Data Loader Task you selected. For Incoming Link Condition, leave the default option of **Always run**.

![The content is described above.](images/image.193.png)

1. For these two tasks to run **in parallel**, you will now add a **merge operator**. Drag and drop the Merge operator on the canvas, then connect the two tasks (LOAD\_CUSTOMERS\_LAB and LOAD\_REVENUE\_DATA\_INTO\_DATA\_WAREHOUSE) to the MERGE\_1 operator.

![The content is described above.](images/image.194.png)

1. Under the Details tab of the **Properties** panel of the **MERGE\_1** operator, you can enter a name and optional description. Change the name to MERGE\_SUCCESS. For Merge Condition select the **All Success** option, which means that all parallel operations that are linked upstream must complete and succeed before the next downstream operation can proceed. *Note*: Be sure to save often during design time!

![The content is described above.](images/image.195.png)

1. Drag and drop an **Integration task** to the pipeline canvas. Connect **MERGE\_1** operator to the Integration task you added.

![The content is described above.](images/image.196.png)

1. On the Properties tab for **INTEGRATION\_TASK\_1**, Details section, click on Select to choose a published Integration task from your Application. This integration task will run **in sequence** after the successful run of the previous parallel tasks.

![The content is described above.](images/image.187.png)

1. A page pops up with the selections for the **Integration Task**:
   1. The **Compartment** with your OCI Data Integration resources is already selected.
   1. The **Workspace** you are currently working in is already selected.
   1. For **Application**, make sure you select the Workshop Application.
   1. Under **Integration Task**, check the Load Employees by Regions task.
   1. Click **Select**.

![The content is described above.](images/image.197.png)

1. In the properties bar, the **Integration Task** Load Employees by Regions is now selected. The Identifier has automatically changed with the name of Integration Task you selected. For Incoming Link Condition, leave the default option of **Run on success of previous operator**.

![The content is described above.](images/image.198.png)

1. Drag and drop an **Expression** operator to the pipeline canvas. A pipeline expression operator lets you create new, derivative fields in a pipeline, similar to an expression operator in a data flow. **Connect the Expression operator** to the **LOAD\_EMPLOYEES\_BY\_REGIONS** integration task.

![The content is described above.](images/image.199.png)

1. In the **Properties** bar of **EXPRESSION\_1** operator, change the Identifier to **PIPELINE\_NAME\_TASK\_RUN** and click on **Add** under Expression. *Note*: Be sure to save often during design time!

![The content is described above.](images/image.200.png)

1. This **Expression** will create a new field based on the **System Defined Parameters** of the pipeline. Generated system parameter values can be used in expressions but the values cannot be modified. For more information on System parameters in OCI Data Integration pipeline, please see this [link](https://docs.oracle.com/en-us/iaas/data-integration/using/pipeline-parameters.htm#parameter-types-pipeline__system-defined-parameters). The expression will concatenate the **PIPELINE\_NAME** system parameter with the **TASK\_RUN\_KEY** system parameter, and the new field will later on be used in the pipeline as input parameter for SQL task.

In the **Add Expression** panel:

1. Enter name PIPELINE\_NAME\_RUN in the **Identifier** field.
1. Leave the default VARCHAR **Data Type** and default **Length**.
1. Copy the following expression and paste it in the **Expression Builder** box. This expression concatenates the PIPELINE\_NAME system parameter with a space character and the TASK\_RUN\_KEY system parameter.

CONCAT(CONCAT(${SYS.PIPELINE\_NAME}, ' '),${SYS.TASK\_RUN\_KEY})

*Note*: You can also manually create the expression in the Expression Builder, by double-click or drag an drop of the System defined parameters and CONCAT function.

1. Click **Add**.

![The content is described above.](images/image.201.png)

1. Drag and drop a **SQL task** operator to the pipeline canvas. Connect the SQL task operator to the **PIPELINE\_NAME\_TASK\_RUN** expression operator.

![The content is described above.](images/image.202.png)

1. On the Properties tab for **SQL\_TASK\_1**, Details section, click on Select to choose a **published SQL task from your Application**.

![The content is described above.](images/image.203.png)

1. A page pops up with the selections for the **SQL Task**:
   1. The **Compartment** with your OCI Data Integration resources is already selected.
   1. The **Workspace** you are currently working in is already selected.
   1. For **Application**, make sure you select the Workshop Application.
   1. Under **SQL Task**, check the Procedure DWH Load Stats task.
   1. Click **Select**.

![The content is described above.](images/image.204.png)

1. In the properties bar, the **SQL Task** Procedure DWH Load Stats is now selected. The Identifier has automatically changed with the name of SQL Task you selected. For Incoming Link Condition, leave the default option of **Run on success of previous operator**. *Note*: Be sure to save often during design time!

![The content is described above.](images/image.205.png)

1. In the properties bar, click on **Configuration** tab and then on Configure where you have **Incoming Parameters Configured: 0/2**.

![The content is described above.](images/image.206.png)

1. A window to **Configure Incoming Parameters** pops up. OCI Data Integration identified the **input parameters of your procedure** (OCIDI\_RESULT and PIPELINE\_NAME\_TASK\_RUN) from the SQL task. Click on **Configure** for the **IN\_DI\_RESULT** parameter.

![The content is described above.](images/image.207.png)

1. In the new windows that is displayed:
   1. Leave the **Assign a value** option checked. This means you will override the default value of this parameter.
   1. In Default value box, write **SUCCESS**.
   1. Click **Done**.

![The content is described above.](images/image.208.png)

1. In the Configure Incoming Parameters window, click on **Configure** for the **PIPELINE\_NAME\_TASK\_RUN** parameter.

![The content is described above.](images/image.209.png)

1. In the new windows that is displayed:
   1. Select **Previous Operator Output** option, to assign the value of an output from a previous operator step to the input.
   1. Check the box to select the PIPELINE\_NAME\_TASK\_RUN.PIPELINE\_NAME\_RUN field from the previous Expression operator. The SQL task will use the value from the Expression as the input parameter for the SQL task.
   1. Click **Done**.

*Note*: Be sure to save often during design time!![The content is described above.](images/image.210.png)

1. The two input parameters of the SQL task now have Configured values . Click **Configure**.

![The content is described above.](images/image.211.png)

1. In **Configuration tab**, the **Incoming Parameters** are now displayed as configured **(2/2)**.

![The content is described above.](images/image.212.png)

1. Drag and drop another **SQL task operator** to the pipeline canvas. Connect the SQL task operator to the **PIPELINE\_NAME\_TASK\_RUN** expression operator.

![The content is described above.](images/image.213.png)

1. On the Properties tab for **SQL\_TASK\_1**, Details section, click on Select to choose a **published SQL task from your Application**.

![The content is described above.](images/image.203.png)

1. A page pops up with the selections for the **SQL Task**:
   1. The **Compartment** with your OCI Data Integration resources is already selected.
   1. The **Workspace** you are currently working in is already selected.
   1. For **Application**, make sure you select the Workshop Application.
   1. Under **Integration Task**, check the Procedure DWH Load Stats task.
   1. Click **Select**.

![The content is described above.](images/image.204.png)

1. In the properties bar, the **SQL Task** Procedure DWH Load Stats is now selected. The Identifier has automatically changed with the name of SQL Task you selected. For Incoming Link Condition, leave the default option of **Run on failure of previous operator**. The arrow from the previous operator to the new SQL task operator will turn **red**. *Note*: Be sure to save often during design time!

![The content is described above.](images/image.214.png)

1. In the properties bar, click on **Configuration** tab and then on Configure where you have **Incoming Parameters Configured: 0/2**.

![The content is described above.](images/image.215.png)

1. A window to **Configure Incoming Parameters** pops up. OCI Data Integration identified the **input parameters of your procedure** (OCIDI\_RESULT and PIPELINE\_NAME\_TASK\_RUN) from the SQL task. Click on **Configure** for the **IN\_DI\_RESULT** parameter.

![The content is described above.](images/image.207.png)

1. In the new windows that is displayed:
   1. Leave the **Assign a value** option checked. This means you will **override the default value of this parameter**
   1. In Default value box, write **ERROR**
   1. Click **Done**.

![The content is described above.](images/image.216.png)

1. In the Configure Incoming Parameters window, click on **Configure** for the **PIPELINE\_NAME\_TASK\_RUN** parameter. Click **Configure.**

![The content is described above.](images/image.217.png)

1. In the new windows that is displayed:
   1. Select **Previous Operator Output** option, to assign the value of an output from a previous operator step to the input.
   1. Check the box to select the PIPELINE\_NAME\_TASK\_RUN.PIPELINE\_NAME\_RUN field from the previous Expression operator. The SQL task will use the value from the Expression as the input parameter for the SQL task.
   1. Click **Done**.

![The content is described above.](images/image.210.png)

1. The two input parameters of the SQL task now have Configured values . Click **Configure**.

![The content is described above.](images/image.218.png)

1. In **Configuration tab**, the **Incoming Parameters** are now displayed as configured **(2/2)**.

![The content is described above.](images/image.212.png)

1. Connect the **two SQL tasks** to the **END\_1** operator. The final Pipeline should look like this:

![The content is described above.](images/image.219.png)

1. Click **Validate**. The result of the Global Validation should display no warnings and no errors.

![The content is described above.](images/image.220.png)

1. Click on **Save and Close**.

![The content is described above.](images/image.221.png)
## **Task 4: Create a Pipeline task**
Pipeline tasks let you take your pipeline design and choose the parameter values you want to use at runtime. You will create a Pipeline task for the pipeline you created in the above step.

1. On the DI\_Workshop Project Details page, from the submenu, click **Tasks**.

![The content is described above.](images/image.222.png)

1. Click **Create Task**, and then select **Pipeline**.

![The content is described above.](images/image.223.png)

1. On the **Create Pipeline Task** page, enter:
   1. For **Name** enter Load DWH Pipeline Task
   1. **Description** (optional)
   1. **Project** DI\_Workshop is auto-populated because we're creating this task from project details page.

![The content is described above.](images/image.224.png)

1. In the **Pipeline** section, click **Select**.

![The content is described above.](images/image.225.png)

1. In the **Select a Pipeline** panel, select the Load DWH Pipeline that this task will run. Then, click Select.

![The content is described above.](images/image.226.png)

1. After selecting the pipeline, it will automatically be validated. When you see the Validation message as **Successful**, click on **Save and Close**.

![The content is described above.](images/image.227.png)
## **Task 5: Publish the Pipeline task**
1. On the DI\_Workshop Project Details page, from the submenu, click **Tasks**.

![The content is described above.](images/image.222.png)

1. All tasks from the DI\_Workshop project will be displayed. Click on the **Actions menu** (three dots) for the Load DWH Pipeline Task. Then, click on **Publish to Application**.

![The content is described above.](images/image.228.png)

1. In the Publish to Application dialog, select the Workshop Application to publish to from the drop-down list. Then, click **Publish**.

![The content is described above.](images/image.229.png)

