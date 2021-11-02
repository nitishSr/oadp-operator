<hr style="height:1px;border:none;color:#333;">
<h1 align="center">Usage of Custom Plugin Images for Velero</h1>
<hr style="height:1px;border:none;color:#333;">

The OADP Operator supports custom plugin images under the `unsupportedOverrides` field as detailed in the YAML below. This feature can be used to support rapid development and testing of custom images for supported plugins and provides a way for developers to quickly deploy and test their changes.

Details for supported plugins and thier usage is given below, and please use the respective keys for the plugins. All keys must be entered in the Velero CR under a new field called as `unsupportedOverrides`, and with the key below for reference and corresponding image tag as their value.


 - Velero Imagekey  -> `veleroPluginImageFqin`
 - AWS Plugin ImageKey  -> `awsPluginImageFqin`
 - OpenShift Plugin ImageKey  -> `openshiftPluginImageFqin`
 - Azure Plugin ImageKey -> `azurePluginImageFqin`
 - GCP Plugin ImageKey  -> `gcpPluginImageFqin`
 - CSI Plugin ImageKey  -> `csiPluginImageFqin`
 - Restic Restore ImageKey -> `resticRestoreImageFqin`

Below is an example Velero CR with the unsupportedOverrides key added for reference. Please note that the `<IMAGE_PLACEHOLDER WITH TAG>` is to be replaced with the plugin image and tag.

```
apiVersion: oadp.openshift.io/v1alpha1
kind: Velero
metadata:
  name: velero-sample
spec:
  defaultVeleroPlugins:
  - aws
  backupStorageLocations:
  - name: default
    provider: aws
    default: true
    objectStorage:
      bucket: my-bucket
      prefix: my-prefix
    config:
      region: us-east-1
      profile: "default"
    credential:
      name: cloud-credentials
      key: cloud
  volumeSnapshotLocations:
  - name: default
    provider: aws
    config:
      region: us-west-2
      profile: "default"
  unsupportedOverrides:
    awsPluginImageFqin: <IMAGE_PLACEHOLDER WITH TAG>
    openshiftPluginImageFqin: <IMAGE_PLACEHOLDER WITH TAG>
```