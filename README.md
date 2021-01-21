# Simple generator for web applications providing a Knative service.yaml file

This generator uses a provided Knative `service.yaml` resource file to deploy a web application as a Knative service using Skaffold with the generated `skaffold.yaml`

You will need to install the following command line tool:

* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
* [skaffold](https://skaffold.dev/docs/install/)

For deploying the app you need a Kubernetes cluster with [Knative serving installed](https://knative.dev/docs/install/any-kubernetes-cluster/).

## Application

### Build the application and deploy to Kubernetes

For a local cluster like Minikube or Docker Desktop you can simply run:

```bash
skaffold run
```

For a remote cluster you need to specify the `default-repo` which is the registry prefix for the image that is being built. For Docker Hub the prefix would be your Docker ID, for other registries it would typically be the registry URL plus your project.

> **NOTE**: You must specify a registry prefix where you have permission to push images.

You can do this globally by running:

```bash
skaffold config set --global default-repo ${REGISTRY_PREFIX}
```

Or, you can set it for the current Kubernetes context:

```bash
skaffold config set default-repo ${REGISTRY_PREFIX}
```

Finally, you can specify it as part of the `run` command:

```bash
skaffold run --default-repo ${REGISTRY_PREFIX} 
```

The `skaffold run` command will build the container image, deploy the application as a Knative service.

You can use `kubectl get all` to verify that the resources were created.

If you leave out the `--port-forward` option then accessing the application's endpoint varies based on the type of Kubernetes cluster and ingress configuration you are using.

### Delete the application

To delete the deployment and the service from your Kubernetes cluster run:

```bash
skaffold delete
```

## Generator

`k8s-simple new` creates

* A `skaffold.yaml` file
