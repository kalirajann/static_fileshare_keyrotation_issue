# static_fileshare_keyrotation_issue

- Created AKS Cluster & Storage(File Share) 
- Assigned "storage account key operator service" Role to Kubelet identity at Storage level
- Executed the yaml file & file shares are mounted in POD. Everything Looks good.
- After key rotation, lost the file share access.
- getting permission issue while recreating.

r: code = Internal desc = volume(csi-test-109223) mount "//xxxxx.file.core.windows.net/sample1" on "/var/lib/kubelet/plugins/kubernetes.io/csi/pv/pv-azure-file-static/globalmount" failed with mount failed: exit status 32
Mounting command: mount
Mounting arguments: -t cifs -o dir_mode=0777,file_mode=0777,uid=1000,gid=1000,mfsymlinks,nobrl,actimeo=30,<masked> //xxxxxxx.file.core.windows.net/sample1 /var/lib/kubelet/plugins/kubernetes.io/csi/pv/pv-azure-file-static/globalmount
Output: mount error(13): Permission denied"
  
 ``` 
  PS C:\Users\kavia\manifest\fs> kubectl get secrets --all-namespaces
NAMESPACE         NAME                                             TYPE                                  DATA   AGE
default           default-token-smdwt                              kubernetes.io/service-account-token   3      12h
kube-node-lease   default-token-b22gv                              kubernetes.io/service-account-token   3      12h
kube-public       default-token-d4w8f                              kubernetes.io/service-account-token   3      12h
kube-system       attachdetach-controller-token-c62ds              kubernetes.io/service-account-token   3      12h
kube-system       azure-cloud-provider-token-z26hr                 kubernetes.io/service-account-token   3      12h
kube-system       bootstrap-signer-token-zkmtx                     kubernetes.io/service-account-token   3      12h
kube-system       certificate-controller-token-kvq85               kubernetes.io/service-account-token   3      12h
kube-system       clusterrole-aggregation-controller-token-j9ljc   kubernetes.io/service-account-token   3      12h
kube-system       coredns-autoscaler-token-n45hg                   kubernetes.io/service-account-token   3      12h
kube-system       coredns-token-m7w87                              kubernetes.io/service-account-token   3      12h
kube-system       cronjob-controller-token-zcq6x                   kubernetes.io/service-account-token   3      12h
kube-system       csi-azuredisk-node-sa-token-nv62g                kubernetes.io/service-account-token   3      12h
kube-system       csi-azurefile-node-sa-token-h7lrk                kubernetes.io/service-account-token   3      12h
kube-system       daemon-set-controller-token-fsmhj                kubernetes.io/service-account-token   3      12h
kube-system       default-token-chdd4                              kubernetes.io/service-account-token   3      12h
kube-system       deployment-controller-token-6blxw                kubernetes.io/service-account-token   3      12h
kube-system       disruption-controller-token-r57j2                kubernetes.io/service-account-token   3      12h
  
  ```
kube-system       endpoint-controller-token-h2nkx                  kubernetes.io/service-account-token   3      12h
kube-system       endpointslice-controller-token-r4x8d             kubernetes.io/service-account-token   3      12h
kube-system       endpointslicemirroring-controller-token-wktxj    kubernetes.io/service-account-token   3      12h
kube-system       ephemeral-volume-controller-token-sjgq2          kubernetes.io/service-account-token   3      12h
kube-system       expand-controller-token-vhwvv                    kubernetes.io/service-account-token   3      12h
kube-system       generic-garbage-collector-token-rncfz            kubernetes.io/service-account-token   3      12h
kube-system       horizontal-pod-autoscaler-token-ppfkk            kubernetes.io/service-account-token   3      12h
kube-system       job-controller-token-t4qxm                       kubernetes.io/service-account-token   3      12h
kube-system       kube-proxy-token-v2fwm                           kubernetes.io/service-account-token   3      12h
kube-system       metrics-server-token-gmxr2                       kubernetes.io/service-account-token   3      12h
kube-system       namespace-controller-token-2lkbq                 kubernetes.io/service-account-token   3      12h
kube-system       node-controller-token-skw4w                      kubernetes.io/service-account-token   3      12h
kube-system       omsagent-secret                                  Opaque                                2      12h
kube-system       omsagent-token-qz6rd                             kubernetes.io/service-account-token   3      12h
kube-system       persistent-volume-binder-token-kbtt5             kubernetes.io/service-account-token   3      12h
kube-system       pod-garbage-collector-token-m9p59                kubernetes.io/service-account-token   3      12h
kube-system       pv-protection-controller-token-dstcd             kubernetes.io/service-account-token   3      12h
kube-system       pvc-protection-controller-token-4chp9            kubernetes.io/service-account-token   3      12h
kube-system       replicaset-controller-token-4dfb6                kubernetes.io/service-account-token   3      12h
kube-system       replication-controller-token-tvcsk               kubernetes.io/service-account-token   3      12h
kube-system       resourcequota-controller-token-2m8fj             kubernetes.io/service-account-token   3      12h
kube-system       root-ca-cert-publisher-token-xms47               kubernetes.io/service-account-token   3      12h
kube-system       route-controller-token-nc2w7                     kubernetes.io/service-account-token   3      12h
kube-system       service-account-controller-token-526cr           kubernetes.io/service-account-token   3      12h
kube-system       service-controller-token-dwk8t                   kubernetes.io/service-account-token   3      12h
kube-system       statefulset-controller-token-ct4tk               kubernetes.io/service-account-token   3      12h
kube-system       token-cleaner-token-vjtkd                        kubernetes.io/service-account-token   3      12h
kube-system       ttl-after-finished-controller-token-gpw9f        kubernetes.io/service-account-token   3      12h
kube-system       ttl-controller-token-hqrt9                       kubernetes.io/service-account-token   3      12h
kube-system       tunnelend                                        Opaque                                2      12h
kube-system       tunnelfront                                      Opaque                                2      12h
kube-system       tunnelfront-tls                                  Opaque                                2      12h
kube-system       tunnelfront-token-mhgw9                          kubernetes.io/service-account-token   3      12h
