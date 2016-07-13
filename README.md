#H2o-Sparkling-GPU

##How to setup H2o-Sparkling on GPU
------------------------------------------

##Cloud
AMI image: TensorFlow 0.6 with GPU Support (ami-e191b38b)
spot instance based ; Login into your instance once you get the ip of your instance 

##Setting JAVA_HOME
file $(which java)
/usr/bin/java: symbolic link to `/etc/alternatives/java'

file /etc/alternatives/java
/etc/alternatives/java: symbolic link to `/usr/lib/jvm/java-8-oracle/jre/bin/java' 

/usr/lib/jvm/java-7-openjdk-amd64/jre is ur java location
include JAVA_HOME in your bash script 
vi .bashrc
export JAVA_HOME="/usr/lib/jvm/java-8-oracle/jre/"

##Setting up Spark 

###Installing Scala 
wget http://www.scala-lang.org/files/archive/scala-2.11.8.tgz
sudo mkdir /usr/local/src/scala
sudo tar xvf scala-2.11.8.tgz -C /usr/local/src/scala/
vi .bashrc
export SCALA_HOME=/usr/local/src/scala/scala-2.11.8
export PATH=$SCALA_HOME/bin:$PATH
source .bashrc

test it by typing:
scala 

###Installing spark 
wget https://www.apache.org/dist/spark/spark-1.6.1/spark-1.6.1.tgz
tar xvf spark-1.6.1.tgz
cd spark-1.6.1
sbt/sbt assembly

./bin/run-example SparkPi 10

##Setting up H20-Sparkling
###Install H2O/Sparkling water 

####Install h2o
http://www.h2o.ai/download/h2o/python
[sudo] pip install -U requests
[sudo] pip install -U tabulate
[sudo] pip install -U future
[sudo] pip install -U six

The following command removes the H2O module for Python.
[sudo] pip uninstall h2o

Next, use pip to install this version of the H2O Python module.
[sudo] pip install http://h2o-release.s3.amazonaws.com/h2o/rel-turin/3/Python/h2o-3.8.3.3-py2.py3-none-any.whl

####Install Sparkling Water 
export SPARK_HOME="/path/to/spark/installation" 
export MASTER="local-cluster[3,2,1024]" 
wget https://dl.dropboxusercontent.com/s/l4vcrowc4l3dtsz/sparkling-water-1.6.5.zip
unzip https://dl.dropboxusercontent.com/s/l4vcrowc4l3dtsz/sparkling-water-1.6.5.zip
cd sparkling-water-1.6.5
IPYTHON_OPTS="notebook" bin/pysparkling

Make sure you have ipython notebook installed 

##Get i-python notebooks
git clone https://github.com/h2oai/sparkling-water.git


##Reference 
http://ramhiser.com/2016/01/05/installing-tensorflow-on-an-aws-ec2-instance-with-gpu-support/

