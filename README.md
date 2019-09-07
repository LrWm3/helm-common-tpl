# helm chart example

This repo contains a helm chart which encompasses all requirements for an on-prem microservice-based system.

## Overview

This helm-repo is divided into the following categories

### common-tpl

`./common-tpl` will contain common templates for concrete apps built with helm. 
Its purpose is to reduce the amount of duplicated yaml for values which are not
expected or intended to frequently change between application deployments. examples
include common ports, labels and general service and virtual service configurations.

application charts will merely need to import `standard-app` from the common template with `values.yml` as an argument to fully template the app.

It will also be possible to template an app using the individual template components for special cases; however the `standard-app` template is intended to cover
all standard deployment requirements.

#### common-tpl requirements

- [ ] TODO, write out common-tpl requirements (ie, dynamically reference appropriate location for common-tpl depending on configuration, and more)

### Infrastructure

`./infrastructure` will contain lightly modified helm charts for infrastructure level helm components

example infrastructure-level components include:

- a docker registry + a helm registry in a nexus repo
- a database, mongo and postgres via CRD
- a message bus, kafka via strimzi-kafka
- a service mesh, istio and kaili
- a network level cache, memd or redis depending on what makes sense
- a security-layer, via istio destination rules + keycloak + ldap
- a distributed file-system, nfs if i cant find anything faster or better
- a git repository, as a git-based database layer, optionally as an oncloud git-repository and git-runner, maybe as a configstore
- a testbed runner, gitlab + katalon + cucumber tests

#### common infrastructure-level requirements

Below are common infrastructure-level requirements, shared among all infrastructure-level components.
These requirements may require extending off-the-shelf components.

- [ ] infrastructure-level components will be able to be labeled to operate on specific nodes
- [ ] infrastructure-level components will have their resource requests prioritized over other services on scheduled nodes
- [ ] infrastructure-level components will have their relative priority in relation to other infrastructure components configurable, to allow prioritization of different infrastructure components
- [ ] infrastructure components must have the option of being deployed to particular namespaces

### apps

Apps are example applications meant to demonstrate various kinds of functionality provided by either infrastructure or common-tpl. 
In a real application, these would really do things.

Apps also have custom go code associated to make for better examples.

#### App requirements

- [ ] Apps must have tests demonstrating their function works

### umbrellas

umbrella charts are meant to demonstrate the orchestration of sub-charts using helm.

There are currently three umbrella-charts:
- umbrella-app is meant to deploy all app-charts
- umbrella-infrastructure is meant to deploy all infrastructure charts
- umbrella-all is meant to deploy all infrastructure charts, including CRD, and then deploy all app-charts

difficulties with this:

- unclear if charts can deploy apps across different namespaces, creating namespaces if they are not available, will need this functionality

#### requirements

later, 2% bat left

### cluster-installer

This component installs kubernetes across n nodes, and then run the helm-charts to set up all apps.
It is able to run without any resources external to this git project. All dependencies, including
docker images and helm charts must be available inside this project. This should not make deploying
using an external helm chart more difficult however.

#### cluster installer requirements

- [ ] can install without any external resources
- [ ] no time-sync issues
- [ ] installs kubernetes and ntp if required, configures firewall rules, but otherwise stays out of the way and lets the helm-chart do as much as possible


