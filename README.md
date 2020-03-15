# Spark Project
Spark and Python3 hands on project
## Setup
The following instructions are made for Mac OS users. For Windows or Linux there could be some variations.
https://sundog-education.com/spark-python/
1. Install python 3 
  - run `brew install python`.
    - python3 will launch the Homebrew-installed Python 3 interpreter (Mac OS has python 2 by default, if we don't want to type python3 everytime we can use a version manager like `pyenv`)
2. Install spark
  - Install Spark using homebrew
    - `brew install apache-spark` 
  - Create a log4j.properties file
    - run `brew info apache-spark` to find the directory where it was installed and it's version
    - `cd /usr/local/Cellar/apache-spark/2.4.5_1` 
    - `cd libexec/conf`
    - `cp log4j.properties.template log4j.properties`
  - Edit the log4j.properties file
    - `vi log4j.properties` 
    - change the log level from INFO to ERROR on log4j.rootCategory (Using a command line editor like vi (vim) or nano. Please refer to the vim section)
 3. Install Anaconda
    - Install the latest Anaconda for Python 3 from anaconda.com and follow https://docs.anaconda.com/anaconda/install/mac-os/
    - Recommended:  verify data integrity with SHA-256 with `shasum -a 256 /path/filename` and check that it matches the hash in https://docs.anaconda.com/anaconda/install/hashes/
    - Anaconda is an open-source Python distribution. It's the easiest way to perform Python/R data science and machine learning but could be also used for plain simple web development. It has so many packages already backed in. Allows to manage libraries, dependencies, and environments with Conda
    - bash ~/Downloads/Anaconda3-2019.10-MacOSX-x86_64.sh
    - check version with `conda -V`
    
 4. Test the Environment
  - run `spark-shell`
  - `scala> sc.parallelize(1 to 1000).count()`
  - `:q`
  - `pyspark`
  - `sc.parallelize(range(1000)).count() ` BUG
  - `exit()`
  
  5. Trouble Shoot - Issue with Spark and MAC's Java Version
  - If pyspark  does not work consider Installing Java 8 JDK
    - `brew cask install adoptopenjdk8` or https://www.oracle.com/java/technologies/javase-downloads.html
    - `/usr/libexec/java_home -V`
    -  copy the path for java8 and add it to JAVA_HOME in bash profile
  - Also try : uninstalling apache and downloading it from http://spark.apache.org/downloads.html and extract it in your home, in this case it is spark-2.4.5-bin-hadoop2.7
  - `vim ~/.bash_profile`
  - and add the following
    - export JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk1.8.0_241.jdk/Contents/Home"
    - export SPARK_HOME=~/spark-2.4.5-bin-hadoop2.7
    - export PATH=$SPARK_HOME/bin:$PATH
    - export PYSPARK_PYTHON=python3
    - export PYTHONPATH=$SPARK_HOME/python:$SPARK_HOME/python/lib/py4j-0.9-src.zip:$PYTHONPATH
    - export PYSPARK_SUBMIT_ARGS=pyspark-shell
  - `source ~/.bash_profile`
   
   6. Done! At this point we've got spark set up in the computer, running on top of a JDK in a python development environment.
   7. `pip install jupyter notebook` 

## Vim 
Most important commands in vi are these:
- To delete the character that is currently under the cursor you must press `x`
- Press `i` to enter the Insert mode. Now you can type in your text.To leave the Insert mode press `ESC`.
- If you have made changes and want to save the file, press `:x`
- If you haven't made any changes, press `:q`
- If you have made changes, but want to leave the file without saving the changes, press `:q!`

## Intro
Spark is a fast and general cluster computing system for Big Data. It provides
high-level APIs in Scala, Java, Python, and R, and an optimized engine that
supports general computation graphs for data analysis.. It also supports a
rich set of higher-level tools including Spark SQL for SQL and DataFrames,
MLlib for machine learning, GraphX for graph processing,
and Spark Streaming for stream processing.
Documentation: http://spark.apache.org/documentation.html

## Start a new conda environment
`conda create -n pyspark_env python=3`
Activate the environment with source activate pyspark_env


PySpark is a Python API to using Spark, which is a parallel and distributed engine for running big data applications

## Data to mess around
We have Movie ratings data freely available for researchers from grouplens.org (movielengs.org).
They have over 40 million ratings in their complete dataset (which qualifies as big data). 
At first we'll be running this just on our desktop (we'll run spark on a cluster later on) so for now, download a smaller dataset -> 100K Dataset (~5mb)
### Movielens - Downloaded folder
  - the u.data file is the one containing all the movie ratings
  - u.items contains the lookup table for all the movie ids to movie names
