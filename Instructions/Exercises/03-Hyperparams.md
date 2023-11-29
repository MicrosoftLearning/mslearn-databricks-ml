---
lab:
    title: 'Optimize Hyperparameters for machine learning in Azure Databricks'
---

# Optimize Hyperparameters for machine learning in Azure Databricks

In this exercise, you'll use the **Hyperopt** library to optimize hyperparameters for machine learning model training in Azure Databricks.

This exercise should take approximately **30** minutes to complete.

## Before you start

You'll need an [Azure subscription](https://azure.microsoft.com/free) in which you have administrative-level access.

## Provision an Azure Databricks workspace

An Azure Databricks workspace provides a central cloud-based environment for all your data science activities in Azure Databricks. You can create a workspace interactively in the Azure portal, use one you already have, or follow the steps below to use a script to provision a *Standard* workspace for this exercise.

> **Tip**: If you already have an Azure Databricks workspace, you can skip this procedure and use your existing workspace.

1. In a web browser, sign into the [Azure portal](https://portal.azure.com) at `https://portal.azure.com`.
2. Use the **[\>_]** button to the right of the search bar at the top of the page to create a new Cloud Shell in the Azure portal, selecting a ***PowerShell*** environment and creating storage if prompted. The cloud shell provides a command line interface in a pane at the bottom of the Azure portal, as shown here:

    ![Azure portal with a cloud shell pane](./images/cloud-shell.png)

    > **Note**: If you have previously created a cloud shell that uses a *Bash* environment, use the the drop-down menu at the top left of the cloud shell pane to change it to ***PowerShell***.

3. Note that you can resize the cloud shell by dragging the separator bar at the top of the pane, or by using the **&#8212;**, **&#9723;**, and **X** icons at the top right of the pane to minimize, maximize, and close the pane. For more information about using the Azure Cloud Shell, see the [Azure Cloud Shell documentation](https://docs.microsoft.com/azure/cloud-shell/overview).

4. In the PowerShell pane, enter the following commands to clone this repo:

    ```
    rm -r mslearn-databricks-ml -f
    git clone https://github.com/MicrosoftLearning/mslearn-databricks-ml
    ```

5. After the repo has been cloned, enter the following commands to change to the folder for this lab and run the **setup.ps1** script it contains:

    ```
    cd mslearn-databricks-ml/Allfiles/labs/03
    ./setup.ps1
    ```

6. If prompted, choose which subscription you want to use (this will only happen if you have access to multiple Azure subscriptions).

7. Wait for the script to complete - this typically takes around 5 minutes, but in some cases may take longer. While you are waiting, review the [Hyperparameter tuning](https://learn.microsoft.com/azure/databricks/machine-learning/automl-hyperparam-tuning/) article in the Azure Databricks documentation.

## Create a cluster

Azure Databricks is a distributed processing platform that uses Apache Spark *clusters* to process data in parallel on multiple nodes. Each cluster consists of a driver node to coordinate the work, and worker nodes to perform processing tasks. In this exercise, you'll create a *single-node* cluster to minimize the compute resources used in the lab environment (in which resources may be constrained). In a production environment, you'd typically create a cluster with multiple worker nodes.

> **Tip**: If you already have a cluster with a 13.3 LTS **<u>ML</u>** or higher runtime version in your Azure Databricks workspace, you can use it to complete this exercise and skip this procedure.

1. In the Azure portal, browse to the **msl-*xxxxxxx*** resource group that was created by the script (or the resource group containing your existing Azure Databricks workspace)
1. Select your Azure Databricks Service resource (named **databricks*xxxxxxx*** if you used the setup script to create it).
1. In the **Overview** page for your workspace, use the **Launch Workspace** button to open your Azure Databricks workspace in a new browser tab; signing in if prompted.

    > **Tip**: As you use the Databricks Workspace portal, various tips and notifications may be displayed. Dismiss these and follow the instructions provided to complete the tasks in this exercise.

1. In the sidebar on the left, select the **(+) New** task, and then select **Cluster**.
1. In the **New Cluster** page, create a new cluster with the following settings:
    - **Cluster name**: *User Name's* cluster (the default cluster name)
    - **Cluster mode**: Single Node
    - **Access mode**: Single user (*with your user account selected*)
    - **Databricks runtime version**: *Select the **<u>ML</u>** edition of the latest non-beta version of the runtime (**Not** a Standard runtime version) that:*
        - *Does **not** use a GPU*
        - *Includes Scala > **2.11***
        - *Includes Spark > **3.0***
    - **Use Photon Acceleration**: <u>un</u>selected
    - **Node type**: Standard_DS3_v2
    - **Terminate after** *30* **minutes of inactivity**

1. Wait for the cluster to be created. It may take a minute or two.

> **Note**: If your cluster fails to start, your subscription may have insufficient quota in the region where your Azure Databricks workspace is provisioned. See [CPU core limit prevents cluster creation](https://docs.microsoft.com/azure/databricks/kb/clusters/azure-core-limit) for details. If this happens, you can try deleting your workspace and creating a new one in a different region. You can specify a region as a parameter for the setup script like this: `./setup.ps1 eastus`

## Use a notebook to optimize hyperparameters

The tasks and code used in this exercise are in a notebook that you will run in your cluster.

1. In the Azure Databricks portal for your workspace, in the sidebar on the left, select **Workspace**. Then select the **&#8962; Home** folder.
1. At the top of the page, in the **&#8942;** menu next to your user name, select **Import**. Then in the **Import** dialog box, select **URL** and import the notebook from `https://github.com/MicrosoftLearning/mslearn-databricks-ml/raw/master/notebooks/Hyperopt.ipynb`
1. Connect the notebook to your cluster, and follow the instructions it contains; running its code cells to work with hyperparameters in machine learning experiments.

## Clean-up

If you're finished working with Azure Databricks for now, in Azure Databricks workspace, on the **Compute** page, select your cluster and select **&#9632; Terminate** to shut it down.

You can then close the Azure Databricks web portal, return to the Azure portal, and delete the **msl-*xxxxxxx*** resource group containing your Azure Databricks workspace.
