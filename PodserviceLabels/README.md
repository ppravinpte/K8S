# Pods and Service are connects through Labels.
- Pods can't be accessed outside of Kubernetes cluster. It neerequires connection with service having port access to browser.
- Add Label to the Pods and Selector to service with matching key:value pairs.  
  Service look for any key:value matching pairs in all available pods and where it finds it, connect with that pod. 
- Type: Nodeport is used in service to access web-browser. nodePort number > 30000 used to test it locally.
- Open browser and type on url - <Minikubeip>:<nodePort-Number>