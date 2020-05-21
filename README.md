# DEVOPS ASSEMBLY LINES(2020)
## TASK 2
### INTEGRATING JENKINS WITH KUBERNETES
REQUIREMENT:Network Connectivity
* Firstly change the VirtualBox->RHEL8->Network Setting.Enable 2 adapters,adapter 1 will be set to NAT and adapter 2 will be set to Host-Only Network.
* Start RHEL8.Make sure RHEL8 is accessing both the Adapters and connected,by checking the ip using "ifconfig" command.

In RHEL8-
* Make sure there are no pods,deployments or any other resource running.
![](JenkinswithKubernetes/1.PNG)

* Install Kubernetes on RHEL8
![](JenkinswithKubernetes/2.PNG)

* Copy the command and paste onto Terminal
![](JenkinswithKubernetes/3.PNG)
![](JenkinswithKubernetes/4.PNG)

* Make kubectl binary executable and move the kubectl file to /usr/bin folder.
![](JenkinswithKubernetes/5.PNG)

* Get the IP of minikube
![](JenkinswithKubernetes/6.PNG)

***[Here the port number is 8843,therefore the IP becomes http://192.168.99.100:8443]***

* Now in order to create the config file to run kubectl commands we need three files-client.key,client.crt & ca.crt which will be available at following paths-
![](JenkinswithKubernetes/7.PNG)
![](JenkinswithKubernetes/8.PNG)

* Use WinSCP to transfer these files from Windows to RHEL8
![](JenkinswithKubernetes/9.PNG)
![](JenkinswithKubernetes/10.PNG)
![](JenkinswithKubernetes/11.PNG)

* Now run the following command on Terminal in RHEL8
![](JenkinswithKubernetes/12.PNG)

***Now using this command we can create ,run, delete pods/deployements etc ,resources on RHEL8 Kubernetes which will remain in sync with the Kubernetes on your system ,in mycase its Windows 10.***

![](JenkinswithKubernetes/13.PNG)
![](JenkinswithKubernetes/14.PNG)

* Now create the myinfo.yml file which will contain path of the files we copied using WinSCP.It will contain the following code.
![](JenkinswithKubernetes/15.PNG)

Save it.Now we can run kubectl commands easily:
kubectl get pods --kubeconfig myinfo

We can make it simpler by copying the myinfo.yml file to .kube folder with name config .Here are the steps-
![](JenkinswithKubernetes/16.PNG)
```
kubectl config view - This command will show the contents of config file.
```
![](JenkinswithKubernetes/17.PNG)
 * Now login into Jenkins.Create first job(here jk1).It will be FreeStyleProject.
 ![](JenkinswithKubernetes/18.PNG)
 ![](JenkinswithKubernetes/19.PNG) 
 
 * Put the GitHub Repository URL,this URL has to contain the following rs1.yml file and must be initialised as well.
 ![](JenkinswithKubernetes/20.PNG)
 ![](JenkinswithKubernetes/28.PNG)
 
 * Execute Shell will contain the following code.
 ![](JenkinswithKubernetes/21.PNG)
 This command will build successfully on first build but on second build it will fail because the pods and ReplicaSet will already be running with the same name.
 ![](JenkinswithKubernetes/22.PNG)
 
 * Therefore update the Execute shell,by putting if and else commands.Here i have also exposed the RS so that i can the HTML page on browser on any system.
 ![](JenkinswithKubernetes/23.PNG)
 
 Thats it!!
 
 Now use curl command to run the RS on Windows
 ![](JenkinswithKubernetes/25.PNG)
 
 The same command will run on RHEL8(use the IP of minikube and port number of RS exposed)
 ![](JenkinswithKubernetes/26.PNG)
 
 ![](JenkinswithKubernetes/27.PNG)
 
 I hope it was helpful.Thankyou!
