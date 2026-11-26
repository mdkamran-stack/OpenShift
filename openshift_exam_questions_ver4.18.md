
=================================
Kubeadmin 
Password:  ZXUPv-bv9xC-T4wAj-ngJuM
=======================================
# while oc whoami getting EOF use this cmd lab start auth-providers 

<img width="773" height="378" alt="image" src="https://github.com/user-attachments/assets/c8bb3fb9-948c-44ea-8276-53aee2fe39d0" />   


Ram sir redhat 
---------------
ram.redhat123
jaishrikrishna@2023

# lab start declarative-manifests

# Question-1
Configure Identity Provider   
Configure Your Openshift cluster to use an HTPasswd identity provider with the Following.  
The name of the identity provider is ex280-htpasswd  
The name of the secrets: ex280-idp-secret  
The user account armstrong is present and can log in with password indionce.  
The user account collins is present and can log in with the password veraster.  
The user account aldrin is present and can log in with password roonkere  
The user account jobs is present and can log with sestiver   
The user account wozniak is present and can log in with password glegunge.  

<details>
<summary><b>Show Answer</b></summary>

**use GUI in exam**
**Solution**
### First create users htpasswd -c -b -B - openshift-passwd jobs redhat  
## htpasswd -b -B - openshift-passwd kamran redhat
htpasswd -b -B - openshift-passwd woznaik redhat

Login to GUI admin> cluster settings > configuration > Oauth > htpasswd > 
# cat openshift-passwd get the user put users into identity provider GUI then name of provider ex280-htpasswd > Add

## oc get secret -n openshift-config take the backup of latest secret > oc get secret -n openshift-config secretname  -o yaml > secret.yml  > oc apply -f secret.yml

## vi secret.yml  put your secret name > oc create -f secret.yml 
## oc get oauth/cluster -o yaml > is.yml  >  vi is.yml  update secret name 
## oc replace -f is.yml  >> oc get pod -n openshift-authentication
oc login -u username -p password 
</details>


if auth fails 
=================
echo "192.168.64.129 oauth-openshift.apps.king.flahcloud.com" >> /etc/hosts

# Question2 **use GUI in exam**
Configure cluster permissions    
configure your openshift cluster to meet the following requirements.  
The user account jobs can perform cluster administration tasks.  
The user account wozniak can create projects    
The user account wozniak cannot  perform cluster administration task 
The use account armstrong cannot  create projects  
The user account kubeadmin is not present   

<details>
<summary><b>Show Answer</b></summary>
**Login to GUI**

1> Goto user management > RoleBinding > **cluster Wide Role Binding** Name xyz > **Role Name** **cluster_admin**  > User name  
2> Goto user management > RoleBinding > **cluster Wide Role Binding** Name xab > **Role Name** **self-provisioner** > wozniak   
3> We have to remove the **self-provisioners** if self-proviosners not their it means already deleted   **from role binding under kube-system**
4 **NOTE** One we completed all questions at last we have to goto **WORKload** >> Secret >> **under name space **kube-system** delete kubeadmin**

</details>

# Question3  **use GUI in exam**

## Configure Project permissions.configure your Openshift cluster to meet the following requirements: The following projects exists.  
apollo  
manhattan  
gemini  
bluebook  
titan  
The user account armstrong is an adminstrator for project apollo and project gemini  
The user account wozniak can view project titan but not administer or delete it.    

1> Goto HOME > Projects > Create projevt like apollo gemini , bluebook, titan > Display name anything >   
2> User management > rolebinding > Crete rolebinding **namespace** >> name anything > namesapce>  project apollo &  > selectrole > admin > username armstring && same as for gemini project  
2> here we have to bind **select role view** 


# Question4   **use GUI in exam**

Configure groups
Configure your Openshift cluster to meet the following requirements.  
The user account armstrong is a member of the commander group  
The User account collins is a member of pilot group  
The user account aldrin is a member of the pilot group  
Members of the commander group have edit permission in the apollo project  
Members of the pilot group have view permission in the apollo Project.  

<details>
<summary><b>Show Answer</b></summary>

1> Under usermgmt select group create a group & name in one short 
2> role-binding  select rolebinding namespace role binding > select namespace and Rolename & goups name permission edit in second case give permission view  

</details>

# Question5   **use CLI in exam**

**Configure Quota**
Configure your openshift cluster to use quotas in the manhattan project with following reuirements.  
The name of the quota is: **ex280-quota**  
The amount of memory consumed across all conatiner may not exceed 160 Mi  
The total amount of cpu consumed across all conatiner may not exceed 2 full cores  
The maximum no .of replication controllers does not exceed 3     
The maximum no of pods does not exceed 3    
The max no of service does not exceed 6  

<details>
<summary><b>Show Answer</b></summary>  
 
oc project
oc new-project manhattan >> oc project manhattan >>  

# oc create quota ex280-quota --help   

--hard=cpu=2,memory=160Mi,pods=3,services=6,replicationcontrollers=3
</details>


# Question6

Configure a secure route  
Configure the oxcart application in the **area51** project with the following requirements:  
The application uses a secure route called **oxcart** 
Traffic between the client and the router is encrypted  
Traffic between the router and the service is unencrypted  a
The route uses a CA signed certificate with the follwoing subject fields:  
/C=US/ST=NV/L=HIKO/O=CIA/OU=UASF/CN=classiffied.apps.domain20.example.com  
The application is reachable only at the following address: https://classified.apps.ocp4.example.com  
The application produces output   

**First we have create the same env in our practice lab.**

***oc new-project area51***  

***oc create deploy oxcart --image=registry.ocp4.example.com:8443/redhattraining/hello-world-nginx:v1.0***  

***oc expose deployment oxcart --port=8080***  

**Route is software define LB in OCP three tyep 1. EDGE  2.passthrogh 3. Re-encrypt**

## To create self sign certificate
***openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:4096 -keyout private.key -out certificate.crt***  && put the given informations. like ca org .  domain name should be in exam its diff classified.apps.doman20.eample.com
## To create Routing 
## oc get service will get name of service 
## Now we have to create route
## To verify
**curl -kv https://classified.apps.ocp4.example.com**

<details>
<summary><b>Show Answer</b></summary>
 
## In Exam   
***oc new-project projectname***  
***oc get deploy***  
***oc get service***   
***oc get route***   
# In exam we will get script named newcert pass argument hello   
# now build SSL certificate from cmd of given script called newcert Then ls to veriy our .crt & .key file 
 
 ***Now we have delete the exisiting route oc delete route oxcart***
 ***Now we have create own route two way cmd or GUI**if UI goto Network Routes in specified project.
 ## Below is cmd line   
 
 ***oc create route edge --service oxcart --cert=certificate.crt --key=private.key --hostname=classified.apps.ocp4.example.com***  
  
 </details>

## In laptop
**oc create deployment oxcart  nginx-test --image=docker.io/nginxinc/nginx-unprivileged:latest** use this image for practice.  


# Question7

**Deploy an application**  
**EX280 exam prepared for Deploy the chart named **redhat-movie** in the **project ascii-movie** from the repository**   
**http://helm.domain20.example.com/chart/**   
In personal lab we have to use this  http://helm.ocp4.example.com/charts
you may use the telnet or nc commands to validate the deployment.

<details>
<summary><b>Show Answer</b></summary>
 
**oc new-project ascii-movie**  
# for practice   
**helm repo add xyz http://helm.ocp4.example.com/charts**  
**helm search repo xyz**  
**helm install redhat-movie xyz/etherpad -n ascii-movie**   
**oc get pod**   
**oc get deploy**    
**oc get route -n ascii-movie**   
**To verify using telnet or nc**   
if pod not running in local lab then edit deployment and update image  registry.ocp4.example.com:8443/etherpad/etherpad:1.8.18   

# In exam  
**we have to create project**  
**helm repo add xyz https:app.domain.com**    
**helm repolist**    
**helm search repo**      
**helm install movie chart-name**     
**oc get po**      
**oc get deploy**  
**oc get route**  

 </details>

# Question 8

**Configure a secret  # Their are 3 types of secret generic 2tls 3 docker registry**  
**Configure a secret in the math project with the following requirements:**   
**The name of the secret is: magic**   
**The secret defines a key with name: decoder_ring**    
**The secret defines the key with value: XPWPKDDCP3T**   

<details>
<summary><b>Show Answer</b></summary>
**cmd line** oc new-project math  **oc create secret generic magic --from-literal decoder_ring="aaaa"**   

Create one project by given name   
**login gui underworkload their is secret put the secret name , key and value**    

<img width="1527" height="498" alt="image" src="https://github.com/user-attachments/assets/27dfe209-a252-4860-8ae8-499cfb7c24af" />   
 </details>


# Question 9  

Configure an application to use a secret.

Configure the application called **qed** in the math project with the following requirements:

The application uses the secret previously created called: magic.

The secret defines an environment variable with the name: DECODER_RING.  

The application output should no longer display: SORRY, application is not configured correctly.  

## we are deploying dummy app for practice 
**oc create deployment qed --image=registry.ocp4.example.com:8443/redhattraining/hello-world-nginx**  
**oc get deployment**  
**oc expose deployment qed --port=8080**  
**oc expose service qed**  
**oc get route**  
## To verify we will get some result instead of sorry
**curl and hostpath**  

<details>
<summary><b>Show Answer</b></summary>
## In exam we have to map using below 

# oc set env deployment qed --from=secret/magic  
## To verify secret is mapped or not in deployment file it will show decoder_ring  
***oc edit deployment >> To check the Decoder_ring is mapped properly***  
**After that new pod will create**  
## oc get pod   

***oc get route***

***curl http://HOST/PORT***

 </details>

# Question 10 use cli

Configure a service account  
Configure a service account in the apples project to meet the following requirements.    
The name of the service account is ex280sa    
The service account allows pods to be run as any available user   

<details>
<summary><b>Show Answer</b></summary>  
 
============
***oc new-project apples***   
***oc create sa ex280sa***    
*****oc adm policy add-scc-to -user anyuid -z ex280sa*****     

 </details>

=============
# Question 11  

## Deploy an application  
## Deploy the application called oranges in the apples project so that the following condition.  
## No configuration components have been added or removed  
## The application produces output  
## The application uses the ex280sa service account   
==============
## In exam will get pod in error/crashloopback issue.  
## The End goal is we have to map service acc to deployemnt   
**for our lab practice**  
**oc new-project apple**  
## oc ge sa   
**oc create deploy orange --image=registry.ocp4.example.com:8443/redhattraining/gitlab-ce:8.4.3-ce.0**  
**oc expose deployment orange --port=80**   
**oc expose service orange**  
**oc get po**  
**oc logs orange** ***We will get permission denied**  
<img width="1098" height="301" alt="image" src="https://github.com/user-attachments/assets/32f67097-3967-416e-9c49-76e8173cca8a" />

<details>
<summary><b>Show Answer</b></summary>
 
***In exam***
## oc get po   
## oc logs of pod
## oc get sa 
## oc get route   
# oc set serviceaccount deploy orange  ex280sa  (deployment name +service acc name)  In exam we have execute this cmd 
## oc get endpoint  ***This cmd show instead of ip it show none once we map ths labels then it will show ip address in endpoint**  
# oc get pod --show-labels **service selector values to match pod labels**  
# oc edit service orange **pod labels should match service selector**  
## oc get endpoints  # we will get none it should be ip address 
# pod label should match service selector
<img width="934" height="324" alt="image" src="https://github.com/user-attachments/assets/1d078214-de3d-44c8-9d64-a1444989f397" />

<img width="976" height="646" alt="image" src="https://github.com/user-attachments/assets/433b07fa-1b28-4e82-b0fb-9257122df940" />

## oc get route will get url check in browser   
<img width="929" height="342" alt="image" src="https://github.com/user-attachments/assets/916a3676-876c-4bba-b6ce-cd3a83752c63" />

 </details>

# Question 12

Deploy an application called atlas in the mercury project so that the following condition.  
No configuration components have been added or removed   
The application produces output  
-------
## Main reason for Deployment and pod failure is its consumed more memory 
## So 80GB so node having Memory issue will not start 
## We will reduce or remove the memory portion from deployment after POD/Deployment will UP.  
## Project already Configure already   
In Lab we will create Deployment and but in exam all are created.
***oc new-project mercury***
 ***oc create deploy atlas --image=registry.ocp4.example.com:8443/redhattraining/hello-world-nginx:v1.0 --dry-run -o yaml  > deploy.yml***
 **oc create -f  deploy.yml**
 ***vi deploy.yml** They will put quota limit in file 

<img width="975" height="224" alt="image" src="https://github.com/user-attachments/assets/db1bb240-2800-4a12-8aa3-676061eaca46" />
# Pod is Pending Due resource Crunch 
# we have to go to deployment in exam 
## oc edit deployment name of deploy

## Finally we have to check the route using curl http://

# Question 13

## This question we have to perform via GUI in exam***

**Configure a network policy using the databases and checker projects with the following requirements.**  
**The database project has network policy with the name db-allow-mysql-conn based on pod selector label**    
**network.openshift.io/policy-group**   
**Connection to the databse project are restricted to deployments from the checker project The network policy is filtered by project selector using the**  
**team devsecops label and pod selector using the deploymentb-mysql label**    
**The application can establish a connection to port 3306/TCP**    
**you can check your work by examining the logs in the checker project**   

===========================
In NS we have to create a policy on pod labels match **network.openshift.io/policy-group** we have to allow lable team devsecops 

**oc create ns database  
**oc create ns checker   
Now we have to deploy app in both project for practice.   
oc create deploy mysql --image=registry.ocp4.example.com:8443/rhscl/mysql-57-rhel7:latest -n database --dry-run -o yaml > deploy.yml   

## It is already their in exam this is for practice purpose   
<img width="647" height="412" alt="image" src="https://github.com/user-attachments/assets/3ae6cfe5-3b20-4214-9c95-9d4d6ea38a53" />  

oc create -f deploy.yml  

<img width="1486" height="639" alt="image" src="https://github.com/user-attachments/assets/d65da9e5-bbcf-4e79-8795-6b1afc5f8395" />  

we will get same type of app in checker namespace   
oc create deploy wordpress --image=registry.ocp4.example.com:8443/rhscl/mysql-57-rhel7:latest -n checker --dry-run -o yaml > deploy.yml  

<img width="842" height="430" alt="image" src="https://github.com/user-attachments/assets/c4be9830-bf5c-45bd-b524-5842431e44ed" />  

#oc create -f deploy.yml -n checker   

## NS also having labels oc label ns checker team:devsceops it laready their in exam   

oc get po -n database 
oc get po -n checker 

<details>
<summary><b>Show Answer</b></summary>
# In exam checker namespace pod in crashloopbakc due to not connecting to app 

# In exam we have to perform graphical it is easy way 
# oc whoami --show-console 
# goto network >> Network policy switch project database create network policy 
**oc get pod -n database --show-labels**
## Allow pod inside the cluster 
## Add namespace selector 
Lables & selector 

## Below ss show all 3 values which we have to placed in GUI n/w policy 

<img width="1667" height="360" alt="image" src="https://github.com/user-attachments/assets/b4273dd1-b8aa-468c-bc6c-154d48b7893b" />

<img width="1041" height="489" alt="image" src="https://github.com/user-attachments/assets/e1c7fe7f-5c9c-498c-b278-58be867af5fd" />

<img width="1092" height="603" alt="image" src="https://github.com/user-attachments/assets/f9f848ba-fc63-4c74-af41-62b96060a4cc" />
# Add the port 3306 & res
<img width="685" height="165" alt="image" src="https://github.com/user-attachments/assets/38ea398f-c4e9-4277-9ff5-bbceb650d5c8" />

# Finally after delting the pod in checker namsepace it will come in running mode

 </details>

 # Question 14

 ## Configure a project template 

 ### Configure your Openshift Cluster so that new projects are created with limits using the following requirements.  

 ### The Name of the limit range is: PROJECT NAME-Limits where PROJECT NAME is the name of the project created using ac new-project The amount of memory consumed by a single container is between 160Mi and 16Mi with a default of 512Mi and default request of 256Mi.  

 for practice : > Minimum: 128Mi > Maximum: 1Gi > Default: 512Mi > Default request: 256Mi

 # Solution: to 

***oc adm create-bootstrap-project-template -o yaml > is.yml***  **In this file we have to add limit range definations**
## We have move GUI Administration >> LimitRange and copy yaml manifest and add to is.yml  

We have to make sure to remove namespace on limit 

<img width="511" height="636" alt="image" src="https://github.com/user-attachments/assets/013b5169-38ff-47cc-9d62-c952a1b4ca25" />

#Make sure from Remove namespace tab from yaml.

**oc create -f is.yml -n openshift-config**

**we can verify it** **oc get template -n openshift-config**

## Now need to tell ref Api (tell Openshift use this Project template)so we need to edit object like project.config add namespace name

**oc edit project.config.openshift.io cluster**  

<img width="611" height="473" alt="image" src="https://github.com/user-attachments/assets/19042288-8a30-411e-9153-562622501413" />


<img width="597" height="677" alt="image" src="https://github.com/user-attachments/assets/a490fab0-923f-456f-a378-0e779109f723" />console openshift




# Question 15 

## Install the file-integrity operator with the following. 
### The operator is installed in the openshift project 
### The approval strategy is Automatic  
### Cluster monitoring is enabled for the openshift-file-integrity project.  

## Solution 

1> Select this 
<img width="1419" height="639" alt="image" src="https://github.com/user-attachments/assets/2a56e65b-a392-4985-9114-fa7266d40a28" />

2 > install it 

3> View Operator >> file integirty >> create instance 
# Question 16 

## Create a Cron job using the image at registry.ocp4.example.com:8443/redhattraining/hello-world-nginx:latest with the following requirements.  
## The cron job name is job-runner 
## The cron job runs at 04:04 on the 2nd day of every month.  
## The successful job histroy limit is 14 
## The service account and service account name is magna 
## The cron job runs in the project called elementum 

## solution:

<img width="1248" height="479" alt="image" src="https://github.com/user-attachments/assets/2936800b-3982-46df-a5d1-a87f23bc5f1c" />

<img width="892" height="638" alt="image" src="https://github.com/user-attachments/assets/42503340-c50f-468e-a31c-0f38f85c630d" />



 

 
 






