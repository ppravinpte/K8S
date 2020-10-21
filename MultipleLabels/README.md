# Added multiple labels in pod. Use labels to connect service with pods as per labels match of service

1) Created Pod with two pod definitions in file "webapp-pd.yml".
   - First pod referes to release:0 version of image. Two labels are added. Additional label release to show version.
     labels:
        appl: webappl
        release: '0'   
   - Second pod referes to release:0-5 version of image.
     labels:
        appl: webappl
        release: '0-5'    
2) Created service with file "webapp-svc.yaml" to have first 0 release of the image with following labels.
    selector:
      appl: webappl
      release: '0'
   For this service, it uses first pod with matching label of release: '0'.
   Get service details with describe command.  
   $ kubectl describe svc fleetman-webappsvc
   o/p:
    Name:                     fleetman-webappsvc
    ...
    Selector:                 appl=webappl,release=0      --> conveys Selector of service.
    Type:                     NodePort
    IP:                       <number1> 
    Port:                     http  80/TCP
    TargetPort:               80/TCP
    NodePort:                 http  30086/TCP
    Endpoints:                <number2>:80
    Session Affinity:         None
    External Traffic Policy:  Cluster
    Events:                   <none>

3) Changed the release from '0' to '0-5' within "webapp-svc.yaml" file of service.  
   For this changed release version in service, it uses second pod with matching label of release: '0-5'.

4) Type: Nodeport is used in service to access web-browser. nodePort number > 30000 used to test it locally.
- Open browser and type on url - http://Minikubeip:nodeportnumber
