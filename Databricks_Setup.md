# Databricks Setup
----

## Introduction
This document details the steps followed to complete the setup in Databricks. 

> [!NOTE]
> The steps below are done in **Azure**.

## Step 1: Creating an Azure Account
You should note that Databricks runs on Azure. This means that you should first create an account on Azure. To do that, follow the link below:
* https://azure.microsoft.com/en-us/pricing/purchase-options/azure-account

After creating your account, access the Azure Portal to manage your resources.

## Step 2: Creating a Resource Group
* Search for `resource group` in the search bar. 
* Select it and click on Create. 
* Give it a meaningful name

### Step 3: Creating a Databricks Workspace
In the Azure Portal,  
* Search for Azure Databricks and create a new workspace.
* Select the resource group you just created.
* Input the Workspace name.
* Choose the region (East US recommended if you do not know what to put.)
* Choose the Pricing Tier: Premium (+ Role-based access controls)
* Go to the Networking tab and select no for both questions.
* Review and Create

> [!NOTE]
> Whenever asked for a region, you should input the same region you used while creating your workspace.

### Step 4: Creating a Storage Group
* Select the resource group.
* Give a name to the storage group. This should be unique and in lowercase.
* Select Standard
* Tick `Enable hierarchical namespace`.
* Leave the rest as is.
* Click on `Next`.
* Click on `Review and Create`, then on `Create`.

### Step 5: Creating a Container
This is done under your storage account. Proceed as follows:  
* Under `Data Storage`, select `Containers`.
* Click on Create and give it a name.
* Open the container you just created and create a directory. This is where you will upload your dataset. You can also create a subdirectory inside your directory.
* Upload your dataset into the directory or subdirectory.
* Confirm that the directory structure is correctly created and accessible.


When all the above are completed, you can now launch your workspace.
* Go to Home -> Resource
* Find the Databricks workspace you created earlier.
* Click on `Launch Workspace`.
* This opens Databricks in a new page on your browser.

> [!NOTE]
> The steps below are done in **Databricks**.

## Step 1: Creating a Spark Cluster
In Databricks,  
* Click on `Compute`.
* Click on `Create` on the top right of your screen.
* Change the name if needed.
* Choose the `Single node`.
* Select the runtime: `13.3 LTS (Scala 2.12 Spark 3.4.1)` or `14.3 LTS (Scala 2.12 Spark 3.5.0)`. This is to bring the compute price to `0.75 DBU/h`.
* Uncheck `Use Photon Acceleration`.
* Select the Node Type: `Standard_D4s_v3 16 GB Memory, 4 Cores`
* Terminate after `30` minutes of inactivity.

> [!WARNING]
> Always ensure that you are running your work on your cluster and NOT the serverless.
> This is to avoid tremendous billing on your Azure account.

## Step 2: Creating a Folder and Running Your First Notebook
* On the top right of your screen, click on `Create` and select `Folder`. Give it a name and create it.
* Load a sample data.
* Select the folder you just created. Click again on Create and select `Notebook`. 
* Create a notebook and give it a name.
* Write & execute basic Spark SQL or Python commands.  

Below is an example  

![Example](https://github.com/Songonge/Collaboration-Databricks/blob/main/Example.png)

Go back to Azure
* Copy the ID of the connector under `databricks-access-connector`.
* Go back to Databricks.
* Click on `Catalog` -> `External data` -> `Credentials` -> `Create credentials`.
* Paste the ID you just copied from Azure.  

## Step 3: Creating a Databricks Access Connector
In the Azure Portal, search for `Databricks Access Connector`.  
* Select `Access connector for Azure Databricks` -> databricks-access-connector
* Click Create -> Assign it to the appropriate Resource Group
* Input the name and region. Here, you can use default settings or configure as needed
* Click Review + Create -> Create
* Copy and keep the Resource ID

## Step 4: Granting Access to the Storage Account
This is done using Managed Identity. Proceed as follows:  
* Navigate to the Storage Account -> Container (your container you created) -> Access Control (IAM)
* Click on `Add` -> Select `Add Role Assignment`.
* Search for `Storage Blob Data Contributor`. and select it. This will be highlighted in Grey.
* Assign the role to the Managed Identity of the Databricks Access Connector.
* Click on `Next` -> Managed identity -> Select `Managed identities` -> Subscription -> Managed identity. 
* Click Save.

## Step 5: Connecting External Storage from Databricks
This is done using the Resource ID. Proceed as follows:  
* In Databricks, use the Resource ID of the Access Connector
* Configure access using credentials passthrough or workspace settings
* No need to mount storage manually
* Validate access within your notebook


## Step 6: This is in GitHub
* Create a repository and add a README.

Go back to Databricks:  
* Create a folder under Repos.
* Create a Git folder by clicking on `Create` and selecting `Repo`.

In GitHub:
* Click on your picture on the top right of your screen.
* Click on `Settings`.
* Locate `Developer Settings` and click on it.
* Click on `Personal Access Tokens`.
* Select `Tokens Classic`.
* Generate a token if you do not have one.
* Copy it somewhere.

## Step 7: In Databricks
* Click on your name at the top right.
* Select Settings -> Linked Accounts -> Add Git Credentials -> Personal Access Tokens.
* Paste the token
* Click on `Save`  

* Create a branch
  * Click on `main`.
  * Click on Create branch.
  * Name your branch -> Create.

> [!NOTE]
> It is advised to always work in a secondary branch instead of the main branch.
> This is where you can do all your testing before sending it to a third-party person who is responsible for deploying your work in the main branch.

## Connecting Power BI to Databricks
It is possible to connect Databricks to Power BI. Follow the steps below to connect.

In Databricks:  
1. Log in to your Azure Portal.
2. Launch your Databricks Workspace.
3. Once your Databricks page opens, click on **Marketplace**.
4. Type **Power BI** in the `Search for products bar`.
5. Select Power BI Desktop.
6. Click on the Connect button at the top right of your screen. This opens a side window.
7. Click on `Download the connection file` and save it on your computer.
8. Locate the file on your computer and open it. It will launch Power BI, and a small pop-up window will appear.  

In Power BI:  
1. Select `Azure Active Directory` and sign in.
2. When you are done signing in, click on `Connect`.
3. Now you are good to go.  

When these steps are completed, any dataset uploaded to Databricks will be accessible in Power BI.

> [!IMPORTANT]
> For the above steps to work, you should ensure you have a Power BI Desktop version installed on your computer.
> You can also use Tableau if you do not have Power BI. Either one you select should be installed on your computer.






















