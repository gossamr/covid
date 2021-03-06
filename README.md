![covid](https://github.com/epidemics/covid/workflows/covid/badge.svg)

# covid-19 visualizer

## Architecture
* `webserver` - a webserver using `fastapi` to render templates.


# Development
## Using docker (the easiest)
```
docker-compose up  # possibly with --build
```
and go to `localhost:8000` (main `server`)

## locally/manually
Manually using [poetry](https://python-poetry.org/docs/#installation):
```
$ poetry install
$ poetry shell
```

then start up the `fastapi` server:
```
$ cd src/server
$ uvicorn main:app --reload
```

### Using conda environments
1. [Install miniconda](https://conda.io/projects/conda/en/latest/user-guide/install/index.html#) ([e.g. Windows](https://conda.io/projects/conda/en/latest/user-guide/install/windows.html))
2. open terminal in the clonned repository and run:
```
$ conda create -n covid python=3.8  # creates a new conda environment with python 3.8
$ conda activate covid  # activates the conda environment
$ pip install poetry  # installs poetry inside this environment
$ poetry install  # installs the project dependencies (you must be in the root of the cloned repository)
```
and then you should be able to follow `locally/manually` way of triggering the server.

## Getting inside the container
```
$ docker-compose run --entrypoint bash server
```

can be used to e.g. install deps:
```
$ docker-compose run --entrypoint poetry server add pyarrow
```

## tests
```
poetry run pytest tests
```
or inside the container

## linting

install the needed packages locally with
```
npm i
```

Then run the linting tests with

```
npm test
```

To automatically lint your files run

```
prettier --write "{src/server/static/**, src/server/templates/**}"
```

# Deployment
We use Github Actions. The pipeline is specified in `.github/workflows/pythonapp.yml`

* On a merge to `staging` branch, the code is deployed to the staging environment.
* On a merge to `master` branch, the code is deployed to the production environment.
