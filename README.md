# JupyterDockerSpawnerOnSRC
Deploy JupyterHub with DockerSpawner on [SURF Research Cloud
(SRC)](https://servicedesk.surf.nl/wiki/display/WIKI/SURF+Research+Cloud).

The [JupyterHub Docker
Spawner](https://jupyterhub-dockerspawner.readthedocs.io/en/latest/) enables
JupyterHub to spawn single user notebook servers in Docker containers.

This document illustrates how to create a component, a catalog item and a
workspace on SRC.

## Create a component

Follow the [SRC Create a
component](https://servicedesk.surf.nl/wiki/display/WIKI/Create+a+component)
instructions and in the step `Define component script and source`, set the
source as `https://github.com/RS-DAT/JupyterDockerSpawnerOnSRC.git`.

See each item below for more technical information about the component:

- [research-cloud-plugin.yml](https://github.com/RS-DAT/JupyterDockerSpawnerOnSRC/blob/main/research-cloud-plugin.yml) for a list of
  packages that are installed.
- [jupyterhub_config.py.j2](https://github.com/RS-DAT/JupyterDockerSpawnerOnSRC/blob/main/roles/jupyter/templates/jupyterhub_config.py.j2)
  for a list of configs for jupyterhub and docker spawner.

## Create a catalog item

Follow the [SRC Create a catalog item](https://servicedesk.surf.nl/wiki/display/WIKI/Create+a+catalog+item) and choose the components as below:

- SRC-OS
- SRC-CO
- SRC-Ngnix
- SRC-External plugin
- the JupyterDockerSpawnerOnSRC component created in the previous step

Note: When choosing the `Operating system` in the step `Cloud provider`, choose
Ubuntu 20, because the latest version of Ubuntu does not support `iRODS` that is
needed for `SRC-CO` component.

## Create a workspace

Follow the [SRC Start a simple workspace](https://servicedesk.surf.nl/wiki/display/WIKI/Start+a+simple+workspace) and choose the item that is created in the previous step.

## Docker images and containers

The docker image can be set in the [jupyterhub config
file](https://github.com/RS-DAT/JupyterDockerSpawnerOnSRC/blob/main/roles/jupyter/templates/jupyterhub_config.py.j2). After logging to
Jupyter server, the docker image is pulled and a container starts running.
The volumes `/data` and `/scratch` are mounted within the user home directory (`~/data` and `~/scratch`)
inside the container. If the user does not stop the server, the container
continues running until a default timeout is reached (see Jupyter parameters [here](https://github.com/RS-DAT/JupyterDockerSpawnerOnSRC/blob/main/roles/jupyter/defaults/main.yml)). Otherwise, the container will be stopped (Status Exited).
Next time the user login, the same container will be used. So, the data and packages are preserved across sessions.
Note that, the container and images will stay on the workspace.
Only when the Jupyter service is stopped, the containers will be removed.

### Remove images or containers

You can log in to the workspace using `ssh` and use docker command with `sudo`
to delete images/containers.

## Credits

Most of the playbooks in this repository have been taken, inspired or adapted from the ones in the [RS-DAT JupyterDaskOnSRC](https://github.com/RS-DAT/JupyterDaskOnSRC) and in the [eWaterCycle infra](https://github.com/eWaterCycle/infra).
