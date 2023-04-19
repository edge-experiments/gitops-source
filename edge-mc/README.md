#### Create Argo CD Applications against edge-mc's Inventory Management Workspace (IMW)
Create two Locations. The command and output should be similar to
```console
$ argocd app create locations \
--repo https://github.com/edge-experiments/gitops-source.git \
--path edge-mc/locations/ \
--dest-server https://172.31.31.125:41973/clusters/root:imw-1 \
--sync-policy automated
application 'locations' created
```

Create two SyncTargets. The command and output should be similar to
```console
$ argocd app create synctargets \
--repo https://github.com/edge-experiments/gitops-source.git \
--path edge-mc/synctargets/ \
--dest-server https://172.31.31.125:41973/clusters/root:imw-1 \
--sync-policy automated
application 'synctargets' created
```

#### Create Argo CD Application against edge-mc's Workload Management Workspace (WMW)
Create an EdgePlacement. The command and output should be similar to
```console
$ argocd app create edgeplacement \
--repo https://github.com/edge-experiments/gitops-source.git \
--path edge-mc/placements/ \
--dest-server https://172.31.31.125:41973/clusters/root:my-org:wmw-1 \
--sync-policy automated
application 'edgeplacement' created
```

Create a Namespace. The command and output should be similar to
```console
$ argocd app create namespace \
--repo https://github.com/edge-experiments/gitops-source.git \
--path edge-mc/namespaces/ \
--dest-server https://172.31.31.125:41973/clusters/root:my-org:wmw-1 \
--sync-policy automated
application 'namespace' created
```

Create a Deployment for 'cpumemload'. The command and output should be similar to
```console
$ argocd app create cpumemload \
--repo https://github.com/edge-experiments/gitops-source.git \
--path edge-mc/workloads/cpumemload/ \
--dest-server https://172.31.31.125:41973/clusters/root:my-org:wmw-1 \
--sync-policy automated
application 'cpumemload' created
```
