### Disclaimer
This repo is very new, experimental, and not yet continuously integrated or tested to the degree we'd like.

### Pre-requisites

1. `minikube` (`brew install minikube`)
1. `helm` (`brew install kubernetes-helm`) We require helm 3.0.0+ to install the
   postgres & minio data stores in your minikube.
1. To ensure cloud controller submodule is up-to-date run `git submodule update --init`
1. Run `./scripts/setup.sh` to enable the minikube registry and add it to your
   local docker daemon's list of insecure registries.
1. Restart your docker daemon if the script thinks you should.


### Installing dependencies and CAPI

CAPI requires a database and blobstore.  We chose to use Postgres and Minio for
those dependencies, respectively.  Both have stable `helm` charts, so that is
the approach we use to install them.


1. `minikube start` to make sure `minikube` is up and running
1. `./scripts/deploy.sh` to deploy the dependencies and CAPI
1. Optionally, you can supply custom configuration as an additional argument.  E.g.:
        `./scripts/deploy.sh my-custom-values.yaml`.  
        See an example of custom configuration here: [custom-values.yml](https://github.com/cloudfoundry/capi-k8s-release/blob/master/scripts/custom-values.yaml)


### Rolling out changes to CAPI

1. `./scripts/build-and-rollout-capi.sh` will take the `cloud_controller_ng` code in
   the `src/cloud_controller_ng` submodule, build a docker image with it, and
   roll the new image out to the `minikube` cluster.
1. Optionally, you can supply custom configuration as an additional argument.  E.g.:
        `./scripts/build-and-rollout-capi.sh my-custom-values.yaml`.  

### Known Issues

1. If you see an issue with helm (eg. tiller not found) then update to the latest helm version (`brew upgrade helm`)

