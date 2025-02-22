# Can Helm upgrade can restart the pods?

ONLY if the upgrade results in changes to the Kubernetes resources managed by the Helm chart. 

When you run helm upgrade, Helm compares the new chart's configuration with the existing release to identify any changes.

### Updating Resources:

If changes are detected in the Kubernetes resources (e.g., ConfigMap, Secret, Deployment, StatefulSet, DaemonSet, etc.), Helm updates those resources.

For example:
Changes to a ConfigMap or Secret referenced by a pod won't restart the pod automatically, but you can configure your Deployment to include checksums of these resources as annotations. 
Changes to the annotation will trigger a pod restart.

Changes to a Deployment (e.g., the container image, environment variables, or resource requests/limits) will trigger a rolling update of the pods managed by the Deployment.

### Restart Mechanism:

For resources like Deployments and StatefulSets, Kubernetes performs a rolling update, which replaces pods one by one to ensure minimal downtime.
Key Scenarios
Configuration Changes: If values.yaml or chart templates change in a way that affects the pod spec (e.g., image version or environment variables), pods will restart.
No Changes Detected: If there are no changes to the Kubernetes resources, pods will not restart.
Forcing a Restart
If you want to force a pod restart without changing configurations, you can update a resource's annotation or label manually or include a dummy change in your values.yaml file to trigger a redeployment. For example:

``` helm upgrade my-release my-chart --set someDummyValue=$(date +%s)```

This works because the timestamp value forces a change in the Helm release, causing affected resources to be updated and pods to restart.

### Dynamic Overrides:

The --set flag in Helm allows you to override or introduce new values temporarily for the upgrade. If someDummyValue is not defined in values.yaml, Helm will include it dynamically during the chart rendering process for that release.
Effect of Dummy Values:

Even if someDummyValue doesn’t map to anything in your chart templates, its inclusion changes the Helm release checksum. This, in turn, triggers a redeployment because Kubernetes sees the release as "modified."
If you want to use it in templates:

If someDummyValue needs to be used in your chart templates (e.g., in an annotation to trigger a pod restart), you must reference it in your chart. For example:
``` yaml
metadata:
  annotations:
    restartTimestamp: "{{ .Values.someDummyValue }}"
```

No Need for Permanent Addition:

If your only goal is to trigger a redeployment, you don't need to modify values.yaml permanently. The --set flag is sufficient for one-time use.

Example Command
 

``` bash
helm upgrade my-release my-chart --set someDummyValue=$(date +%s)
```
This ensures that a change is detected in the Helm release, even if someDummyValue is not defined in values.yaml, triggering a pod restart.
