# Apache PySpark in Docker

PySpark docker container based on OpenJDK 8 and Miniconda 3

[![](https://images.microbadger.com/badges/image/sudheerpalyam/pyspark.svg)](https://microbadger.com/images/sudheerpalyam/pyspark "Get your own image badge on microbadger.com") [![](https://images.microbadger.com/badges/version/sudheerpalyam/pyspark.svg)](https://microbadger.com/images/sudheerpalyam/pyspark "Get your own version badge on microbadger.com") 

## Build this Image
```bash
docker build -t sudheerpalyam/pyspark .                 
```

## Running the container
By default spark-submit --help is run:

```bash
docker run sudheerpalyam/pyspark 
```

To launch into docker container (skipping default ENTRYPOINT of spark-submit)
```bash
docker run -t -i --entrypoint="/bin/bash" sudheerpalyam/pyspark
```

To run your own job, make the job accessible through a volume and pass the necessary arguments:

```bash
docker run -v /local_folder:/job sudheerpalyam/pyspark [options] /job/<python file> [app arguments]
```

### Samples

The folder samples contain some PySpark jobs, how to obtain a spark session and crunch some data. The current directory is mapped as /job. So run the docker command from the root directory of this project.

```bash
# Self word counter:
docker run -v $(pwd):/job sudheerpalyam/pyspark /job/samples/word_counter.py

# Self word counter with spark extra options
docker run -v $(pwd):/job sudheerpalyam/pyspark \
	--name "I count myself" \
	--master "local[1]" \
	--conf "spark.ui.showConsoleProgress=True" \
	--conf "spark.ui.enabled=False" \
	/job/samples/word_counter.py "jobSampleArgument1"
```