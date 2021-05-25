# kustomize_example
Easy example of using kustomize to produce environment specific manifests.

# Directory setup

## kustomization.yaml
This is the kustomize file to configure what will be included in the kustomize and what options to set.
Each directory should have a kustomize.yaml file to specify things like what base to use, if needed. Which labels to set for all resources. Additional resources to include.

## ./base
This is the base layer of manifests for shared config options between environments.

## ./prod
The prod layer of config options specific to the production environment

# Example
To generate the manifest output for development/base:

`kubectl kustomize ./base`

To generate the manifests output using the production overlay layer:

`kubectl kustomize ./prod`

NOTE: Several productioin specific options have been set or overridden the development one like:
 - namespace
 - environment variables
 - net new resources
 - node affinities
 - rollout strategies

# Applying
Applying env specific manifests to the cluster

development/base:

`kubectl apply -k ./base`

production:

`kubectl apply -k ./prod`