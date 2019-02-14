# kubevirt-olm
Playground for demonstrating KubeVirt in OLM

# Want to try?

1. Build (and push) a container image yourself (like: `docker build -t
   docker.io/djzager/kubevirt-operators:$(git rev-parse --short HEAD) -f
   Dockerfile .` and `docker push docker.io/djzager/kubevirt-operators:$(git
   rev-parse --short HEAD)`) **OR** choose from
   [lveyde](https://hub.docker.com/r/lveyde/kubevirt-operators/tags) or
   [djzager](https://hub.docker.com/r/djzager/kubevirt-operators/tags) that have
   already been built.
1. Update the `kubevirt-operator.catalogsource.yaml` with your container image
   of choice. Want to know more about the base container image? [check this
   out](https://github.com/operator-framework/operator-registry/)
1. `kubectl create -f kubevirt-operator.catalogsource.yaml` at this point you
   should be able to see the `kubevirt` and `cdi` operators in the UI under
   `Operator Management`. You should also see a pod started for a
   `kubevirt-operators` image started up in the
   `openshift-operator-lifecycle-manager` namespace.
1. (Non-Step, just notes) At this stage, we are making use of features specifically provided by the
   `grpc` type catalogsource. This has the caveat that we'll need to "Subscribe"
   to our operator in the `kubevirt` namespace to align with the ServiceAccount
   that we reference
   [here](registry/kubevirt/0.14.0/kubevirtoperator.clusterrolebinding.yaml) and
   [here](registry/kubevirt/0.14.0/cdi-operator.clusterrolebinding.yaml). With
   the added benefit of allowing us to aggregate roles, like
   [here](registry/kubevirt/0.14.0/kubevirtoperator.clusterrole.yaml).
1. In order to be able to subscribe to our operator in the `kubevirt` namespace
   we must first `kubectl create namespace kubevirt` and `kubectl create -f
   kubevirt-operator.operatorgroup.yaml`.
1. Now we should be able to make a subscription to our operator in the `kubevirt`
   throught the UI or by creating a subscription object. (Maybe want to add a
   subscription to this project for reference)

# Some references

1. Information about the operator-registry image that the `kubevirt-operators` image is
   based on https://github.com/operator-framework/operator-registry/
1. Information about how to build a CSV
   https://github.com/operator-framework/operator-lifecycle-manager/blob/master/Documentation/design/building-your-csv.md
1. The community operators project
   https://github.com/operator-framework/community-operators/
