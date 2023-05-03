#### Tekton Pipelines
`PodSecurityPolicy` was [deprecated](https://kubernetes.io/docs/concepts/security/pod-security-policy/) in Kubernetes v1.21, and removed from k8s v1.25.
I am using k8s v1.25, where the `PodSecurityPolicy` in [the yaml](./pipelines.yaml) doesn't work.
I just removed it from the yaml.
Similarly the `HorizontalPodAutoscaler` is removed from the yaml (see comments there).

With this modified installation, it seems OK with the [Getting Started](https://tekton.dev/docs/getting-started/) tutorial.

I do have options with previous k8s versions by using k3s or Kind. But after thinking twice let me try to continue with my regular k8s first. After all, I want to run Tekton together with kyst, and I don't know: Whether kyst's large footprint can fit into k3s or Kind?

Tekton community already has an issue documented [here](https://github.com/tektoncd/pipeline/issues/4112), but it is not fixed yet as of Sep 20, 2022.

#### Tekton Triggers
Again `PodSecurityPolicy` is there in the official [release](https://storage.googleapis.com/tekton-releases/triggers/latest/release.yaml) of Tekton Triggers, which is removed from k8s v1.25.
I just removed the `tekton-triggers` PodSecurityPolicy from the yaml.
[Here](./triggers.yaml) is a saved copy of the modified installation.

[Installation](https://storage.googleapis.com/tekton-releases/triggers/latest/interceptors.yaml) for interceptors works just fine.
I saved a copy [here](./interceptors.yaml).

#### Installed Components
After installations, the components look similar to
```console
👉 kyst-configurations $ kubectl -n tekton-pipelines get all -oname
pod/tekton-pipelines-controller-5994cbf4c8-xl5jd
pod/tekton-pipelines-webhook-6b46dd7ff8-x9rqq
pod/tekton-triggers-controller-dbb46c886-8txhn
pod/tekton-triggers-core-interceptors-57dd764784-vvmbg
pod/tekton-triggers-webhook-587c7b599d-kz2j9
service/tekton-pipelines-controller
service/tekton-pipelines-webhook
service/tekton-triggers-controller
service/tekton-triggers-core-interceptors
service/tekton-triggers-webhook
deployment.apps/tekton-pipelines-controller
deployment.apps/tekton-pipelines-webhook
deployment.apps/tekton-triggers-controller
deployment.apps/tekton-triggers-core-interceptors
deployment.apps/tekton-triggers-webhook
replicaset.apps/tekton-pipelines-controller-5994cbf4c8
replicaset.apps/tekton-pipelines-webhook-6b46dd7ff8
replicaset.apps/tekton-triggers-controller-dbb46c886
replicaset.apps/tekton-triggers-core-interceptors-57dd764784
replicaset.apps/tekton-triggers-webhook-587c7b599d
```