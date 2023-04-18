#### Create Argo CD Application against edge-mc's Workload Management Workspace (WMW)

The command and output should be similar to
```console
$ argocd app create edgeplacement \
--repo https://github.com/edge-experiments/gitops-source.git \
--path edge-mc/placement/ \
--dest-server https://172.31.31.125:41973/clusters/root:my-org:wmw-1 \
--sync-policy automated
application 'edgeplacement' created
```
