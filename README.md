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

[Note the `PYTHONHASHSEED` is from https://stackoverflow.com/a/46674748/5179470]

# === ORIGINAL README: ===

# PySpark-Boilerplate
A boilerplate for writing PySpark Jobs

For details see accompanyiong blog post at https://developerzen.com/best-practices-writing-production-grade-pyspark-jobs-cb688ac4d20f#.wg3iv4kie
