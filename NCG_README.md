# Dotscience

### Description
[Dotscience](https://dotscience.com/) is a platform that allows you to put your machine learning development and deployment into a model management framework. 

Dotscience puts your code, datasets of any size, and compute environments under version control. It auto-tracks the provenance of all your assets through development and into production, wherever your models are served.

Dotscience also enables tracking of variables involved in model runs in training: including hyperparameter combinations, and accuracy metrics. This record provides a run history of your team's work, so members can see at a glance how different model versions perform. It can also be visualized on the Dotscience web interface, to give insights into model behavior: for instance, to show the effect of a hyperparameter choice on accuracy metrics.

### Publisher
Dotscience

### Built By
Dotscience

### Latest Tag
`0.0.4`

### Modified
 Feb 11 2019
### Size
 16.3 MB


**`pull command`:** `docker pull nvcr.io/nvidia/dotmesh/dotscience-runner:0.0.4`

### Using Dotscience
To use Dotscience for version control and provenance tracking, you need to install the Dotscience container image on your chosen compute, called a runner (see below. 

To extract model run metadata (such as hyperparameter combinations and summary metrics) you should annotate your model code with the Dotscience Python library. Any additional files, including training data, required by the model can be added to the Dotscience web interface to place them under version control.

### Model specification
Models can be defined and trained in Jupyter notebooks, accessed via the Dotscience web interface. They may be GPU enabled. Runners can be any cloud VM or local machine.

## Run Dotscience
### Requirements
* A runner (any machine, either local or a cloud VM) running either Ubuntu 16.04+ or CentOS 7, with Docker installed. 
For details on setting up your runner, see [the Dotscience documentation on runners](https://docs.dotscience.com/setup/#2-set-up-your-runner).

* If you want to use your runner's GPUs, see [the Dotscience documentation on GPU runners](https://docs.dotscience.com/setup/expose-gpus-on-your-runner/).


### Instructions

1. Email sales@dotscience.com to receive a time-limited Dotscience account, giving you 7 days access. Log in to [cloud.dotscience.net](https://cloud.dotscience.net) with your credentials.
2. Navigate to the **Runners** page of the Dotscience web interface. Click **Add new** to add a new runner. Give the new runner a name and, optionally, a description. On the new runner page, extract the runner `TOKEN` from the code snippet shown.
3. If you want to run a GPU-accelerated model, and have set up a [GPU runner](https://docs.dotscience.com/setup/expose-gpus-on-your-runner/), select `nvidia runtime` from the dropdown menu on the **Runers** page.
3. SSH into your runner. Store the extracted `TOKEN` as an environment variable there, named `TOKEN`, as follows:

```
$ export TOKEN="<your token>"  # replace <your token> with your copied value here
```

4.  Run the following:

```
docker run --name dotscience-runner -d -e TOKEN=$TOKEN \
    --restart always -v /var/run/docker.sock:/var/run/docker.sock \
    -v dotscience-task-spool:/spool \
    nvcr.io/nvidia/dotmesh/dotscience-runner:latest #TODO update image location
```

The `dotscience-runner` container will then boot up a couple more Docker containers on your runner. 

5. Create a Dotscience project in the **Projects** view. Upload data files you will need by clicking **Add files**.  Then **Launch Jupyter** to open a Jupyter lab instance using your runner as the backing compute. You can use the terminal on Jupyterlab to import more data, libraries, and other files.

For now, model development with Dotscience is done using Jupyter notebooks in Python. Coming soon is support for development in any development environment, such as a local text editor, in Python or R.

6. Annotate your model code with the Dotscience Python library. See documentation and examples here: [github.com/dotmesh-io/dotscience-python](https://github.com/dotmesh-io/dotscience-python)

7. Visualise your model metrics and provenance graph in the Dotscience web interface. Access collaboration features, including Github-style fork and merge, and version control for massive datasets.

## Documentation
[https://docs.dotscience.com/](https://docs.dotscience.com/)

## Community
[Join the Dotscience community Slack here.](https://dotmesh-community.slack.com/join/shared_invite/enQtMjU0NzczMTQ2MDgxLTM0MGJhNDcxNWQ4ZWE0OWMxMTE4NDg4ZmY5ZDRiMmQyYzIwYTIyMWNiYTIxMWMyMGUzNDI5YTc0N2JiMzg5OGE)

## Licensing
Dotscience is commercial software for enterprises. Access to Dotscience is provided here as a time-limited trial. Please talk to sales@dotscience.com to discuss signing up for an enterprise pilot.
