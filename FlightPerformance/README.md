# FlightPerformance

We will explore the world of airline on-time performance data analysis. Your task will be to implement a pipeline that runs a set of pseudo distributed map reduce tasks to plot the mean delay of the five most active airlines and for the five most active airports in the country. Specifically, your code should take a set of data files as input and produce visualizations of delays. You are free to choose how to visualize delays, how many graphs you want to produce, etc. You will be asked to defend your choice.

## Expected elements of a solution:
- A Makefile that builds and runs the pipeline (including graph generation);
- One or more map reduce tasks that read and clean the data, any corrupt row can be deleted, and output data that can be used to generate a graph
- A R Markdown file that includes code to generate graphs from the output of the MR task and explanation of the results.

## Fine print
Data for one month is in `input` folder 

## Code Structure

- `Driver`  : `org.neu.FlightPerformance`
  - Arguments `<iterations> <k> <input> <output> <report-loc>`
- `Job` :  `org.neu.job.FlightDelayJob`

## Hadoop Cluster Config
### AWS EC2 pseudo-distributed
Used with Experiment 1 mentioned in the report
- `conf/pseudo-distributed/core-site.xml`
- `conf/pseudo-distributed/hdfs-site.xml`
- `conf/pseudo-distributed/mapred-site.xml`
- `conf/pseudo-distributed/yarn-site.xml`


## Running Instructions
### Local
- Default : `make` (_`build gunzip setup-hdfs run`_)
- If already unzipped use : `make all-uz` (_`build setup-hdfs run`_)
### AWS EMR
Make sure you have AWS CLI working with your KEY+SECRET
- Step1: 
```
make setup-s3
```
- Step2: 
```
make cloud AWS_REGION=us-east-1 AWS_BUCKET_NAME=mr-neighbor AWS_SUBNET_ID=subnet-51e4fd7a AWS_NUM_NODES=1 AWS_INSTANCE_TYPE=m1.medium INPUT_TYPE=books AWS_NUM_NODES=1
```


## Reports
- Score : `make get-output-row-count (gives o/p count. Use 'hdfs dfs -get output output' to copy all output files to local)`
- Markdown Report : `report/report.Rmd`
- HTML Report : `report/report.html`
- PDF Report : `report/report.pdf`
