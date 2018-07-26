Spark submit structure: `spark-submit --py-files pyfile.py,zipfile.zip main.py --arg1 val1`

1. Prepare python files for pyspark:
```
pip install -r requirements.txt -t ./src/libs
make build
```

2. Run job (requires setup from https://github.com/asmith26/docker-spark-cluster):
```
docker run --rm -it --link master:master --volumes-from spark-datastore --volume ~/git/PySpark-Boilerplate/dist/:/scripts spark-submit spark-submit --master spark://172.17.0.3:7077 --conf spark.executorEnv.PYTHONHASHSEED=321 --py-files /scripts/jobs.zip,/scripts/libs.zip /scripts/main.py --job wordcount
```

or with yarn* `export PYSPARK_PYTHON="/home/PythonVersions/Python3.5.5/bin/python3.5" && spark2-submit --conf spark.executorEnv.PYTHONHASHSEED=321 --master yarn --py-files dist/jobs.zip,dist/libs.zip dist/main.py --job wordcount`

> **Better Note:** Using Miniconda to manage non-sudo python and pacakges (as per below): https://conda.io/docs/user-guide/getting-started.html

>*Note: since `--py-files` inserts these files into the `PYTHONPATH`, we need to ensure we have permission to do so. The easiest way to ensure this is by putting the Python install somewhere widely accessible: e.g (includes instructions for install Python from source and getting it on the slaves when no internet is avaiable)
  ```
# Download https://www.python.org/downloads/
#
# On edge:
tar -xvf Python..zip
cd Python...
sudo mkdir -p /home/PythonVersions/Python3.5.5
sudo chmod 777 /home/PythonVersions/Python3.5.5
./configure --prefix=/home/PythonVersions/Python3.5.5
make
make install
/home/PythonVersions/Python3.5.5/bin/python3.5
#
cp /home/PythonVersions/Python3.5.5/ folder to the 4 workers, put in same location/permissions
```

[Note the `PYTHONHASHSEED` is from https://stackoverflow.com/a/46674748/5179470]

# === ORIGINAL README: ===

# PySpark-Boilerplate
A boilerplate for writing PySpark Jobs

For details see accompanyiong blog post at https://developerzen.com/best-practices-writing-production-grade-pyspark-jobs-cb688ac4d20f#.wg3iv4kie
