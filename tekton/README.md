#### Manually run the pipeline
First, make sure Tekton's CLI `tkn` is installed. Then, in `tekton/`, run
```shell
kubectl apply -f definitions/ && \
kubectl create -f runs/pipelinerun.yaml && \
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

#### Resources for Tasks and Pipelines
There is a catalog of reuseable Tasks from Tekton. [This one](https://github.com/tektoncd/catalog/blob/main/task/git-clone/0.8/samples/git-clone-checking-out-a-branch.yaml) clones a branch then shows its README.md.

There are quite a lot of Pipeline examples [here](https://github.com/tektoncd/pipeline/tree/main/examples/v1beta1).
[One of it](https://github.com/tektoncd/pipeline/blob/main/examples/v1beta1/pipelineruns/workspace-from-volumeclaimtemplate.yaml) shows how to use a workspace to share data between tasks.

#### Resources for Triggers
There are [examples](https://github.com/tektoncd/triggers/tree/main/examples) in Tekton Triggers GitHub [repository](https://github.com/tektoncd/triggers).
