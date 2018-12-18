# ETL-PySpark
The goal of this project is to do some ETL (Extract, Transform and Load)  with the Spark Python API ([PySpark](https://spark.apache.org/docs/latest/api/python/pyspark.html)) and Hadoop Distributed File System ([HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsUserGuide.html)).

Working with CSV's files from [HiggsTwitter dataset](http://snap.stanford.edu/data/higgs-twitter.html) we'll do :
- Convert CSV's dataframes to [Apache Parquet](https://parquet.apache.org/) files.
- Use **Spark SQL** using DataFrames API and SQL language.
- Some **performance testing** like compressed CSV vs Parquet, cached DF vs not cached DF and local file access vs local HDFS access.

### Preparing the environment
We will need to install/extract Hadoop and Spark, and remember to create the necessary environment variables:

*Windows environment variables (example)*:
~~~
JAVA_HOME=C:\Progra~1\Java\jdk1.8.0_131
HADOOP_HOME=C:\hadoop
SPARK_HOME=C:\spark
PYTHONPATH=%SPARK_HOME%\python;
PATH=C:\Python;C:\Python\Scripts;%HADOOP_HOME%\bin;%SPARK_HOME%\bin;%PYTHONPATH%;%PATH%;
~~~


### Hadoop
Hadoop can be downloaded from [Hadoop releases webpage](http://hadoop.apache.org/releases.html). These releases do not include [winutils](https://github.com/steveloughran/winutils/releases) (Windows binaries for Hadoop versions) required in order to run Hadoop in Windows systems.

#### Configuring Hadoop
Read this guide in order to install Hadoop on Windows: https://wiki.apache.org/hadoop/Hadoop2OnWindows

Some notes to consider:
- Spark and Hadoop and **require Java**. JDK 8 64bits worked for me.
- **JAVA_HOME** must match our Java downloaded version (in my case 1.8.0_131). "Progra\~1" for 64bits path installation and "Progra\~2" for 32bits.
- **PYTHONPATH** is the path were Python will look for additional libraries. In this case, is set to look for the spark ones.
- In **PATH** variable, *%PATH%* means the same PATH value we already have. Basically add the new paths at the beginning of the PATH value.
- In order to avoid troubles, we should set **hadoop.tmp.dir** in file *\hadoop\etc\hadoop\core-site.xml* with Hadoop tmp directory we want (note that drive letter is preceded by /). For example:
~~~
  <property>
    <name>hadoop.tmp.dir</name>
    <value>/C:/hadoop/temp/</value>
  </property>
~~~

### PySpark
In order to run PySpark we need to install the Python library py4j:
~~~
pip install py4j
~~~

Then we can go to [Jupyter Notebook ETL example](jupyter/ETL.ipynb) in order to see some ETL with PySpark.
