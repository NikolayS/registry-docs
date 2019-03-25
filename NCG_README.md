# Dotscience

### Description
[Dotscience](https://dotscience.com/) allows teams to put their machine learning development and deployment into a robust model management framework. Models and all accompanying files are versioned and their provenance is auto-recorded throughout training and into deployment. 

Dotscience tracks the variables, such as hyperparameter combinations and accuracy metrics, in every run in model training and optimization. This record provides a run history of your team's work, so that team members can easily compare the performance of models using different code, data versions, and hyperparameter combinations. 

The data can also be visualized on the Dotscience web interface to give insights into model behavior: for instance, to show the effect of a hyperparameter choice on accuracy metrics.

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
To use Dotscience for version control and provenance tracking, you need to install the Dotscience container image on your chosen compute, called a runner (see **Run Dotscience** below). 

Additionally, any files required for model development, including training data and model code, should be added to Dotscience storage to place them under version control. Files are added via the Dotscience web interface.

To instead use Dotscience for on premise version control, please contact us directly at `sales@dotscience.com`.

To extract model run metadata for your run history, such as hyperparameter combinations and summary metrics, you should annotate your model code with the Dotscience Python library. 


## Run Dotscience
### Requirements
* A runner (any machine, either local or a cloud VM) running either Ubuntu 16.04+ or CentOS 7, with Docker installed. 
For details on setting up your runner, see [the Dotscience documentation on runners](https://docs.dotscience.com/setup/#2-set-up-your-runner).

* If you want to use your runner's GPUs for compute, see [the Dotscience documentation on GPU runners](https://docs.dotscience.com/setup/expose-gpus-on-your-runner/).


### Instructions



1. Email sales@dotscience.com to receive a time-limited Dotscience account, giving you 7 days access to the Dotscience web interface. Log in to [cloud.dotscience.net](https://cloud.dotscience.net) with your credentials.

2. Get an authentication token from the NVIDIA NGC registry so that you can pull the Docker container. Open https://ngc.nvidia.com/setup/api-key and click the button **Generate API Key**. Then, using the code snippet on the page, log in to Docker on your computer using 

```
$ docker login nvcr.io

Username: $oauthtoken
Password: <YOUR NCG AUTH TOKEN>
```



3. Now you can set up your runner. Navigate to the **Runners** page of the Dotscience web interface. Click **Add new** to add a new runner to your account. 

Select the runner type: `CPU` or `GPU`. For GPU runners see step 3.
Select the required storage quantity to be allocated to the runner.

4. If you want to run a GPU-accelerated model, and have set up a [GPU runner](https://docs.dotscience.com/setup/expose-gpus-on-your-runner/), select `nvidia runtime` from the dropdown menu on the **Runers** page.

4.  Under **Launching this runner** is a code snippet. Extract the runner `TOKEN` from the code snippet displayed.

4. SSH into your runner. Store the extracted `TOKEN` as an environment variable there, named `TOKEN`, as follows:

```
$ export TOKEN="<your token>"  # replace <your token> with your copied value here
```

5.  Run the following:

```
docker run --name dotscience-runner -d -e TOKEN=$TOKEN \
    --restart always -v /var/run/docker.sock:/var/run/docker.sock \
    -v dotscience-task-spool:/spool \
    nvcr.io/partners/dotscience-runner:latest 
```

This starts the `dotscience-runner` container, which will then boot up a couple more Docker containers on your runner. 

6. Create a Dotscience project in the **Projects** view. Upload data files you will need by clicking **Add files**.  Then **Launch Jupyter** to open a Jupyter lab instance using your runner as the backing compute. You can use the terminal on Jupyterlab to import more data, libraries, and other files.

For now, model development with Dotscience is done using Jupyter notebooks in Python. Coming soon is support for development in any development environment, such as a local text editor, in Python or R.

7. Annotate your model code with the Dotscience Python library. See documentation and examples here: [github.com/dotmesh-io/dotscience-python](https://github.com/dotmesh-io/dotscience-python)

8. Visualise your model metrics and provenance graph in the Dotscience web interface. Access collaboration features, including Github-style fork and merge, and version control for massive datasets.

## Documentation
[https://docs.dotscience.com/](https://docs.dotscience.com/)

## Community
[Join the Dotscience community Slack here.](https://dotmesh-community.slack.com/join/shared_invite/enQtMjU0NzczMTQ2MDgxLTM0MGJhNDcxNWQ4ZWE0OWMxMTE4NDg4ZmY5ZDRiMmQyYzIwYTIyMWNiYTIxMWMyMGUzNDI5YTc0N2JiMzg5OGE)

## Licensing
Dotscience is commercial software for enterprises. Access to Dotscience is provided here as a time-limited trial. Please talk to sales@dotscience.com to discuss signing up for an enterprise pilot.
