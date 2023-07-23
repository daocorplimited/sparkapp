# Spark Application

## How to run the app

To run the application you can use just Kubernetes Client Kubectl using the following:

        kubectl apply -f spark-app.yaml -n spark

It will work immediately but for the next run you need to adjust the parameter *metadata.name* for any another, because there could not be more than one application with the same name in a Kubernetes Cluster.

To make it programmatically invocable I have paramtrized it in a standard way with Helm (alternativelly Kustomize could be used). To run the parametrized SparkApplication, you need to call it as:

        helm upgrade sparkapp sparkapp/ -n spark --set runId=15 --install

Just pay attention to the parameter *runId* it should have a unique value (any format, could be integer either string). Currently you also can manage the following parameters:

- Number of executor instances with *executor.instances*.
- Memory for executor instances with *executor.memory*.

For example, the application could be run as follows:

        helm upgrade sparkapp sparkapp/ -n spark --set runId=16 --set executor.instances=2 --set executor.memory="512M" --install

So it means, that the client, which initiate the Spark Application can dynamically allocate the resources.