# CI/CD pipeline using Jenkins


## Requirements:
- Application Server (installation package: Docker)
- Jenkins Server (Installation Package: Jenkins, Docker)

> Note: Configure ssh keygen for password less login from Jenkins server to application server
This videw will help you to create pass less: [Configure SSH Password less Login Authentication using SSH keygen on Linux](https://www.youtube.com/watch?v=9M56CrVbOgk)

## Docker HUB & Git Account

Note: Create repository and add require file. You can download all file from my repo:
https://github.com/Arefinrumi/DEV_PRO.git
branch should be master
look like this—
![image](https://user-images.githubusercontent.com/76535072/196407250-c2902339-35d1-4c2c-89c1-08c4eca31560.png)

## Jenkins Web UI 
login jenkins account from web and install ssh agent plugin from manage plugin.
![image](https://user-images.githubusercontent.com/76535072/196407430-e2af4c9d-fcdb-4cec-a276-5b607ab1290b.png)

environment is ready now. Let’s start deployment!!!!!

## Step-1: Open Jenkins file from your git and modify it look like this…

![image](https://user-images.githubusercontent.com/76535072/196447471-26acdefe-2590-42dd-8c41-697edf79d2bc.png)
Modify as per above snap  & save Jenkinsfile.

## Step-2:  Now login Jenkins from browser and create new pipeline:
Go to new item—Item name – (write item name)—choose pipeline – click ok
Pipeline created. Check below pic for visual..

![image](https://user-images.githubusercontent.com/76535072/196447705-99fc46de-cb5b-446e-b5a5-d4bd93b59b6e.png)

## Step-3: Under pipeline go to definition and select pipeline scrip from SCM
From SCM section select git
From Repositories option provides your repositories URL
Brance name should be master
Below pic for visualize!!

![image](https://user-images.githubusercontent.com/76535072/196447818-146dbe5b-cce5-45a1-b631-6c18a2fd1b91.png)

## Step-4: In the last section from pipeline you will be find Pipeline Syntax option Please click it and it will be open from new TAB. Look like this----

![image](https://user-images.githubusercontent.com/76535072/196447927-a97a7e50-052e-4b3f-9c42-e1d8b311b9af.png)
Note: From this pipeline syntax we will get many types of syntax for Jenkins File. 
We need to 2(two pipeline syntax for Jenkins file which one for credentials & another one for ssh agent)

## Let’s create syntax from sample step:

First we need to choose from sample step with Credentials: Bind credentials to variables
From Bindings  click Add & choose Secret text 
Vairable: dockerhubpassword
From Credentials—Add—Jenkins—Kind—Secret text—Secret= (in this secret section provide your docker hub account password)—ID= dockerpassword1 (this is credential ID which you can find from Jenkinsfile)—Description= dockerhubpassword
 Now Click “add” button then click “Generate Pipeline Script”
Your output should be like this---

![image](https://user-images.githubusercontent.com/76535072/196448274-8fb920b8-8695-4c6b-aa67-426ef1e0bd79.png)

## Step-5: Now we Generate pipeline script for SSHAgent
From pipeline syntax-

From Sample Step to select  sshagent: SSH Agent 
Click Add—Jenkins
From kind select SSH username with private key
ID=  dockerserver
Username= root (provide jenkins server username)
From Private Key select Enter directly 
Click add and provide private key from your Jenkins server.
How to find private key from Jenkins server:
Login Jenkins server
#cd .ssh
#ls
#cat id_rsa 
Here you find private key select all and paste it.

After provide private key click add.
Then click Generate pipeline Script

SSH Agent syntax done! See below pic you got output look like this…

![image](https://user-images.githubusercontent.com/76535072/196448725-132462b4-4f33-447e-a30a-6b9e0d32000e.png)

## Step-6: We have almost near to build our pipeline. Before bulding pipeline we need to give permission to our Jenkins server for running Docker Deamon. Let’s do it.

Login Jenkins server:
#usermod –aG docker Jenkins
#reboot

After rebooting the server login your Jenkins from web browser and bulid your pipeline from build now section. If job build is success that’s means your configuration ok, if any failed check log and resolve it.

Successful pipeline build look like this…

![image](https://user-images.githubusercontent.com/76535072/196448883-8074ac14-012b-42b8-bfae-81fda268aefc.png)
For check open your browser and write your application server IP with 4040 port!

![image](https://user-images.githubusercontent.com/76535072/196448965-9338c458-ee4a-4005-b777-c2b026c49161.png)
Every visit will be count!!!!!

> Project Done!



