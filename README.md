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
