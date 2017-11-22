# Nexus_Install_Application

## Description:

Install a Nexus Server using a docker image built from a binary artefact in a specified binary repository.

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

| Variable  | Description  | Default  |
|---|---|---|
| **docker_registry** | The name of the docker registry host. |"registry.connect.redhat.com" |
| **nexus_image_name** | The fully qualified name of the Docker image in the Docker registry, including the tag. |"sonatype/nexus-repository-manager:3.6.0-01-rhel" |
| **nexus_port** | The port number Nexus will be listening on the Docker host. | 8081 |
| **nexus_data** | The folder where Nexus will store its data on the Docker host. | /nexus-data |
| **epel_uri** | The base repository of the EPEL repository used to install various dependent packages (only if CentOS is used - for RHEL host assumes managed yum repositories via Satellite. ) | http://dl.fedoraproject.org/pub/epel/7/x86_64/ |
| docker_compose_version** | The version of Docker Compose to be installed to manage the lifecycle of the Nexus Docker container. | 1.17.1 |

### Secrets

The following secrets are required by this role:

| Variable  | Description  |
|---|---|
| **registry_username** | The user name used to log into the Docker registry containing the required Nexus image. |
| **registry_password** | The password used to log into the Docker registry containing the required Nexus image. |

**NOTE**: for testing purposes, a file (i.e. secrets.yml) can be created an placed in the roles /vars folder containing the secret values indicated above. Otherwise the secrets need to be passed as extra variables when executing the role.

### Default Nexus Credentials

Default Nexus credentials, which need to be changed by the Administrator after installation are:

```bash
admin : admin123
```
