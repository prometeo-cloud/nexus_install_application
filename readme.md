# [product_action_subject]

## Description:

Install a Nexus Server using a docker image built from a binary artefact in a specified binary repository.

## Behaviour:

**Feature:** Installs Nexus repository.
As a System Admin
I want to install a Nexus binary repository
So that binary artefacts can be managed centrally.

**Scenario:** Creates Nexus docker image if it does not exists  in the local docker registry
- **Given** a valid Nexus docker images does not exist in the local registry
- **Given** a docker file for the image is defined
- **Given** a binary repository URI containing the Nexusa binary is defined
- **When** the installation is requested
- **Then** the image is build in the local registry 
 
**Scenario:** Installs Nexus from existing docker image
- **Given** a valid Nexus docker image exists in the local registry
- **Given** there is enough disk space in the file system for storing artefacts
- **When** the installation is requested 
- **Then** the binary repository is deployed in a docker container running on the docker host
- **Then** a persistent volume is mapped to the host for binary artefact storage
    

## Configuration:

A list of the external variables used by the role.

| Variable  | Description  | Example  | 
|---|---|---|
| **var1**  | Var1 description  |  Var1 example. |
| **var2**  |   |   |
| **var3**  |   |   |


## Usage:

How to invoke the role from a playbook:

```yaml
- name: Creates Tenant
  include_role:
    name: OpenShift_Create_Tenant
  vars:
    var1: '???'
    var2: '???'
    var3: '???'
```