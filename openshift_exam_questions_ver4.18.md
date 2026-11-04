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





