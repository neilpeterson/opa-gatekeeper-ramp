# Kubernetes Gatekeeper Demo

Create constraint template that enforces a label on all namespaces.

```
> kubectl create -f constraint-template-label.yaml

constrainttemplate.templates.gatekeeper.sh/clusterrequiredlabels created
```

Create the constraint, which includes the expected label name as a parameter

```
> kubectl create -f constraint-label.yaml

clusterrequiredlabels.constraints.gatekeeper.sh/costcenterlabelrequired created
```

Attempt to create a namespace without a label named `region`.

```
> kubectl create -f ns-no-label.yaml

Error from server (Forbidden): error when creating "ns-no-label.yaml": admission webhook "validation.gatekeeper.sh" denied the request: [costcenterlabelrequired] you must provide labels: {"region"}
```

Create a namespace with label region=westus

```
> kubectl create -f ns-with-label.yaml

namespace/demo created
```