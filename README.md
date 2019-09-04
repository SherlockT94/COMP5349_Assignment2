# COMP5349_Assignment2
### Prepare the configuration file and bootstrapping file
1.  load the configuration file in S3 <br>
[
{
"Classification": "spark-env",
"Configurations": [
{
"Classification": "export",
"Properties": {
"PYSPARK_PYTHON": "/usr/bin/python3"
}
}
]
},
{
"Classification": "yarn-env",
"Properties": {},
"Configurations": [
{
"Classification": "export",
"Properties": {
"PYSPARK_PYTHON": "/usr/bin/python3",
}
}
]
},
{
    "Classification": "spark",
    "Properties": {
      "maximizeResourceAllocation": "true"
    }
},
{"classification": "livy-conf",
  "Properties": {"livy.server.session.timeout":"5h"}}
]

2. load the bootstrap file in S3: <br>
sudo yum install git <br>
sudo pip-3.6 install --quiet tensorflow-hub <br> 
sudo pip-3.6 install --quiet numpy<br>
sudo pip-3.6 install --quiet nltk<br>
sudo python -m nltk.downloader 'punkt' -d /usr/share/nltk_data punkt


### Create the cluster on EMR
Click the 'Create Cluster' then click 'go to advanced options' button
1. software and steps configuration: choose EMR 5.23.0, choose the Hadoop 2.8.5, spark 2.4.0, livy 0.5.0 and TensorFlow 1.12.0. For 'edit software setting', load the json from S3
2. hardware configuration: select use 1 master node and 4 core nodes. Change the instance type to m4.xlarge
3. general cluster setting: Expand
the Bootstrap Actions options at the bottom of the page. In Add bootstrap action
drop down list, select “Custom action”, then click Configure and Add. This will
bring out a window allowing you to select the bootstrapping file from S3
4. Security: select the EC2 key pair

### Upload the notebook to EMR notebook
Following the instruction given by AWS (https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-managed-notebooks-working-with.html)

### Running the notebook
1. Open the EMR notebook in the cluster just created
2. Click the 'Cell' in the top bar and then Click 'Run all' to run all cells.
