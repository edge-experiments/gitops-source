Here is an example of Tekton triggers and Tekton pipelines.
In this example, pushing to GitHub triggers a PipelineRun, which in turn ensures some custom resources are up current.

### Manually run the pipeline
The pipeline can be ran without the trigger.

```shell
cd tekton/
kubectl apply -f pipelines/definitions/ && \
kubectl create -f pipelines/runs/ && \
tkn pipelinerun logs ensure-latest-kyst-custom-resources-run -f
```

The output should be similar to
```console
task.tekton.dev/apply configured
task.tekton.dev/git-clone configured
pipeline.tekton.dev/ensure-latest-kyst-custom-resources configured
serviceaccount/tekton-kyst unchanged
clusterrole.rbac.authorization.k8s.io/tekton-kyst unchanged
clusterrolebinding.rbac.authorization.k8s.io/tekton-kyst unchanged
task.tekton.dev/wrap4kyst configured
pipelinerun.tekton.dev/ensure-latest-kyst-custom-resources-run created
[fetch-repo : clone] + '[' false '=' true ]
[fetch-repo : clone] + '[' false '=' true ]
[fetch-repo : clone] + '[' false '=' true ]
[fetch-repo : clone] + CHECKOUT_DIR=/workspace/output/
[fetch-repo : clone] + '[' true '=' true ]
[fetch-repo : clone] + cleandir
[fetch-repo : clone] + '[' -d /workspace/output/ ]
[fetch-repo : clone] + rm -rf '/workspace/output//*'
[fetch-repo : clone] + rm -rf '/workspace/output//.[!.]*'
[fetch-repo : clone] + rm -rf '/workspace/output//..?*'
[fetch-repo : clone] + test -z 
[fetch-repo : clone] + test -z 
[fetch-repo : clone] + test -z 
[fetch-repo : clone] + /ko-app/git-init '-url=https://github.com/edge-experiments/gitops-source.git' '-revision=main' '-refspec=' '-path=/workspace/output/' '-sslVerify=true' '-submodules=true' '-depth=1' '-sparseCheckoutDirectories='
[fetch-repo : clone] {"level":"info","ts":1682994560.014205,"caller":"git/git.go:170","msg":"Successfully cloned https://github.com/edge-experiments/gitops-source.git @ 4598b3d30b848d05c27526a95109a6925c7dbdb5 (grafted, HEAD, origin/main) in path /workspace/output/"}
[fetch-repo : clone] {"level":"info","ts":1682994560.0300348,"caller":"git/git.go:208","msg":"Successfully initialized and updated submodules in path /workspace/output/"}
[fetch-repo : clone] + cd /workspace/output/
[fetch-repo : clone] + git rev-parse HEAD
[fetch-repo : clone] + RESULT_SHA=4598b3d30b848d05c27526a95109a6925c7dbdb5
[fetch-repo : clone] + EXIT_CODE=0
[fetch-repo : clone] + '[' 0 '!=' 0 ]
[fetch-repo : clone] + printf '%s' 4598b3d30b848d05c27526a95109a6925c7dbdb5
[fetch-repo : clone] + printf '%s' https://github.com/edge-experiments/gitops-source.git

[wrap-for-kyst : ls] content of the repository:
[wrap-for-kyst : ls] README.md
[wrap-for-kyst : ls] edge-mc
[wrap-for-kyst : ls] flux
[wrap-for-kyst : ls] kcp
[wrap-for-kyst : ls] kubernetes
[wrap-for-kyst : ls] turbonomic

[wrap-for-kyst : wrap] 2023/05/02 02:29:24 target: k8s
[wrap-for-kyst : wrap] 2023/05/02 02:29:24 Found file: guestbook-ui-deployment.yaml, adding to raw content
[wrap-for-kyst : wrap] 2023/05/02 02:29:24 Found file: guestbook-ui-svc.yaml, adding to raw content

[show-configspec : cat] apiVersion: edge.kyst.kube/v1alpha1
[show-configspec : cat] kind: ConfigSpec
[show-configspec : cat] metadata:
[show-configspec : cat]     name: guestbook
[show-configspec : cat] spec:
[show-configspec : cat]     content:
[show-configspec : cat]         - |
[show-configspec : cat]           apiVersion: apps/v1
[show-configspec : cat]           kind: Deployment
[show-configspec : cat]           metadata:
[show-configspec : cat]             name: guestbook-ui
[show-configspec : cat]             namespace: default
[show-configspec : cat]           spec:
[show-configspec : cat]             replicas: 3
[show-configspec : cat]             revisionHistoryLimit: 3
[show-configspec : cat]             selector:
[show-configspec : cat]               matchLabels:
[show-configspec : cat]                 app: guestbook-ui
[show-configspec : cat]             template:
[show-configspec : cat]               metadata:
[show-configspec : cat]                 labels:
[show-configspec : cat]                   app: guestbook-ui
[show-configspec : cat]               spec:
[show-configspec : cat]                 containers:
[show-configspec : cat]                 - image: gcr.io/heptio-images/ks-guestbook-demo:0.2
[show-configspec : cat]                   name: guestbook-ui
[show-configspec : cat]                   ports:
[show-configspec : cat]                   - containerPort: 80
[show-configspec : cat]                   resources:
[show-configspec : cat]                     limits:
[show-configspec : cat]                       cpu: 100m
[show-configspec : cat]                       memory: 64Mi
[show-configspec : cat]         - |
[show-configspec : cat]           apiVersion: v1
[show-configspec : cat]           kind: Service
[show-configspec : cat]           metadata:
[show-configspec : cat]             name: guestbook-ui
[show-configspec : cat]             namespace: default
[show-configspec : cat]           spec:
[show-configspec : cat]             ports:
[show-configspec : cat]             - port: 80
[show-configspec : cat]               targetPort: 80
[show-configspec : cat]             selector:
[show-configspec : cat]               app: guestbook-ui

[apply-manifests : kubectl-version] Flag --short has been deprecated, and will be removed in the future. The --short output will become the default.
[apply-manifests : kubectl-version] Client Version: v1.27.1
[apply-manifests : kubectl-version] Kustomize Version: v5.0.1

[apply-manifests : kubectl-apply] before applying:
[apply-manifests : kubectl-apply] NAMESPACE   NAME                                          AGE
[apply-manifests : kubectl-apply] default     configspec.edge.kyst.kube/configspec-sample   206d
[apply-manifests : kubectl-apply] 
[apply-manifests : kubectl-apply] NAMESPACE   NAME                                            AGE
[apply-manifests : kubectl-apply] default     devicegroup.edge.kyst.kube/devicegroup-sample   206d
[apply-manifests : kubectl-apply] applying:
[apply-manifests : kubectl-apply] configspec.edge.kyst.kube/guestbook created
[apply-manifests : kubectl-apply] devicegroup.edge.kyst.kube/guestbook1 created
[apply-manifests : kubectl-apply] after applying:
[apply-manifests : kubectl-apply] NAMESPACE   NAME                                          AGE
[apply-manifests : kubectl-apply] default     configspec.edge.kyst.kube/configspec-sample   206d
[apply-manifests : kubectl-apply] default     configspec.edge.kyst.kube/guestbook           0s
[apply-manifests : kubectl-apply] 
[apply-manifests : kubectl-apply] NAMESPACE   NAME                                            AGE
[apply-manifests : kubectl-apply] default     devicegroup.edge.kyst.kube/devicegroup-sample   206d
[apply-manifests : kubectl-apply] default     devicegroup.edge.kyst.kube/guestbook1           0s
```

Remove the pipelinerun:
```shell
kubectl delete pipelinerun ensure-latest-kyst-custom-resources-run
```

Remove the kyst custom resources:
```shell
kubectl delete configspec guestbook
kubectl delete devicegroup guestbook1
```

### Setup triggers for the pipeline
The pipeline can be triggered by a push to GitHub.

This part is a variant of Tekton triggers' [Getting Started](https://github.com/tektoncd/triggers/tree/main/docs/getting-started) tutorial.

This part assumes NGINX Ingress Controller for Kubernetes is inplace.
```console
$ kc -n ingress-nginx get all
NAME                                            READY   STATUS    RESTARTS   AGE
pod/ingress-nginx-controller-7844b9db77-q7m9j   1/1     Running   0          212d

NAME                                         TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)                      AGE
service/ingress-nginx-controller             LoadBalancer   10.99.171.186   <pending>     80:32619/TCP,443:32612/TCP   212d
service/ingress-nginx-controller-admission   ClusterIP      10.99.74.224    <none>        443/TCP                      212d

NAME                                       READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/ingress-nginx-controller   1/1     1            1           212d

NAME                                                  DESIRED   CURRENT   READY   AGE
replicaset.apps/ingress-nginx-controller-7844b9db77   1         1         1       212d
```

Setup RBAC.
```shell
kubectl apply -f triggers/definitions/rbac/admin-role.yaml -f ./definitions/rbac/clusterrolebinding.yaml
kubectl apply -f triggers/definitions/rbac/webhook-role.yaml
```

Ensure the definitions of the pipeline.
```shell
kubectl apply -f pipelines/definitions/
```

Install the example Triggers resources.
```shell
kubectl apply -f triggers/definitions/triggers.yaml
```

Ensure the tasks for creating ingress and GitHub webhook.
```shell
kubectl apply -f triggers/definitions/create-ingress.yaml
kubectl apply -f triggers/definitions/create-webhook.yaml
```

Create the ingress.
```shell
kubectl apply -f triggers/runs/create-ingress.yaml
```

Create a GitHub Personal Access Token with the following access privileges:
- public_repo
- admin:repo_hook

Add the token to `triggers/secret.yaml`. Do NOT base64-encode the token.
Create the secret.
```shell
kubectl apply -f triggers/secret.yaml
```

Create the GitHub webhook.
```shell
kubectl apply -f triggers/runs/create-webhook.yaml
```

Finally, start the entire chain of automation, including the triggers and the pipeline.
```shell
git commit -m "empty commit" --allow-empty && git push
```

Check the log of the PipelineRun
```shell
tkn pipelinerun logs ensure-latest-kyst-custom-resources-run -f
```

Remove the kyst custom resources:
```shell
kubectl delete configspec guestbook
kubectl delete devicegroup guestbook1
```

Remove the pipelinerun:
```shell
kubectl delete pr ensure-latest-kyst-custom-resources-run
```

### Resources for Tasks and Pipelines
There is a [catalog](https://github.com/tektoncd/catalog) of reuseable Tasks from Tekton. [This one](https://github.com/tektoncd/catalog/blob/main/task/git-clone/0.8/samples/git-clone-checking-out-a-branch.yaml) clones a branch then shows its README.md.

There are quite a lot of Pipeline examples [here](https://github.com/tektoncd/pipeline/tree/main/examples/v1beta1).
[One of it](https://github.com/tektoncd/pipeline/blob/main/examples/v1beta1/pipelineruns/workspace-from-volumeclaimtemplate.yaml) shows how to use a workspace to share data between tasks.

### Resources for Triggers
There are [examples](https://github.com/tektoncd/triggers/tree/main/examples) in Tekton Triggers GitHub [repository](https://github.com/tektoncd/triggers).
