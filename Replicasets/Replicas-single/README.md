# Replicaset created to run single instance of pod.
1) Created Replicaset to include the template of pod definition.
   - Pod definition has a Label "application: webappln".  This must be equal to Replicaset spec->selector->matchLabels
2) Created service to provide port number for outside access. It needs same Labels underneath of selectors as of pod to connect to that pod.
3) If pod gets deleted accidently, replicaset will immediately create a new pod to retain web browser access. However, still there must be a downtime of 1-2 second. 
To overcome this, it's best practie to have 2 replicas at least.

Possible errors encountered:
(1) kind: Replicaset
If s is not caps then error: needs, kind: ReplicaSet 
error: unable to recognize "runpods.yaml": no matches for kind "Replicaset" in version "apps/v1".

(2)if template is not properly indented then error
error: error validating "runpods.yaml": error validating data: ValidationError(ReplicaSet): unknown field "template" in io.k8s.api.apps.v1.ReplicaSet; if you choose to ignore these errors, turn validation off with --validate=false
Need proper indentation
spec:
...
  template:

(3) if tries to mismatch the labels of pod defination and replicaset in runpods.yaml file then it errored.
The ReplicaSet ""<name of replicaset-name>"is invalid:
* spec.template.metadata.labels: Invalid value: map[string]string{"application":"<name of labels>"}: `selector` does not match template `labels`
* spec.selector: Invalid value: v1.LabelSelector{MatchLabels:map[string]string{"application":"<name of labels>"}, MatchExpressions:[]v1.LabelSelectorRequirement(nil)}: field is immutable.
