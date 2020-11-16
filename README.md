# Analyzing flight delay and weather data

This repository contains a set of Python scripts and Jupyter notebooks that analyze and predict flight delays.

We use [Elyra](https://github.com/elyra-ai/elyra) to create a pipeline that:

* Loads the data
* Pre-processes the data
* Performs data merging and feature extraction
* Analyzes and visualizes the data
* Trains and evaluates machine learning models for predicting delayed flights

This pipeline runs locally and on [Kubeflow Pipelines](https://www.kubeflow.org/docs/pipelines/overview/pipelines-overview/) using Elyra's execution capabilities.

![Flight Delays Pipeline](docs/source/images/flight-delays-pipeline.png)

### Configuring the local development environment

It's highly recommended to create a dedicated and consistent Python environment for running the notebooks in this repository:

1. Install [Anaconda](https://docs.anaconda.com/anaconda/install/)
   or [Miniconda](https://docs.conda.io/en/latest/miniconda.html)
1. Navigate to your local copy of this repository.
1. Create an Anaconda environment from the env file in the repository:
    ```console
    $ conda env create -f flight-delays-env.yaml
    ```
1. Activate the new environment:
    ```console
    $ conda activate flight-delays-env
    ```
1. If running JupyterLab and Elyra for the first time, build the extensions:
    ```console
    $ jupyter lab build
    ```
1. Launch JupyterLab:
    ```console
    $ jupyter lab
    ```

### Configuring a local Kubeflow Pipeline runtime

[Elyra's Notebook pipeline visual editor](https://elyra.readthedocs.io/en/latest/getting_started/overview.html#notebook-pipelines-visual-editor)
currently supports running these pipelines in a Kubeflow Pipeline runtime.  If required, these are
[the steps to install a local deployment of KFP](https://elyra.readthedocs.io/en/latest/recipes/deploying-kubeflow-locally-for-dev.html).

After installing your Kubeflow Pipeline runtime, use the command below (with proper updates) to configure the new
KFP runtime with Elyra.

```bash
elyra-metadata install runtimes --replace=true \
       --schema_name=kfp \
       --name=kfp_local \
       --display_name="Kubeflow Pipeline (local)" \
       --api_endpoint=http://[host]:[api port]/pipeline \
       --cos_endpoint=http://[host]:[cos port] \
       --cos_username=[cos username] \
       --cos_password=[cos password] \
       --cos_bucket=flights
``` 

**Note:** The cloud object storage above is a local minio object storage but other cloud-based object storage 
services could be configured and used in this scenario.