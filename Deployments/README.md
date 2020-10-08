# This example is of Kubernetes Deployment.
"""
Deployment is an entity that manages replicasets and replicasets creates corresponding pods.
- Tried changing version manually from release0 to 0-5 in image of container section within pod.yaml file to perform auto rolling updates with zero downtime.
- Tried with incorrect version name in image to witness how previous pod replicas of 0-5 still continue to runs and keeps the site alive where as current image status changes to Errimgpull and eventually, imagepullBackoff.
- After correcting image name in pod.yaml, previous pod name was deleted but replicaset still keep version of the corrupted image in replicaset history.
"""