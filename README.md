- **STEP**: install velero client

- **STEP**: install velero server

Execute this command, by default velero will be installed in the velero namespace of the cluster

```
$ velero install \
    --provider aws \
    --plugins velero/velero-plugin-for-aws:v1.11.0 \
    --bucket velero \
    --secret-file ./credentials-velero \
    --use-volume-snapshots=false \
    --backup-location-config region=minio,s3ForcePathStyle="true",s3Url=https://sample-hl.default.svc:9000,insecureSkipTLSVerify="true"
CustomResourceDefinition/backuprepositories.velero.io: attempting to create resource
CustomResourceDefinition/backuprepositories.velero.io: attempting to create resource client
CustomResourceDefinition/backuprepositories.velero.io: created
CustomResourceDefinition/backups.velero.io: attempting to create resource
CustomResourceDefinition/backups.velero.io: attempting to create resource client
CustomResourceDefinition/backups.velero.io: created
CustomResourceDefinition/backupstoragelocations.velero.io: attempting to create resource
CustomResourceDefinition/backupstoragelocations.velero.io: attempting to create resource client
CustomResourceDefinition/backupstoragelocations.velero.io: created
CustomResourceDefinition/deletebackuprequests.velero.io: attempting to create resource
CustomResourceDefinition/deletebackuprequests.velero.io: attempting to create resource client
CustomResourceDefinition/deletebackuprequests.velero.io: created
CustomResourceDefinition/downloadrequests.velero.io: attempting to create resource
CustomResourceDefinition/downloadrequests.velero.io: attempting to create resource client
CustomResourceDefinition/downloadrequests.velero.io: created
CustomResourceDefinition/podvolumebackups.velero.io: attempting to create resource
CustomResourceDefinition/podvolumebackups.velero.io: attempting to create resource client
CustomResourceDefinition/podvolumebackups.velero.io: created
CustomResourceDefinition/podvolumerestores.velero.io: attempting to create resource
CustomResourceDefinition/podvolumerestores.velero.io: attempting to create resource client
CustomResourceDefinition/podvolumerestores.velero.io: created
CustomResourceDefinition/restores.velero.io: attempting to create resource
CustomResourceDefinition/restores.velero.io: attempting to create resource client
CustomResourceDefinition/restores.velero.io: created
CustomResourceDefinition/schedules.velero.io: attempting to create resource
CustomResourceDefinition/schedules.velero.io: attempting to create resource client
CustomResourceDefinition/schedules.velero.io: created
CustomResourceDefinition/serverstatusrequests.velero.io: attempting to create resource
CustomResourceDefinition/serverstatusrequests.velero.io: attempting to create resource client
CustomResourceDefinition/serverstatusrequests.velero.io: created
CustomResourceDefinition/volumesnapshotlocations.velero.io: attempting to create resource
CustomResourceDefinition/volumesnapshotlocations.velero.io: attempting to create resource client
CustomResourceDefinition/volumesnapshotlocations.velero.io: created
CustomResourceDefinition/datadownloads.velero.io: attempting to create resource
CustomResourceDefinition/datadownloads.velero.io: attempting to create resource client
CustomResourceDefinition/datadownloads.velero.io: created
CustomResourceDefinition/datauploads.velero.io: attempting to create resource
CustomResourceDefinition/datauploads.velero.io: attempting to create resource client
CustomResourceDefinition/datauploads.velero.io: created
Waiting for resources to be ready in cluster...
Namespace/velero: attempting to create resource
Namespace/velero: attempting to create resource client
Namespace/velero: created
ClusterRoleBinding/velero: attempting to create resource
ClusterRoleBinding/velero: attempting to create resource client
ClusterRoleBinding/velero: created
ServiceAccount/velero: attempting to create resource
ServiceAccount/velero: attempting to create resource client
ServiceAccount/velero: created
Secret/cloud-credentials: attempting to create resource
Secret/cloud-credentials: attempting to create resource client
Secret/cloud-credentials: created
BackupStorageLocation/default: attempting to create resource
BackupStorageLocation/default: attempting to create resource client
BackupStorageLocation/default: created
Deployment/velero: attempting to create resource
Deployment/velero: attempting to create resource client
Deployment/velero: created
Velero is installed! ⛵ Use 'kubectl logs deployment/velero -n velero' to view the status.
```

```
$ kubectl logs deployment/velero -n velero
Defaulted container "velero" out of: velero, velero-velero-plugin-for-aws (init)
time="2024-12-22T19:28:07Z" level=info msg="setting log-level to INFO" logSource="pkg/cmd/server/server.go:110"
time="2024-12-22T19:28:07Z" level=info msg="Starting Velero server v1.15.0 (1d4f1475975b5107ec35f4d19ff17f7d1fcb3edf-dirty)" logSource="pkg/cmd/server/server.go:112"
time="2024-12-22T19:28:07Z" level=info msg="1 feature flags enabled []" logSource="pkg/cmd/server/server.go:114"
time="2024-12-22T19:28:07Z" level=info msg="plugin process exited" cmd=/velero id=15 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/velero
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=BackupItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/crd-remap-version
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=BackupItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/pod
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=BackupItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/pv
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=BackupItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/service-account
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=BackupItemActionV2 logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/csi-pvc-backupper
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=BackupItemActionV2 logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/csi-volumesnapshot-backupper
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=BackupItemActionV2 logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/csi-volumesnapshotclass-backupper
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=BackupItemActionV2 logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/csi-volumesnapshotcontent-backupper
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/add-pv-from-pvc
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/add-pvc-from-pod
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/admission-webhook-configuration
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/apiservice
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/change-image-name
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/change-pvc-node-selector
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/change-storage-class
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/cluster-role-bindings
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/crd-preserve-fields
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/dataupload
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/init-restore-hook
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/job
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/pod
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/pod-volume-restore
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/role-bindings
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/secret
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/service
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/service-account
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemActionV2 logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/csi-pvc-restorer
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemActionV2 logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/csi-volumesnapshot-restorer
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemActionV2 logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/csi-volumesnapshotclass-restorer
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=RestoreItemActionV2 logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/csi-volumesnapshotcontent-restorer
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=DeleteItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/csi-volumesnapshot-delete
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=DeleteItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/csi-volumesnapshotcontent-delete
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=DeleteItemAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/dataupload-delete
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=ItemBlockAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/pod
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=ItemBlockAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/pvc
time="2024-12-22T19:28:07Z" level=info msg="registering plugin" command=/velero kind=ItemBlockAction logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/service-account
time="2024-12-22T19:28:08Z" level=info msg="plugin process exited" cmd=/plugins/velero-plugin-for-aws id=25 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/plugins/velero-plugin-for-aws
time="2024-12-22T19:28:08Z" level=info msg="registering plugin" command=/plugins/velero-plugin-for-aws kind=VolumeSnapshotter logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/aws
time="2024-12-22T19:28:08Z" level=info msg="registering plugin" command=/plugins/velero-plugin-for-aws kind=ObjectStore logSource="pkg/plugin/clientmgmt/process/registry.go:101" name=velero.io/aws
time="2024-12-22T19:28:08Z" level=info msg="Checking existence of namespace." logSource="pkg/cmd/server/server.go:387" namespace=velero
time="2024-12-22T19:28:08Z" level=info msg="Namespace exists" logSource="pkg/cmd/server/server.go:393" namespace=velero
time="2024-12-22T19:28:08Z" level=info msg="Checking existence of Velero custom resource definitions" logSource="pkg/cmd/server/server.go:422"
time="2024-12-22T19:28:08Z" level=info msg="Found custom resource" kind=Schedule logSource="pkg/cmd/server/server.go:433"
time="2024-12-22T19:28:08Z" level=info msg="Found custom resource" kind=BackupRepository logSource="pkg/cmd/server/server.go:433"
time="2024-12-22T19:28:08Z" level=info msg="Found custom resource" kind=Backup logSource="pkg/cmd/server/server.go:433"
time="2024-12-22T19:28:08Z" level=info msg="Found custom resource" kind=BackupStorageLocation logSource="pkg/cmd/server/server.go:433"
time="2024-12-22T19:28:08Z" level=info msg="Found custom resource" kind=DeleteBackupRequest logSource="pkg/cmd/server/server.go:433"
time="2024-12-22T19:28:08Z" level=info msg="Found custom resource" kind=PodVolumeRestore logSource="pkg/cmd/server/server.go:433"
time="2024-12-22T19:28:08Z" level=info msg="Found custom resource" kind=Restore logSource="pkg/cmd/server/server.go:433"
time="2024-12-22T19:28:08Z" level=info msg="Found custom resource" kind=DownloadRequest logSource="pkg/cmd/server/server.go:433"
time="2024-12-22T19:28:08Z" level=info msg="Found custom resource" kind=PodVolumeBackup logSource="pkg/cmd/server/server.go:433"
time="2024-12-22T19:28:08Z" level=info msg="Found custom resource" kind=VolumeSnapshotLocation logSource="pkg/cmd/server/server.go:433"
time="2024-12-22T19:28:08Z" level=info msg="Found custom resource" kind=ServerStatusRequest logSource="pkg/cmd/server/server.go:433"
time="2024-12-22T19:28:08Z" level=info msg="Found custom resource" kind=DataDownload logSource="pkg/cmd/server/server.go:433"
time="2024-12-22T19:28:08Z" level=info msg="Found custom resource" kind=DataUpload logSource="pkg/cmd/server/server.go:433"
time="2024-12-22T19:28:08Z" level=info msg="All Velero custom resource definitions exist" logSource="pkg/cmd/server/server.go:451"
time="2024-12-22T19:28:08Z" level=warning msg="Velero node agent not found; pod volume backups/restores will not work until it's created" logSource="pkg/cmd/server/server.go:458"
time="2024-12-22T19:28:09Z" level=info msg="Starting controllers" logSource="pkg/cmd/server/server.go:492"
time="2024-12-22T19:28:09Z" level=info msg="Starting metric server at address [:8085]" logSource="pkg/cmd/server/server.go:497"
time="2024-12-22T19:28:09Z" level=info msg="Server starting..." logSource="pkg/cmd/server/server.go:861"
time="2024-12-22T19:28:09Z" level=info msg="Starting metrics server" logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" logger=controller-runtime.metrics
time="2024-12-22T19:28:09Z" level=info msg="Serving metrics server" bindAddress=":8080" logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" logger=controller-runtime.metrics secure=false
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=backupstoragelocation controllerGroup=velero.io controllerKind=BackupStorageLocation logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.BackupStorageLocation"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=backupstoragelocation controllerGroup=velero.io controllerKind=BackupStorageLocation logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.BackupStorageLocationList"
time="2024-12-22T19:28:09Z" level=info msg="Starting Controller" controller=backupstoragelocation controllerGroup=velero.io controllerKind=BackupStorageLocation logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=deletebackuprequest controllerGroup=velero.io controllerKind=DeleteBackupRequest logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.DeleteBackupRequest"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=deletebackuprequest controllerGroup=velero.io controllerKind=DeleteBackupRequest logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.DeleteBackupRequestList"
time="2024-12-22T19:28:09Z" level=info msg="Starting Controller" controller=deletebackuprequest controllerGroup=velero.io controllerKind=DeleteBackupRequest logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=backup controllerGroup=velero.io controllerKind=Backup logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.Backup"
time="2024-12-22T19:28:09Z" level=info msg="Starting Controller" controller=backup controllerGroup=velero.io controllerKind=Backup logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=backup controllerGroup=velero.io controllerKind=Backup logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.Backup"
time="2024-12-22T19:28:09Z" level=info msg="Starting Controller" controller=backup controllerGroup=velero.io controllerKind=Backup logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=backupstoragelocation controllerGroup=velero.io controllerKind=BackupStorageLocation logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.BackupStorageLocation"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=backupstoragelocation controllerGroup=velero.io controllerKind=BackupStorageLocation logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.BackupStorageLocationList"
time="2024-12-22T19:28:09Z" level=info msg="Starting Controller" controller=backupstoragelocation controllerGroup=velero.io controllerKind=BackupStorageLocation logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=backup controllerGroup=velero.io controllerKind=Backup logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.Backup"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=backup controllerGroup=velero.io controllerKind=Backup logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.BackupList"
time="2024-12-22T19:28:09Z" level=info msg="Starting Controller" controller=backup controllerGroup=velero.io controllerKind=Backup logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=backuprepository controllerGroup=velero.io controllerKind=BackupRepository logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.BackupRepository"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=downloadrequest controllerGroup=velero.io controllerKind=DownloadRequest logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.DownloadRequest"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=downloadrequest controllerGroup=velero.io controllerKind=DownloadRequest logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.DownloadRequestList"
time="2024-12-22T19:28:09Z" level=info msg="Starting Controller" controller=downloadrequest controllerGroup=velero.io controllerKind=DownloadRequest logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=restore controllerGroup=velero.io controllerKind=Restore logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.Restore"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=restore controllerGroup=velero.io controllerKind=Restore logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.RestoreList"
time="2024-12-22T19:28:09Z" level=info msg="Starting Controller" controller=restore controllerGroup=velero.io controllerKind=Restore logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=backuprepository controllerGroup=velero.io controllerKind=BackupRepository logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.BackupRepositoryList"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=restore controllerGroup=velero.io controllerKind=Restore logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.Restore"
time="2024-12-22T19:28:09Z" level=info msg="Starting Controller" controller=restore controllerGroup=velero.io controllerKind=Restore logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=backup controllerGroup=velero.io controllerKind=Backup logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.Backup"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=backup controllerGroup=velero.io controllerKind=Backup logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.BackupList"
time="2024-12-22T19:28:09Z" level=info msg="Starting Controller" controller=backup controllerGroup=velero.io controllerKind=Backup logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=backuprepository controllerGroup=velero.io controllerKind=BackupRepository logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.BackupStorageLocation"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=schedule controllerGroup=velero.io controllerKind=Schedule logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.Schedule"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=serverstatusrequest controllerGroup=velero.io controllerKind=ServerStatusRequest logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.ServerStatusRequest"
time="2024-12-22T19:28:09Z" level=info msg="Starting Controller" controller=serverstatusrequest controllerGroup=velero.io controllerKind=ServerStatusRequest logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108"
time="2024-12-22T19:28:09Z" level=info msg="Starting Controller" controller=backuprepository controllerGroup=velero.io controllerKind=BackupRepository logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=restore controllerGroup=velero.io controllerKind=Restore logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.Restore"
time="2024-12-22T19:28:09Z" level=info msg="Starting EventSource" controller=schedule controllerGroup=velero.io controllerKind=Schedule logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" source="kind source: *v1.ScheduleList"
time="2024-12-22T19:28:09Z" level=info msg="Starting Controller" controller=schedule controllerGroup=velero.io controllerKind=Schedule logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108"
time="2024-12-22T19:28:09Z" level=info msg="Starting Controller" controller=restore controllerGroup=velero.io controllerKind=Restore logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108"
time="2024-12-22T19:28:09Z" level=info msg="Starting workers" controller=backupstoragelocation controllerGroup=velero.io controllerKind=BackupStorageLocation logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" worker count=1
time="2024-12-22T19:28:09Z" level=info msg="Starting workers" controller=backup controllerGroup=velero.io controllerKind=Backup logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" worker count=1
time="2024-12-22T19:28:09Z" level=info msg="Starting workers" controller=deletebackuprequest controllerGroup=velero.io controllerKind=DeleteBackupRequest logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" worker count=1
time="2024-12-22T19:28:09Z" level=info msg="Starting workers" controller=backup controllerGroup=velero.io controllerKind=Backup logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" worker count=1
time="2024-12-22T19:28:09Z" level=info msg="Starting workers" controller=restore controllerGroup=velero.io controllerKind=Restore logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" worker count=1
time="2024-12-22T19:28:09Z" level=info msg="Starting workers" controller=restore controllerGroup=velero.io controllerKind=Restore logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" worker count=1
time="2024-12-22T19:28:09Z" level=info msg="Starting workers" controller=backupstoragelocation controllerGroup=velero.io controllerKind=BackupStorageLocation logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" worker count=1
time="2024-12-22T19:28:09Z" level=info msg="Starting workers" controller=serverstatusrequest controllerGroup=velero.io controllerKind=ServerStatusRequest logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" worker count=10
time="2024-12-22T19:28:09Z" level=info msg="Starting workers" controller=backuprepository controllerGroup=velero.io controllerKind=BackupRepository logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" worker count=1
time="2024-12-22T19:28:09Z" level=info msg="Starting workers" controller=backup controllerGroup=velero.io controllerKind=Backup logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" worker count=1
time="2024-12-22T19:28:09Z" level=info msg="Starting workers" controller=downloadrequest controllerGroup=velero.io controllerKind=DownloadRequest logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" worker count=1
time="2024-12-22T19:28:09Z" level=info msg="Starting workers" controller=schedule controllerGroup=velero.io controllerKind=Schedule logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" worker count=1
time="2024-12-22T19:28:09Z" level=info msg="Starting workers" controller=backup controllerGroup=velero.io controllerKind=Backup logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" worker count=1
time="2024-12-22T19:28:09Z" level=info msg="Starting workers" controller=restore controllerGroup=velero.io controllerKind=Restore logSource="/go/pkg/mod/github.com/bombsimon/logrusr/v3@v3.0.0/logrusr.go:108" worker count=1
time="2024-12-22T19:28:09Z" level=info msg="Validating BackupStorageLocation" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:142"
time="2024-12-22T19:28:09Z" level=info msg="BackupStorageLocations is valid, marking as available" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:127"
time="2024-12-22T19:28:09Z" level=info msg="plugin process exited" backupLocation=velero/default cmd=/plugins/velero-plugin-for-aws controller=backup-sync id=41 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/plugins/velero-plugin-for-aws
time="2024-12-22T19:28:09Z" level=error msg="Current BackupStorageLocations available/unavailable/unknown: 0/0/1)" controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:181"
time="2024-12-22T19:28:09Z" level=info msg="plugin process exited" backup-storage-location=velero/default cmd=/plugins/velero-plugin-for-aws controller=backup-storage-location id=37 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/plugins/velero-plugin-for-aws
time="2024-12-22T19:28:09Z" level=info msg="Validating BackupStorageLocation" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:142"
time="2024-12-22T19:28:09Z" level=info msg="BackupStorageLocations is valid, marking as available" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:127"
time="2024-12-22T19:28:09Z" level=info msg="plugin process exited" backup-storage-location=velero/default cmd=/plugins/velero-plugin-for-aws controller=backup-storage-location id=57 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/plugins/velero-plugin-for-aws
time="2024-12-22T19:29:09Z" level=info msg="Validating BackupStorageLocation" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:142"
time="2024-12-22T19:29:09Z" level=info msg="BackupStorageLocations is valid, marking as available" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:127"
time="2024-12-22T19:29:09Z" level=info msg="plugin process exited" backup-storage-location=velero/default cmd=/plugins/velero-plugin-for-aws controller=backup-storage-location id=72 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/plugins/velero-plugin-for-aws
time="2024-12-22T19:29:09Z" level=info msg="plugin process exited" backupLocation=velero/default cmd=/plugins/velero-plugin-for-aws controller=backup-sync id=67 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/plugins/velero-plugin-for-aws
time="2024-12-22T19:29:15Z" level=info msg="Setting up backup log" backup=velero/nginx-backup logSource="pkg/controller/backup_controller.go:605"
time="2024-12-22T19:29:15Z" level=info msg="Setting up backup temp file" backup=velero/nginx-backup logSource="pkg/controller/backup_controller.go:616"
time="2024-12-22T19:29:15Z" level=info msg="Setting up plugin manager" backup=velero/nginx-backup logSource="pkg/controller/backup_controller.go:623"
time="2024-12-22T19:29:15Z" level=info msg="Getting backup item actions" backup=velero/nginx-backup logSource="pkg/controller/backup_controller.go:627"
time="2024-12-22T19:29:15Z" level=info msg="Getting ItemBlock actions" backup=velero/nginx-backup logSource="pkg/controller/backup_controller.go:632"
time="2024-12-22T19:29:15Z" level=info msg="Setting up backup store to check for backup existence" backup=velero/nginx-backup logSource="pkg/controller/backup_controller.go:637"
time="2024-12-22T19:29:15Z" level=info msg="Writing backup version file" backup=velero/nginx-backup logSource="pkg/backup/backup.go:238"
time="2024-12-22T19:29:15Z" level=info msg="Including namespaces: *" backup=velero/nginx-backup logSource="pkg/backup/backup.go:244"
time="2024-12-22T19:29:15Z" level=info msg="Excluding namespaces: <none>" backup=velero/nginx-backup logSource="pkg/backup/backup.go:245"
time="2024-12-22T19:29:15Z" level=info msg="Including resources: *" backup=velero/nginx-backup logSource="pkg/util/collections/includes_excludes.go:506"
time="2024-12-22T19:29:15Z" level=info msg="Excluding resources: <none>" backup=velero/nginx-backup logSource="pkg/util/collections/includes_excludes.go:507"
time="2024-12-22T19:29:15Z" level=info msg="Backing up all volumes using pod volume backup: false" backup=velero/nginx-backup logSource="pkg/backup/backup.go:263"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:349" resource=pods
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=pods
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource pods was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 3 items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=pods
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:349" resource=persistentvolumeclaims
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=persistentvolumeclaims
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource persistentvolumeclaims was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=persistentvolumeclaims
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:349" resource=persistentvolumes
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=persistentvolumes
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource persistentvolumes was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=persistentvolumes
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:349" resource=limitranges
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=limitranges
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource limitranges was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=limitranges
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:349" resource=namespaces
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:349" resource=nodes
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=nodes
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource nodes was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=nodes
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:349" resource=configmaps
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=configmaps
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource configmaps was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=configmaps
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:349" resource=secrets
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=secrets
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource secrets was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=secrets
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:349" resource=endpoints
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=endpoints
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource endpoints was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 1 items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=endpoints
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:349" resource=resourcequotas
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=resourcequotas
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource resourcequotas was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=resourcequotas
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:349" resource=events
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=events
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource events was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=events
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:349" resource=replicationcontrollers
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=replicationcontrollers
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource replicationcontrollers was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=replicationcontrollers
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:349" resource=podtemplates
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=podtemplates
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource podtemplates was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=podtemplates
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:349" resource=serviceaccounts
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=serviceaccounts
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource serviceaccounts was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=serviceaccounts
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:349" resource=services
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=services
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource services was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 1 items" backup=velero/nginx-backup group=v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=services
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=apiregistration.k8s.io/v1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=apiregistration.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=apiservices
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=apiregistration.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=apiservices
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource apiservices.apiregistration.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=apiregistration.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=apiservices
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=apps/v1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=apps/v1 logSource="pkg/backup/item_collector.go:349" resource=daemonsets
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=apps/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=daemonsets
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource daemonsets.apps was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=apps/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=daemonsets
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=apps/v1 logSource="pkg/backup/item_collector.go:349" resource=deployments
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=apps/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=deployments
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource deployments.apps was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 2 items" backup=velero/nginx-backup group=apps/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=deployments
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=apps/v1 logSource="pkg/backup/item_collector.go:349" resource=controllerrevisions
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=apps/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=controllerrevisions
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource controllerrevisions.apps was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=apps/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=controllerrevisions
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=apps/v1 logSource="pkg/backup/item_collector.go:349" resource=replicasets
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=apps/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=replicasets
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource replicasets.apps was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 2 items" backup=velero/nginx-backup group=apps/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=replicasets
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=apps/v1 logSource="pkg/backup/item_collector.go:349" resource=statefulsets
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=apps/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=statefulsets
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource statefulsets.apps was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=apps/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=statefulsets
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=events.k8s.io/v1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=events.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=events
time="2024-12-22T19:29:15Z" level=info msg="Skipping resource because it cohabitates and we've already processed it" backup=velero/nginx-backup cohabitatingResource1=events cohabitatingResource2=events.events.k8s.io group=events.k8s.io/v1 logSource="pkg/backup/item_collector.go:428" resource=events
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=autoscaling/v2 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=autoscaling/v2 logSource="pkg/backup/item_collector.go:349" resource=horizontalpodautoscalers
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=autoscaling/v2 logSource="pkg/backup/item_collector.go:522" namespace= resource=horizontalpodautoscalers
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource horizontalpodautoscalers.autoscaling was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=autoscaling/v2 logSource="pkg/backup/item_collector.go:558" namespace= resource=horizontalpodautoscalers
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=batch/v1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=batch/v1 logSource="pkg/backup/item_collector.go:349" resource=jobs
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=batch/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=jobs
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource jobs.batch was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=batch/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=jobs
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=batch/v1 logSource="pkg/backup/item_collector.go:349" resource=cronjobs
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=batch/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=cronjobs
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource cronjobs.batch was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=batch/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=cronjobs
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=certificates.k8s.io/v1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=certificates.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=certificatesigningrequests
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=certificates.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=certificatesigningrequests
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource certificatesigningrequests.certificates.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=certificates.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=certificatesigningrequests
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=networking.k8s.io/v1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=networking.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=networkpolicies
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=networking.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=networkpolicies
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource networkpolicies.networking.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=networking.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=networkpolicies
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=networking.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=ingresses
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=networking.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=ingresses
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource ingresses.networking.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=networking.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=ingresses
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=networking.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=ingressclasses
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=networking.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=ingressclasses
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource ingressclasses.networking.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=networking.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=ingressclasses
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=policy/v1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=policy/v1 logSource="pkg/backup/item_collector.go:349" resource=poddisruptionbudgets
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=policy/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=poddisruptionbudgets
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource poddisruptionbudgets.policy was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=policy/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=poddisruptionbudgets
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=rbac.authorization.k8s.io/v1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=rbac.authorization.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=roles
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=rbac.authorization.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=roles
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource roles.rbac.authorization.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=rbac.authorization.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=roles
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=rbac.authorization.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=clusterrolebindings
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=rbac.authorization.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=clusterrolebindings
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource clusterrolebindings.rbac.authorization.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=rbac.authorization.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=clusterrolebindings
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=rbac.authorization.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=rolebindings
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=rbac.authorization.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=rolebindings
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource rolebindings.rbac.authorization.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=rbac.authorization.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=rolebindings
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=rbac.authorization.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=clusterroles
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=rbac.authorization.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=clusterroles
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource clusterroles.rbac.authorization.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=rbac.authorization.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=clusterroles
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=storage.k8s.io/v1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=storage.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=csinodes
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=storage.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=csinodes
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource csinodes.storage.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=storage.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=csinodes
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=storage.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=csidrivers
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=storage.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=csidrivers
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource csidrivers.storage.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=storage.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=csidrivers
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=storage.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=csistoragecapacities
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=storage.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=csistoragecapacities
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource csistoragecapacities.storage.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=storage.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=csistoragecapacities
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=storage.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=volumeattachments
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=storage.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=volumeattachments
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource volumeattachments.storage.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=storage.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=volumeattachments
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=storage.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=storageclasses
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=storage.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=storageclasses
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource storageclasses.storage.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=storage.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=storageclasses
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=admissionregistration.k8s.io/v1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=admissionregistration.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=validatingwebhookconfigurations
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=admissionregistration.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=validatingwebhookconfigurations
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource validatingwebhookconfigurations.admissionregistration.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=admissionregistration.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=validatingwebhookconfigurations
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=admissionregistration.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=mutatingwebhookconfigurations
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=admissionregistration.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=mutatingwebhookconfigurations
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource mutatingwebhookconfigurations.admissionregistration.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=admissionregistration.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=mutatingwebhookconfigurations
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=admissionregistration.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=validatingadmissionpolicybindings
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=admissionregistration.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=validatingadmissionpolicybindings
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource validatingadmissionpolicybindings.admissionregistration.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=admissionregistration.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=validatingadmissionpolicybindings
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=admissionregistration.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=validatingadmissionpolicies
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=admissionregistration.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=validatingadmissionpolicies
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource validatingadmissionpolicies.admissionregistration.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=admissionregistration.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=validatingadmissionpolicies
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=apiextensions.k8s.io/v1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=apiextensions.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=customresourcedefinitions
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=apiextensions.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=customresourcedefinitions
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource customresourcedefinitions.apiextensions.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=apiextensions.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=customresourcedefinitions
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=scheduling.k8s.io/v1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=scheduling.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=priorityclasses
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=scheduling.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=priorityclasses
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource priorityclasses.scheduling.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=scheduling.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=priorityclasses
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=coordination.k8s.io/v1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=coordination.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=leases
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=coordination.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=leases
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource leases.coordination.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=coordination.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=leases
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=node.k8s.io/v1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=node.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=runtimeclasses
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=node.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=runtimeclasses
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource runtimeclasses.node.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=node.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=runtimeclasses
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=discovery.k8s.io/v1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=discovery.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=endpointslices
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=discovery.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=endpointslices
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource endpointslices.discovery.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 1 items" backup=velero/nginx-backup group=discovery.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=endpointslices
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=flowcontrol.apiserver.k8s.io/v1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=flowcontrol.apiserver.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=flowschemas
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=flowcontrol.apiserver.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=flowschemas
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource flowschemas.flowcontrol.apiserver.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=flowcontrol.apiserver.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=flowschemas
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=flowcontrol.apiserver.k8s.io/v1 logSource="pkg/backup/item_collector.go:349" resource=prioritylevelconfigurations
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=flowcontrol.apiserver.k8s.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=prioritylevelconfigurations
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource prioritylevelconfigurations.flowcontrol.apiserver.k8s.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=flowcontrol.apiserver.k8s.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=prioritylevelconfigurations
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=job.min.io/v1alpha1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=job.min.io/v1alpha1 logSource="pkg/backup/item_collector.go:349" resource=miniojobs
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=job.min.io/v1alpha1 logSource="pkg/backup/item_collector.go:522" namespace= resource=miniojobs
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource miniojobs.job.min.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=job.min.io/v1alpha1 logSource="pkg/backup/item_collector.go:558" namespace= resource=miniojobs
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=minio.min.io/v2 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=minio.min.io/v2 logSource="pkg/backup/item_collector.go:349" resource=tenants
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=minio.min.io/v2 logSource="pkg/backup/item_collector.go:522" namespace= resource=tenants
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource tenants.minio.min.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=minio.min.io/v2 logSource="pkg/backup/item_collector.go:558" namespace= resource=tenants
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=sts.min.io/v1alpha1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=sts.min.io/v1alpha1 logSource="pkg/backup/item_collector.go:349" resource=policybindings
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=sts.min.io/v1alpha1 logSource="pkg/backup/item_collector.go:522" namespace= resource=policybindings
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource policybindings.sts.min.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=sts.min.io/v1alpha1 logSource="pkg/backup/item_collector.go:558" namespace= resource=policybindings
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:349" resource=backupstoragelocations
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=backupstoragelocations
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource backupstoragelocations.velero.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=backupstoragelocations
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:349" resource=serverstatusrequests
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=serverstatusrequests
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource serverstatusrequests.velero.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=serverstatusrequests
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:349" resource=restores
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=restores
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource restores.velero.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=restores
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:349" resource=downloadrequests
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=downloadrequests
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource downloadrequests.velero.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=downloadrequests
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:349" resource=volumesnapshotlocations
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=volumesnapshotlocations
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource volumesnapshotlocations.velero.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=volumesnapshotlocations
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:349" resource=deletebackuprequests
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=deletebackuprequests
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource deletebackuprequests.velero.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=deletebackuprequests
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:349" resource=backups
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=backups
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource backups.velero.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=backups
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:349" resource=podvolumerestores
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=podvolumerestores
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource podvolumerestores.velero.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=podvolumerestores
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:349" resource=podvolumebackups
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=podvolumebackups
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource podvolumebackups.velero.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=podvolumebackups
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:349" resource=backuprepositories
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=backuprepositories
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource backuprepositories.velero.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=backuprepositories
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:349" resource=schedules
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:522" namespace= resource=schedules
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource schedules.velero.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=velero.io/v1 logSource="pkg/backup/item_collector.go:558" namespace= resource=schedules
time="2024-12-22T19:29:15Z" level=info msg="Getting items for group" backup=velero/nginx-backup group=velero.io/v2alpha1 logSource="pkg/backup/item_collector.go:242"
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=velero.io/v2alpha1 logSource="pkg/backup/item_collector.go:349" resource=datauploads
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=velero.io/v2alpha1 logSource="pkg/backup/item_collector.go:522" namespace= resource=datauploads
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource datauploads.velero.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=velero.io/v2alpha1 logSource="pkg/backup/item_collector.go:558" namespace= resource=datauploads
time="2024-12-22T19:29:15Z" level=info msg="Getting items for resource" backup=velero/nginx-backup group=velero.io/v2alpha1 logSource="pkg/backup/item_collector.go:349" resource=datadownloads
time="2024-12-22T19:29:15Z" level=info msg="Listing items" backup=velero/nginx-backup group=velero.io/v2alpha1 logSource="pkg/backup/item_collector.go:522" namespace= resource=datadownloads
time="2024-12-22T19:29:15Z" level=info msg="list for groupResource datadownloads.velero.io was not paginated" backup=velero/nginx-backup logSource="pkg/backup/item_collector.go:680"
time="2024-12-22T19:29:15Z" level=info msg="Retrieved 0 items" backup=velero/nginx-backup group=velero.io/v2alpha1 logSource="pkg/backup/item_collector.go:558" namespace= resource=datadownloads
time="2024-12-22T19:29:15Z" level=info msg="Collected 12 items matching the backup spec from the Kubernetes API (actual number of items backed up may be more or less depending on velero.io/exclude-from-backup annotation, plugins returning additional related items to back up, etc.)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:327" progress=
time="2024-12-22T19:29:15Z" level=info msg="Processing item" backup=velero/nginx-backup logSource="pkg/backup/backup.go:439" name=nginx-676b6c5bbc-gjqh2 namespace=default progress= resource=pods
time="2024-12-22T19:29:15Z" level=info msg="adding pods default/nginx-676b6c5bbc-gjqh2 to ItemBlock" backup=velero/nginx-backup logSource="pkg/backup/itemblock.go:63"
time="2024-12-22T19:29:15Z" level=info msg="Executing ItemBlock action" backup=velero/nginx-backup logSource="pkg/backup/backup.go:568"
time="2024-12-22T19:29:15Z" level=info msg="Executing pod ItemBlockAction" backup=velero/nginx-backup cmd=/velero logSource="pkg/itemblock/actions/pod_action.go:51" pluginName=velero
time="2024-12-22T19:29:15Z" level=info msg="Done executing pod ItemBlockAction" backup=velero/nginx-backup cmd=/velero logSource="pkg/itemblock/actions/pod_action.go:58" pluginName=velero
time="2024-12-22T19:29:15Z" level=info msg="Backing Up Item Block including pods default/nginx-676b6c5bbc-gjqh2 (1 items in block)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:476"
time="2024-12-22T19:29:15Z" level=info msg="Backing up item" backup=velero/nginx-backup logSource="pkg/backup/item_backupper.go:184" name=nginx-676b6c5bbc-gjqh2 namespace=default resource=pods
time="2024-12-22T19:29:15Z" level=info msg="Executing custom action" backup=velero/nginx-backup logSource="pkg/backup/item_backupper.go:357" name=nginx-676b6c5bbc-gjqh2 namespace=default resource=pods
time="2024-12-22T19:29:15Z" level=info msg="Executing podAction" backup=velero/nginx-backup cmd=/velero logSource="pkg/backup/actions/pod_action.go:51" pluginName=velero
time="2024-12-22T19:29:15Z" level=info msg="Done executing podAction" backup=velero/nginx-backup cmd=/velero logSource="pkg/backup/actions/pod_action.go:58" pluginName=velero
time="2024-12-22T19:29:15Z" level=info msg="Backed up 1 items out of an estimated total of 12 (estimate will change throughout the backup)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:499" name=nginx-676b6c5bbc-gjqh2 namespace=default progress= resource=pods
time="2024-12-22T19:29:15Z" level=info msg="Processing item" backup=velero/nginx-backup logSource="pkg/backup/backup.go:439" name=nginx-deployment-79b46bdcb5-2h8xx namespace=nginx-example progress= resource=pods
time="2024-12-22T19:29:15Z" level=info msg="adding pods nginx-example/nginx-deployment-79b46bdcb5-2h8xx to ItemBlock" backup=velero/nginx-backup logSource="pkg/backup/itemblock.go:63"
time="2024-12-22T19:29:15Z" level=info msg="Executing ItemBlock action" backup=velero/nginx-backup logSource="pkg/backup/backup.go:568"
time="2024-12-22T19:29:15Z" level=info msg="Executing pod ItemBlockAction" backup=velero/nginx-backup cmd=/velero logSource="pkg/itemblock/actions/pod_action.go:51" pluginName=velero
time="2024-12-22T19:29:15Z" level=info msg="Done executing pod ItemBlockAction" backup=velero/nginx-backup cmd=/velero logSource="pkg/itemblock/actions/pod_action.go:58" pluginName=velero
time="2024-12-22T19:29:15Z" level=info msg="Backing Up Item Block including pods nginx-example/nginx-deployment-79b46bdcb5-2h8xx (1 items in block)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:476"
time="2024-12-22T19:29:15Z" level=info msg="Backing up item" backup=velero/nginx-backup logSource="pkg/backup/item_backupper.go:184" name=nginx-deployment-79b46bdcb5-2h8xx namespace=nginx-example resource=pods
time="2024-12-22T19:29:15Z" level=info msg="Executing custom action" backup=velero/nginx-backup logSource="pkg/backup/item_backupper.go:357" name=nginx-deployment-79b46bdcb5-2h8xx namespace=nginx-example resource=pods
time="2024-12-22T19:29:15Z" level=info msg="Executing podAction" backup=velero/nginx-backup cmd=/velero logSource="pkg/backup/actions/pod_action.go:51" pluginName=velero
time="2024-12-22T19:29:15Z" level=info msg="Done executing podAction" backup=velero/nginx-backup cmd=/velero logSource="pkg/backup/actions/pod_action.go:58" pluginName=velero
time="2024-12-22T19:29:15Z" level=info msg="Backed up 2 items out of an estimated total of 12 (estimate will change throughout the backup)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:499" name=nginx-deployment-79b46bdcb5-2h8xx namespace=nginx-example progress= resource=pods
time="2024-12-22T19:29:15Z" level=info msg="Processing item" backup=velero/nginx-backup logSource="pkg/backup/backup.go:439" name=nginx-deployment-79b46bdcb5-ffl4g namespace=nginx-example progress= resource=pods
time="2024-12-22T19:29:15Z" level=info msg="adding pods nginx-example/nginx-deployment-79b46bdcb5-ffl4g to ItemBlock" backup=velero/nginx-backup logSource="pkg/backup/itemblock.go:63"
time="2024-12-22T19:29:15Z" level=info msg="Executing ItemBlock action" backup=velero/nginx-backup logSource="pkg/backup/backup.go:568"
time="2024-12-22T19:29:15Z" level=info msg="Backing Up Item Block including pods nginx-example/nginx-deployment-79b46bdcb5-ffl4g (1 items in block)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:476"
time="2024-12-22T19:29:15Z" level=info msg="Backing up item" backup=velero/nginx-backup logSource="pkg/backup/item_backupper.go:184" name=nginx-deployment-79b46bdcb5-ffl4g namespace=nginx-example resource=pods
time="2024-12-22T19:29:15Z" level=info msg="Executing custom action" backup=velero/nginx-backup logSource="pkg/backup/item_backupper.go:357" name=nginx-deployment-79b46bdcb5-ffl4g namespace=nginx-example resource=pods
time="2024-12-22T19:29:15Z" level=info msg="Executing pod ItemBlockAction" backup=velero/nginx-backup cmd=/velero logSource="pkg/itemblock/actions/pod_action.go:51" pluginName=velero
time="2024-12-22T19:29:15Z" level=info msg="Done executing pod ItemBlockAction" backup=velero/nginx-backup cmd=/velero logSource="pkg/itemblock/actions/pod_action.go:58" pluginName=velero
time="2024-12-22T19:29:15Z" level=info msg="Executing podAction" backup=velero/nginx-backup cmd=/velero logSource="pkg/backup/actions/pod_action.go:51" pluginName=velero
time="2024-12-22T19:29:15Z" level=info msg="Done executing podAction" backup=velero/nginx-backup cmd=/velero logSource="pkg/backup/actions/pod_action.go:58" pluginName=velero
time="2024-12-22T19:29:15Z" level=info msg="Backed up 3 items out of an estimated total of 12 (estimate will change throughout the backup)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:499" name=nginx-deployment-79b46bdcb5-ffl4g namespace=nginx-example progress= resource=pods
time="2024-12-22T19:29:15Z" level=info msg="Processing item" backup=velero/nginx-backup logSource="pkg/backup/backup.go:439" name=default namespace= progress= resource=namespaces
time="2024-12-22T19:29:15Z" level=info msg="adding namespaces /default to ItemBlock" backup=velero/nginx-backup logSource="pkg/backup/itemblock.go:63"
time="2024-12-22T19:29:15Z" level=info msg="Backing Up Item Block including namespaces /default (1 items in block)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:476"
time="2024-12-22T19:29:15Z" level=info msg="Backing up item" backup=velero/nginx-backup logSource="pkg/backup/item_backupper.go:184" name=default namespace= resource=namespaces
time="2024-12-22T19:29:15Z" level=info msg="Backed up 4 items out of an estimated total of 12 (estimate will change throughout the backup)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:499" name=default namespace= progress= resource=namespaces
time="2024-12-22T19:29:15Z" level=info msg="Processing item" backup=velero/nginx-backup logSource="pkg/backup/backup.go:439" name=nginx-example namespace= progress= resource=namespaces
time="2024-12-22T19:29:15Z" level=info msg="adding namespaces /nginx-example to ItemBlock" backup=velero/nginx-backup logSource="pkg/backup/itemblock.go:63"
time="2024-12-22T19:29:15Z" level=info msg="Backing Up Item Block including namespaces /nginx-example (1 items in block)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:476"
time="2024-12-22T19:29:15Z" level=info msg="Backing up item" backup=velero/nginx-backup logSource="pkg/backup/item_backupper.go:184" name=nginx-example namespace= resource=namespaces
time="2024-12-22T19:29:15Z" level=info msg="Backed up 5 items out of an estimated total of 12 (estimate will change throughout the backup)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:499" name=nginx-example namespace= progress= resource=namespaces
time="2024-12-22T19:29:15Z" level=info msg="Processing item" backup=velero/nginx-backup logSource="pkg/backup/backup.go:439" name=my-nginx namespace=nginx-example progress= resource=endpoints
time="2024-12-22T19:29:15Z" level=info msg="adding endpoints nginx-example/my-nginx to ItemBlock" backup=velero/nginx-backup logSource="pkg/backup/itemblock.go:63"
time="2024-12-22T19:29:15Z" level=info msg="Backing Up Item Block including endpoints nginx-example/my-nginx (1 items in block)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:476"
time="2024-12-22T19:29:15Z" level=info msg="Backing up item" backup=velero/nginx-backup logSource="pkg/backup/item_backupper.go:184" name=my-nginx namespace=nginx-example resource=endpoints
time="2024-12-22T19:29:15Z" level=info msg="Backed up 6 items out of an estimated total of 12 (estimate will change throughout the backup)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:499" name=my-nginx namespace=nginx-example progress= resource=endpoints
time="2024-12-22T19:29:15Z" level=info msg="Processing item" backup=velero/nginx-backup logSource="pkg/backup/backup.go:439" name=my-nginx namespace=nginx-example progress= resource=services
time="2024-12-22T19:29:15Z" level=info msg="adding services nginx-example/my-nginx to ItemBlock" backup=velero/nginx-backup logSource="pkg/backup/itemblock.go:63"
time="2024-12-22T19:29:15Z" level=info msg="Backing Up Item Block including services nginx-example/my-nginx (1 items in block)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:476"
time="2024-12-22T19:29:15Z" level=info msg="Backing up item" backup=velero/nginx-backup logSource="pkg/backup/item_backupper.go:184" name=my-nginx namespace=nginx-example resource=services
time="2024-12-22T19:29:15Z" level=info msg="Backed up 7 items out of an estimated total of 12 (estimate will change throughout the backup)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:499" name=my-nginx namespace=nginx-example progress= resource=services
time="2024-12-22T19:29:15Z" level=info msg="Processing item" backup=velero/nginx-backup logSource="pkg/backup/backup.go:439" name=nginx namespace=default progress= resource=deployments.apps
time="2024-12-22T19:29:15Z" level=info msg="adding deployments.apps default/nginx to ItemBlock" backup=velero/nginx-backup logSource="pkg/backup/itemblock.go:63"
time="2024-12-22T19:29:15Z" level=info msg="Backing Up Item Block including deployments.apps default/nginx (1 items in block)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:476"
time="2024-12-22T19:29:15Z" level=info msg="Backing up item" backup=velero/nginx-backup logSource="pkg/backup/item_backupper.go:184" name=nginx namespace=default resource=deployments.apps
time="2024-12-22T19:29:15Z" level=info msg="Backed up 8 items out of an estimated total of 12 (estimate will change throughout the backup)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:499" name=nginx namespace=default progress= resource=deployments.apps
time="2024-12-22T19:29:15Z" level=info msg="Processing item" backup=velero/nginx-backup logSource="pkg/backup/backup.go:439" name=nginx-deployment namespace=nginx-example progress= resource=deployments.apps
time="2024-12-22T19:29:15Z" level=info msg="adding deployments.apps nginx-example/nginx-deployment to ItemBlock" backup=velero/nginx-backup logSource="pkg/backup/itemblock.go:63"
time="2024-12-22T19:29:15Z" level=info msg="Backing Up Item Block including deployments.apps nginx-example/nginx-deployment (1 items in block)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:476"
time="2024-12-22T19:29:15Z" level=info msg="Backing up item" backup=velero/nginx-backup logSource="pkg/backup/item_backupper.go:184" name=nginx-deployment namespace=nginx-example resource=deployments.apps
time="2024-12-22T19:29:15Z" level=info msg="Backed up 9 items out of an estimated total of 12 (estimate will change throughout the backup)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:499" name=nginx-deployment namespace=nginx-example progress= resource=deployments.apps
time="2024-12-22T19:29:15Z" level=info msg="Processing item" backup=velero/nginx-backup logSource="pkg/backup/backup.go:439" name=nginx-676b6c5bbc namespace=default progress= resource=replicasets.apps
time="2024-12-22T19:29:15Z" level=info msg="adding replicasets.apps default/nginx-676b6c5bbc to ItemBlock" backup=velero/nginx-backup logSource="pkg/backup/itemblock.go:63"
time="2024-12-22T19:29:15Z" level=info msg="Backing Up Item Block including replicasets.apps default/nginx-676b6c5bbc (1 items in block)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:476"
time="2024-12-22T19:29:15Z" level=info msg="Backing up item" backup=velero/nginx-backup logSource="pkg/backup/item_backupper.go:184" name=nginx-676b6c5bbc namespace=default resource=replicasets.apps
time="2024-12-22T19:29:15Z" level=info msg="Backed up 10 items out of an estimated total of 12 (estimate will change throughout the backup)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:499" name=nginx-676b6c5bbc namespace=default progress= resource=replicasets.apps
time="2024-12-22T19:29:15Z" level=info msg="Processing item" backup=velero/nginx-backup logSource="pkg/backup/backup.go:439" name=nginx-deployment-79b46bdcb5 namespace=nginx-example progress= resource=replicasets.apps
time="2024-12-22T19:29:15Z" level=info msg="adding replicasets.apps nginx-example/nginx-deployment-79b46bdcb5 to ItemBlock" backup=velero/nginx-backup logSource="pkg/backup/itemblock.go:63"
time="2024-12-22T19:29:15Z" level=info msg="Backing Up Item Block including replicasets.apps nginx-example/nginx-deployment-79b46bdcb5 (1 items in block)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:476"
time="2024-12-22T19:29:15Z" level=info msg="Backing up item" backup=velero/nginx-backup logSource="pkg/backup/item_backupper.go:184" name=nginx-deployment-79b46bdcb5 namespace=nginx-example resource=replicasets.apps
time="2024-12-22T19:29:15Z" level=info msg="Backed up 11 items out of an estimated total of 12 (estimate will change throughout the backup)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:499" name=nginx-deployment-79b46bdcb5 namespace=nginx-example progress= resource=replicasets.apps
time="2024-12-22T19:29:15Z" level=info msg="Processing item" backup=velero/nginx-backup logSource="pkg/backup/backup.go:439" name=my-nginx-h2rwx namespace=nginx-example progress= resource=endpointslices.discovery.k8s.io
time="2024-12-22T19:29:15Z" level=info msg="adding endpointslices.discovery.k8s.io nginx-example/my-nginx-h2rwx to ItemBlock" backup=velero/nginx-backup logSource="pkg/backup/itemblock.go:63"
time="2024-12-22T19:29:15Z" level=info msg="Backing Up Item Block including endpointslices.discovery.k8s.io nginx-example/my-nginx-h2rwx (1 items in block)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:476"
time="2024-12-22T19:29:15Z" level=info msg="Backing up item" backup=velero/nginx-backup logSource="pkg/backup/item_backupper.go:184" name=my-nginx-h2rwx namespace=nginx-example resource=endpointslices.discovery.k8s.io
time="2024-12-22T19:29:15Z" level=info msg="Backed up 12 items out of an estimated total of 12 (estimate will change throughout the backup)" backup=velero/nginx-backup logSource="pkg/backup/backup.go:499" name=my-nginx-h2rwx namespace=nginx-example progress= resource=endpointslices.discovery.k8s.io
time="2024-12-22T19:29:15Z" level=info msg="Summary for skipped PVs: []" backup=velero/nginx-backup logSource="pkg/backup/backup.go:542"
time="2024-12-22T19:29:15Z" level=info msg="Backed up a total of 12 items" backup=velero/nginx-backup logSource="pkg/backup/backup.go:546" progress=
time="2024-12-22T19:29:15Z" level=info msg="Setting up backup store to persist the backup" backup=velero/nginx-backup logSource="pkg/controller/backup_controller.go:731"
time="2024-12-22T19:29:15Z" level=info msg="Initial backup processing complete, moving to Finalizing" backup=velero/nginx-backup logSource="pkg/controller/backup_controller.go:745"
time="2024-12-22T19:29:15Z" level=info msg="plugin process exited" backup=velero/nginx-backup cmd=/velero id=87 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/velero
time="2024-12-22T19:29:15Z" level=info msg="plugin process exited" backup=velero/nginx-backup cmd=/plugins/velero-plugin-for-aws id=97 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/plugins/velero-plugin-for-aws
time="2024-12-22T19:29:15Z" level=info msg="Updating backup's status" backuprequest=velero/nginx-backup controller=backup logSource="pkg/controller/backup_controller.go:310"
time="2024-12-22T19:29:15Z" level=info msg="plugin process exited" backup=velero/nginx-backup cmd=/plugins/velero-plugin-for-aws controller=backup-finalizer id=109 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/plugins/velero-plugin-for-aws
time="2024-12-22T19:29:32Z" level=info msg="plugin process exited" cmd=/plugins/velero-plugin-for-aws controller=download-request downloadRequest=velero/nginx-backup-ceced742-0c92-465c-84ef-8ae4579956fe id=120 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/plugins/velero-plugin-for-aws
time="2024-12-22T19:30:09Z" level=info msg="Validating BackupStorageLocation" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:142"
time="2024-12-22T19:30:09Z" level=info msg="BackupStorageLocations is valid, marking as available" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:127"
time="2024-12-22T19:30:09Z" level=info msg="plugin process exited" backupLocation=velero/default cmd=/plugins/velero-plugin-for-aws controller=backup-sync id=131 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/plugins/velero-plugin-for-aws
time="2024-12-22T19:30:09Z" level=info msg="plugin process exited" backup-storage-location=velero/default cmd=/plugins/velero-plugin-for-aws controller=backup-storage-location id=136 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/plugins/velero-plugin-for-aws
time="2024-12-22T19:31:09Z" level=info msg="Validating BackupStorageLocation" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:142"
time="2024-12-22T19:31:09Z" level=info msg="BackupStorageLocations is valid, marking as available" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:127"
time="2024-12-22T19:31:09Z" level=info msg="plugin process exited" backupLocation=velero/default cmd=/plugins/velero-plugin-for-aws controller=backup-sync id=150 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/plugins/velero-plugin-for-aws
time="2024-12-22T19:31:09Z" level=info msg="plugin process exited" backup-storage-location=velero/default cmd=/plugins/velero-plugin-for-aws controller=backup-storage-location id=157 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/plugins/velero-plugin-for-aws
time="2024-12-22T19:32:09Z" level=info msg="Validating BackupStorageLocation" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:142"
time="2024-12-22T19:32:09Z" level=info msg="BackupStorageLocations is valid, marking as available" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:127"
time="2024-12-22T19:32:09Z" level=info msg="plugin process exited" backup-storage-location=velero/default cmd=/plugins/velero-plugin-for-aws controller=backup-storage-location id=176 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/plugins/velero-plugin-for-aws
time="2024-12-22T19:32:09Z" level=info msg="plugin process exited" backupLocation=velero/default cmd=/plugins/velero-plugin-for-aws controller=backup-sync id=169 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/plugins/velero-plugin-for-aws
time="2024-12-22T19:33:09Z" level=info msg="plugin process exited" backupLocation=velero/default cmd=/plugins/velero-plugin-for-aws controller=backup-sync id=189 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/plugins/velero-plugin-for-aws
time="2024-12-22T19:33:09Z" level=info msg="Validating BackupStorageLocation" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:142"
time="2024-12-22T19:33:09Z" level=info msg="BackupStorageLocations is valid, marking as available" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:127"
time="2024-12-22T19:33:09Z" level=info msg="plugin process exited" backup-storage-location=velero/default cmd=/plugins/velero-plugin-for-aws controller=backup-storage-location id=199 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/plugins/velero-plugin-for-aws
time="2024-12-22T19:34:09Z" level=info msg="Validating BackupStorageLocation" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:142"
time="2024-12-22T19:34:09Z" level=info msg="BackupStorageLocations is valid, marking as available" backup-storage-location=velero/default controller=backup-storage-location logSource="pkg/controller/backup_storage_location_controller.go:127"
time="2024-12-22T19:34:09Z" level=info msg="plugin process exited" backupLocation=velero/default cmd=/plugins/velero-plugin-for-aws controller=backup-sync id=210 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/plugins/velero-plugin-for-aws
time="2024-12-22T19:34:09Z" level=info msg="plugin process exited" backup-storage-location=velero/default cmd=/plugins/velero-plugin-for-aws controller=backup-storage-location id=217 logSource="pkg/plugin/clientmgmt/process/logrus_adapter.go:80" plugin=/plugins/velero-plugin-for-aws
```

uninstall velero:

```
$ velero uninstall
You are about to uninstall Velero.
Are you sure you want to continue (Y/N)? Y
Waiting for resource with attached finalizer to be deleted

Waiting for velero namespace "velero" to be deleted
............................................................
Velero namespace "velero" deleted
Velero uninstalled ⛵
```


https://github.com/vmware-tanzu/velero-plugin-for-aws#compatibility