## Step 1 : Create your cluster

First of all, once you are logged into your databricks dashboard, you have to create a cluster for your spark program to run on. (Note that with the trial version your cluster will be deleted after 2 hours being idle, you will have to repeat this step quite often).

![Create your cluster 1](https://github.com/alamit/How-to-run-your-assignments-on-databricks/blob/master/create-cluster1.png?raw=true)

Note that you don't have access to many configuration with the trial version, you will have to stick to default configs (1 master, no workers, 6GB of memory). You can add some Spark configuration options in the **Spark** tab.

![Create your cluster 2](https://github.com/alamit/How-to-run-your-assignments-on-databricks/blob/master/create-cluster3.png?raw=true)

Now that you created your cluster, you have to import the data you want to work with on it, so go back to your dashboard.

## Step 2 : Importing your data.

You have to complete **Step 1** before uploading your data, you need an active cluster in order to import data on it.

Back to your dashboard, you will now use **Table** to add data to your cluster.

![Import Data 1](https://github.com/alamit/How-to-run-your-assignments-on-databricks/blob/master/import-data1.png?raw=true)

Use **File** as Data Source type (if your Data Source is a File, later on we might some other types of data source). Then upload your file and you should see something like this.

![Import Data 2](https://github.com/alamit/How-to-run-your-assignments-on-databricks/blob/master/import-data2.png?raw=true)

*Please note the DBFS path of your file you will need later on.*

Now that your data is imported, you want to run some Spark program on it ! So go back to your dashboard, it's time to create your first Notebook.

## Step 3 : Create a Scala Notebook

Back on your dahsboard, let's now create a Scala Notebook. 

![Create Notebook 1](https://github.com/alamit/How-to-run-your-assignments-on-databricks/blob/master/create-notebook1.png?raw=true)

Be sure to use Scala as a language parameter, and choose the name of your notebook.

![Create Notebook 2](https://github.com/alamit/How-to-run-your-assignments-on-databricks/blob/master/create-notebook2.png?raw=true)

This will send you to your fresh notebook, don't forget to link your Notebook to your cluster.

![Create Notebook 3](https://github.com/alamit/How-to-run-your-assignments-on-databricks/blob/master/create-notebook3.png?raw=true)

## Step 4 : Write your Spark program.

**This code example contains some code samples from the assignment wikipedia on [Coursera](https://www.coursera.org/learn/scala-spark-big-data/home/info), this code is owned by the teaching team.**

Now that your Notebook is ready, you can run your spark program on it. I'd like to attract your attention on two points : 
- `SparkContext sc` is already defined in your Notebook, don't create a new one.
- Load your `RDD` using `RDD[String] = sc.textFile("your-path-as-shown-in-step-2")`
- Note that if you want to pass a something that comes from an `object` to a `RDD`'s method, your object will have to be `Serializable`.

Here is a small code example that can run on your cluster, this code will give you back all the articles' titles starting with the letter "X" : 
```scala
case class WikipediaArticle(title: String, text: String)

object WikipediaData extends Serializable {
  def parse(line: String): WikipediaArticle = {
    val subs = "</title><text>"
    val i = line.indexOf(subs)
    val title = line.substring(14, i)
    val text  = line.substring(i + subs.length, line.length-16)
    WikipediaArticle(title, text)
  }
}

val myRDD = sc.textFile("your-path-as-shown-in-step-2").map(WikipediaData.parse)

def titlesStartingWith(prefix: String, rdd: RDD[WikipediaArticle]): List[String] = {
  rdd.map(_.title).filter(_.startsWith(prefix)).collect.toList
}

println(titlesStartingWith("X", myRDD))
```
