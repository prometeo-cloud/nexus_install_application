# Nexus_Install_Application

## Description:

Install a Nexus Server using a docker image pulled from a Docker registry.

## Behaviour:

**Feature:** Installs Nexus repository.
As a System Admin
I want to install a Nexus binary repository
So that binary artefacts can be managed centrally.

**Scenario:** Pulls Nexus docker image if it does not exists  in the local docker registry
- **Given** a valid Nexus docker images does not exist in the local registry
- **Given** the location of a Docker registry containing Nexus is known
- **Given** the secrets to log into the Docker registry are known
- **When** the installation is requested
- **Then** the image is pulled into the local registry

**Scenario:** Installs Nexus from existing docker image
- **Given** a valid Nexus docker image exists in the local registry
- **Given** there is enough disk space in the file system for storing artefacts
- **When** the installation is requested
- **Then** a docker container running Nexus is started on the docker host
- **Then** a persistent volume is mapped to the host for binary artefact storage


## Configuration:

### Default variables

The following is a list of default variables used by this role.

| Variable  | Description  |
|---|---|
| **nexus_registry** | The name of the docker registry host use to pull the Nexus docker image. |
| **nexus_registry_login** | Whether to enable Docker registry login for secure registries. Its default value is "true". |
| **nexus_image_name** | The fully qualified name of the Docker image in the Docker registry, including the tag. |
| **nexus_port** | The port mapping in the format **host-port:container-port(i.e. 8081)**. |
| **nexus_data** | The folder where Nexus will store its data on the Docker host. |

### Secrets

The following secrets are required by this role:

| Variable  | Description  |
|---|---|
| **nexus_registry_username** | The user name used to log into the Docker registry containing the required Nexus image. |
| **nexus_registry_password** | The password used to log into the Docker registry containing the required Nexus image. |

**NOTE**: for testing purposes, a file (i.e. secrets.yml) can be created an placed in the molecule /vars folder containing the secret values indicated above. Otherwise the secrets need to be passed as extra variables when executing the role.

### Default Nexus Credentials

Default Nexus credentials, which need to be changed by the Administrator after installation are:

```bash
admin : admin123
```

### Testing the role

To test using Docker as a host:

```bash
# requires Docker
# executes the default molecule scenario configured to use the Docker driver  
$ molecule test
```

**NOTE**: requires molecule/default/vars/secrets.yml file to be added manually before the test is run.

To test using Vagrant as a host:

```bash
# requires Vagrant and a virtualisation engine (VirtualBox or libvirt)
# executes the vagrant molecule scenario configured to use the Vagrant driver
$ molecule test -s vagrant
```

**NOTE**: requires molecule/vagrant/vars/secrets.yml file to be added manually before the test is run.
