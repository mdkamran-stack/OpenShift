**Question-1**
Configure Identity Provider   
Configure Your Openshift cluster to use an HTPasswd identity provider with the Following.  
The name of the identity provider is ex:280-htpasswd  
The name of the secrets: ex280-idp-secret  
The user account armstrong is present and can log in with password indionce.  
The user account collins is present and can log in with the password veraster.  
The user account aldrin is present and can log in with password roonkere The user account jobs is present and can log with sestiver   
The user account wozniak is present and can log in with password glegunge.  

**use GUI in exam**

if auth fails 
=================
echo "192.168.64.129 oauth-openshift.apps.king.flahcloud.com" >> /etc/hosts

**Question2**
Configure cluster permissions  
configure your openshift cluster to meet the following requirements.  
The user account jobs can perform cluster administration tasks.  
The user account wozniak can create projects  
The user account wozniak cant perform cluster administration task ,The use account armstrong cant create projects  
The user account kubeadmin is not present  

**use GUI in exam**

**Question3**

Configure Project permissions.configure your Openshift cluster to meet the following requirements: The following projects exists.  
Apollo  
manhattan  
gemini  
bluebook  
titan  
The user account armstrong is an adminstrator for project apollo and project gemini The user account wozniak can view project titan but not administer or delete it.  

**use GUI in exam**

**Question4**

Configure groups
Configure your Openshift cluster to meet the following requirements.  
The user account armstrong is a member of the commander group  
The User account collins is a member of pilot group  
The user account aldrin is a member of the pilot group  
Members of the commander group have edit permission in the apollo project  
Members of the pilot group have view permission in the apollo Project.  

**use CLI in exam**

**Question5**

**Configure Quota**
Configure your openshift cluster to use quotas in the manhattan project with following reuirements.  
The name of the quota is: **ex280-quota**
The amount of memory consumed across all conatiner may not exceed 160 Mi  
The total amount of cpu consumed across all conatiner may not exceed 2 full cores  
The maximum no .of replication controllers does not exceed 3  
The maximum no of pods does not exceed 3 
The max no of service does not exceed 6  

**use CLI in exam**

**Question6**

Configure a secure route  
Configure the oxcart application in the area51 project with the following requirements:  

The application uses a secure route called oxcart  
Traffic between the client and the router is encrypted  
Traffic between the router and the service is unencrypted  
The route uses a CA signed certificate with the follwoing subject fields:  
/C=US/ST=NV/L=HIKO/O=CIA/OU=UASF/CN=classiffied.apps.domain20.example.com  
The application is reachable only at the following address: https://classified.apps.doman20.eample.com  
The application produces output   

**Question7**

Deploy an application 
EX280 exam prepared for Deploy the chart named **redhat-movie** in the project ascii-movie from the repository  
http://helm.domain20.example.com/chart//  
you may use the telnet or ne commands to validate the deployment.  





