## Step 1 : Create your cluster

First of all, once you are logged into your databricks dashboard, you have to create a cluster for your spark program to run on. (Note that with the trial version your cluster will be deleted after 2 hours being idle, you will have to repeat this step quite often).

![Create your cluster 1](https://github.com/alamit/How-to-run-your-assignments-on-databricks/blob/master/create-cluster1.png)

Note that you don't have access to many configuration with the trial version, you will have to stick to default configs (1 master, no workers, 6GB of memory). You can add some Spark configuration options in the **Spark** tab.

![Create your cluster 2](https://github.com/alamit/How-to-run-your-assignments-on-databricks/blob/master/create-cluster3.png)

Now that you created your cluster, you have to import the data you want to work with on it, so go back to your dashboard.

## Step 2 : Importing your data.

You have to complete **Step 1** before uploading your data, you need an active cluster in order to import data on it.

Back to your dashboard, you will now use **Table** to add data to your cluster.

![Import Data 1](https://github.com/alamit/How-to-run-your-assignments-on-databricks/blob/master/import-data1.png)

Use **File** as Data Source type (if your Data Source is a File, later on we might some other types of data source). Then upload your file and you should see something like this.

![Import Data 2](https://github.com/alamit/How-to-run-your-assignments-on-databricks/blob/master/import-data2.png)

Now that your data is imported, you want to run some Spark program on it ! So go back to your dashboard, it's time to create your first Notebook.

## Step 3 : Create a Scala Notebook

Back on your dahsboard, let's now create a Scala Notebook. 

![Create Notebook 1](https://github.com/alamit/How-to-run-your-assignments-on-databricks/blob/master/create-notebook1.png)

Be sure to use Scala as a language parameter, and choose the name of your notebook.

![Create Notebook 2](https://github.com/alamit/How-to-run-your-assignments-on-databricks/blob/master/create-notebook2.png)

This will send you to your fresh notebook, don't forget to link your Notebook to your cluster.

![Create Notebook 3](https://github.com/alamit/How-to-run-your-assignments-on-databricks/blob/master/create-notebook3.png)

## Step 4 : Write your Spark program.


