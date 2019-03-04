# Dotscience

### Description
Dotscience is a platform for collaborative and reproducibible machine learning. 

It enables tracking of all model variables, inputs, data and code versions throughout model development and deployment. This record provides a version history of your team's work. It can be to visualized on the Dotscience web interface to show interactions between hyperparameters and accuracy metrics in model development. It is also used to track file provenance throughout the model training and serving cycle. 

### Publisher
Dotscience

### Built By
Dotscience

### Latest Tag
`latest`

### Modified
 #TODO
### Size
 #TODO



## **`pull command`:** `docker pull nvcr.io/nvidia/dotmesh/dotscience-runner:latest` #TODO

### Using Dotscience
To use Dotscience, you need to intall the Dotscience container image on your chosen runner, and annotate your model code with the Dotscience Python library. If your model is defined and trained in a Jupyter notebook, you can edit the code via the Dotscience web interface Jupyterlab instance. Any additional files, including training data, can be added to the Dotscience web interface to place them under version control.


### Model specification
Models can be run in Jupyter notebooks or Python command-line scripts. They may be GPU enabled. Runners can be any cloud VM or local machine. 

## Run Dotscience
### Requirements
* A runner (any cloud machine) running either Ubuntu or CentOS 7, with Docker installed.

* If you want to run on your runner's GPUs, then you will need to have installed `nvidia container runtime`. For installation instructions, see the [NVIDIA documentation](https://github.com/NVIDIA/nvidia-container-runtime).


### Instructions

1. Get a Dotscience account #TODO
2. Navigate to the **Runners** page of the Dotscience web interface. Click **Add new** to add a new runner. Give the new runner a name and, optionally, a description. On the new runner page, extract the runner `TOKEN` from the code snippet shown.
3. If you want to run a GPU-accelerated model, tick the box on the runner page marked **GPU runner**. #TODO
3. SSH into your runner. Store the extracted `TOKEN` as an environment variable there, named `TOKEN`:
```
$ TOKEN = $TOKEN  # replace the second 'TOKEN with your copied value
```
4.  Run the following:

```
    docker run --name dotscience-runner -d -e TOKEN=$TOKEN \
    --restart always -v /var/run/docker.sock:/var/run/docker.sock \
    -v dotscience-task-spool:/spool \
    nvcr.io/nvidia/dotmesh/dotscience-runner:latest #TODO
```

Note that the `dotscience-runner` container will boot up a couple more Docker containers on your runner. 

5. Annotate your model code with the Dotscience Python library. See documentation and examples here: [github.com/dotmesh-io/dotscience-python](https://github.com/dotmesh-io/dotscience-python)

6. Visualise your model metrics and provenance graph in the Dotscience web interface. Access collaboration features, including Github-style fork and merge, and version control for massive datasets.

## Documentation
#TODO add link

## Licensing
Dotscience is commerical software for enterprises. Please talk to sales@dotscience.com for information about signing up.