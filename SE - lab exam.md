SE - lab exam 

1\) Jenkins 

q1) two pipeline

q2) three pipeline

q3) buildtriggers - webhook

q4) email-notification

q5)scripted pipeline




prerequisites 

1\) local host tomct - 8080 

2\) plugins - email extension

3\) tools and configuration - maven,git,jdk



Jenkins codes-

q1)
pipeline {
    agent any

    tools {
        maven 'maven'
        jdk 'jdk22'
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/archanareddyse/mavenweb.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                bat 'copy target\\mavenweb.war C:\\apache-tomcat-9.0.89\\webapps\\'
            }
        }
    }
}

Step 3 — Restart Tomcat
cd C:\apache-tomcat-9.0.89\bin
shutdown.bat
startup.bat



q2) two stage pipeline

pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/archanareddyse/mavenweb.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
    }
}


q3) 

pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/archanareddyse/mavenweb.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying to Tomcat...'
            }
        }
    }
}



q4)

pipeline {
    agent any

    tools {
        maven 'maven'
        jdk 'jdk22'
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/archanareddyse/mavenweb.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying WAR file to Tomcat server...'
            }
        }
    }

    post {
        success {
            mail to: 'mandajavali@gmail.com',
                 subject: "SUCCESS: ${env.JOB_NAME} Build #${env.BUILD_NUMBER}",
                 body: "Your Jenkins job '${env.JOB_NAME}' succeeded.\nCheck Console Output for details."
        }
        failure {
            mail to: 'mandajavali@gmail.com',
                 subject: "FAILURE: ${env.JOB_NAME} Build #${env.BUILD_NUMBER}",
                 body: "Your Jenkins job '${env.JOB_NAME}' failed.\nPlease check the errors."
        }
    }
}


q5) scripted pipeline-

node {
    stage('Clone') {
        git 'https://github.com/archanareddyse/mavenweb.git'
    }

    stage('Build') {
        bat 'mvn clean install'
    }

    stage('Deploy') {
        echo 'Deploying WAR file to Tomcat server...'
    }
}










7\)


commands in aws-



sudo su

sudo apt-get update

sudo apt-get install docker.io

sudo docker --version

sudo docker images

sudo docker ps

git clone http of maven-web application

-navigate to maven-web application 

cd maven-web folder name

ls

nano DockerFile



sudo docker built -t img1 .



sudo docker images

sudo docker run -d -p 8080:8080 img1

then go to chrome incognito and paste go into details and paste auto assigned ip address in incognito with port no 

ex 3.231.271.190:8080




welcome to maven web! in local host



-----------------------------------------------------------------------------------
Q ) kuberenetes - minikube

pre req- docker desktop and docker image



Minikube cmds- 





minkube start

minikube status

kubectl get deployments

--if u have previous deployments so to delete

kubectl delete deployment dep\_name

kubectl get pods

-- to delete the pods 

kubectl delete pod pod\_name

-- to create deployment 

kubectl create deployment mynginx --image=<docker hub image name>

eg: kubectl create deployment mynginx --image=<imagename>

-go to docker hub

-go to repo

-click on public view

-image name 

------------------------------------------------------

\- default image present in docker is nginx

kubectl create deployment mynginx --image=nginx

kubectl get deployments

--u should see nginx

kubectl get pods 

kubectl describe pods 

//expose deployment service

kubectl expose deployment mynginx --type=NodePort --port=80 --target-port=80 -- for default like nginx

kubectl expose deployment mynginx --type=NodePort --port=8080 --target-port=8080 -- for customade images

kubectl get service mynginx 

kubectl port-forward svc/mynginx 80:80 - for nginx 

now go to chrome and paste localhost:80 - for nginx 

and localhost:8080 - for other images





kubectl scale deployment mynginx --replicas=4



--------------------------------------------------------------------------

ngrok - tunnelling

----

webhooks

install ngrok

sign up ngrok

open the cmd prompt of ngrok




>ngrok http 80


GitHub--repo--settiings--webhoooks-underpayload-paste grok forwarding url



add - /github-webhook/ 

https://9938c896b282.ngrok-free.app/github-webhook/
       

&nbsp;      v
from ngrok http 80 running in ngrok application in downloads C:/



----------------------------------------------------
ngios- 

//docker pull jasonrbriggs/nagios



1)

docker run -d -p 3000:80 jasonrivers/nagios

open localhost:3000 in browser

username- nagiosadmin
ps- nagios
login to nagios dashboard


----------------------------------------------------------------
DONEEEEEEEEEEEEEEE




now-


Q1 – Jenkins Pipeline for Maven Web App Deployment (Full CI/CD)

Clone → Build → Deploy WAR to Tomcat → View Running Output

🔹 Prerequisites

Install Jenkins

Install Java

Install Maven

Install Git

Install Tomcat

Set tool paths in Jenkins:

Manage Jenkins → Global Tool Configuration

Add:

JDK

Maven

Git

🔹 Step-by-Step
Step 1 — Create a New Pipeline Job

Jenkins → New Item

Name: mavenweb-pipeline

Choose Pipeline

Click OK

Step 2 — Add Jenkinsfile Script

Go to the bottom Pipeline Script section and paste:

pipeline {
    agent any

    tools {
        maven 'maven'
        jdk 'jdk22'
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/archanareddyse/mavenweb.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                bat 'copy target\\mavenweb.war C:\\apache-tomcat-9.0.89\\webapps\\'
            }
        }
    }
}

Step 3 — Restart Tomcat
cd C:\apache-tomcat-9.0.89\bin
shutdown.bat
startup.bat

Step 4 — Verify Deployment

Open:

http://localhost:8080/mavenweb


OUTPUT: Your web page: “Hello Welcome to Maven Web!”

🎯 Q1 Completed Successfully
✅ Q2 – Jenkins Freestyle Job for Maven Build
🔹 Steps
Step 1 — Create Freestyle Job

Jenkins → New Item

Name: mavenweb-freestyle

Select Freestyle Project

Step 2 — Add Git Repository

Go to Source Code Management → Git
Enter:

https://github.com/archanareddyse/mavenweb.git

Step 3 — Build Step

Choose:

Invoke top-level Maven targets


Goal:

clean install

Step 4 — Post Build Deployment

Add Post-build Action → Deploy WAR to container
Provide:

WAR path: target/mavenweb.war

Container: Tomcat 9

Tomcat URL: http://localhost:8080/

Credentials: Tomcat Manager user

Step 5 — Build Now

Result:

BUILD SUCCESS


Open:

http://localhost:8080/mavenweb/

🎯 Q2 Completed
✅ Q3 – GitHub Webhook Triggered Jenkins Build (CI)
🔹 Prerequisites

Install plugin: GitHub Integration

Install ngrok

Expose Jenkins:

ngrok http 8080


Copy the forwarding URL.

🔹 Steps
1. Jenkins – Configure GitHub Hook

Go to Your Pipeline → Configure

Scroll to Build Triggers

Enable:

GitHub hook trigger for GITScm polling

2. GitHub Repository → Settings → Webhooks

Add Webhook:

URL:

<ngrok-URL>/github-webhook/


Content type: application/json

Trigger: Just the push event

Webhook added successfully.

3. Commit Something

Edit README.md in GitHub → Commit.

Within seconds → Jenkins auto builds.

4. Verify

In Jenkins you will see:

Started by GitHub push by javali06

🎯 Q3 Completed
✅ Q4 – Jenkins Email Notification Setup
🔹 Steps
Step 1 — Install Email Extension Plugin

Go to:

Manage Jenkins → Plugins → Available


Install:

Email Extension Plugin

Step 2 — Configure SMTP

Go to:

Manage Jenkins → System


Scroll to Extended E-mail Notification
Set:

SMTP server: smtp.gmail.com
SMTP Port: 587
Use TLS: Yes
Username: your-gmail
App Password: 16-digit Google App Password

Step 3 — Add Email in Pipeline

Add inside Jenkinsfile:

post {
    success {
        mail to: 'mandajavali@gmail.com',
        subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: "Build was successful."
    }

    failure {
        mail to: 'mandajavali@gmail.com',
        subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: "Build failed. Check console output."
    }
}

Step 4 — Run Job

You get email notifications.

🎯 Q4 Completed
✳️ Q5 – Jenkins Scripted Pipeline (Using Node & Stages)
🔹 Scripted Pipeline Example

Create New Item → Pipeline → Scripted Pipeline

Paste:

node {
    stage('Clone') {
        git 'https://github.com/archanareddyse/mavenweb.git'
    }

    stage('Build') {
        bat "mvn clean install"
    }

    stage('Deploy') {
        echo 'Deploying to server...'
    }
}

Run Job → Success

You’ll see:

Started by user javali reddy
Cloning…
Building…
Deploying…
Finished: SUCCESS

🎯 Q5 Completed








/*

docker pull checkmk/check-mk-raw
docker run -d --name monitoring -p 8081:5000 checkmk/check-mk-raw
docker ps
 expected---- monitoring   0.0.0.0:8081->5000/tcp

open in- http://localhost:8081


docker exec -it monitoring bash
omd status
omd sites

omd start cmk

cat ~cmk/etc/htpasswd

cmkadmin


*/
-------------------------------------------------------------




ngrok - tunnel local ports to public URLs and inspect traffic



USAGE:

ngrok                                                                                                   (Ctrl+C to quit)



&nbsp;  Create instant endpoints for local containers within Docker Desktop → https://ngrok.com/r/docker



Session Status                online

Account                       Javali Reddy (Plan: Free)

Update                        update available (version 3.33.0, Ctrl-U to update)

Version                       3.22.1

Region                        India (in)

Latency                       184ms

Web Interface                 http://127.0.0.1:4040

Forwarding                    https://9938c896b282.ngrok-free.app -> http://localhost:80



Connections                   ttl     opn     rt1     rt5     p50     p90

&nbsp;                             0       0       0.00    0.00    0.00    0.00











------------------------------------------------------------------------





minikube start





\* minikube v1.37.0 on Microsoft Windows 11 Home 10.0.26200.7171 Build 26200.7171

\* Automatically selected the docker driver

\* Using Docker Desktop driver with root privileges

\* Starting "minikube" primary control-plane node in "minikube" cluster

\* Pulling base image v0.0.48 ...

\* Downloading Kubernetes v1.34.0 preload ...

&nbsp;   > preloaded-images-k8s-v18-v1...:  337.07 MiB / 337.07 MiB  100.00% 9.92 Mi

&nbsp;   > gcr.io/k8s-minikube/kicbase...:  488.52 MiB / 488.52 MiB  100.00% 7.90 Mi

\* Creating docker container (CPUs=2, Memory=4000MB) ...

! Failing to connect to https://registry.k8s.io/ from inside the minikube container

\* To pull new external images, you may need to configure a proxy: https://minikube.sigs.k8s.io/docs/reference/networking/proxy/

\* Preparing Kubernetes v1.34.0 on Docker 28.4.0 ...

\* Configuring bridge CNI (Container Networking Interface) ...

\* Verifying Kubernetes components...

&nbsp; - Using image gcr.io/k8s-minikube/storage-provisioner:v5

\* Enabled addons: storage-provisioner, default-storageclass



! C:\\Program Files\\Docker\\Docker\\resources\\bin\\kubectl.exe is version 1.30.5, which may have incompatibilities with Kubernetes 1.34.0.

&nbsp; - Want kubectl v1.34.0? Try 'minikube kubectl -- get pods -A'

\* Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default





PS C:\\Users\\manda> minikube status

minikube

type: Control Plane

host: Running

kubelet: Running

apiserver: Running

kubeconfig: Configured





PS C:\\Users\\manda> kubectl get deployments

No resources found in default namespace.



>

kubectl create deployment mynginx --image=<docker\_hubimage name>



&nbsp;kubectl create deployment mynginx --image=nginx

deployment.apps/mynginx created

PS C:\\Users\\manda>





&nbsp;kubectl get deployments

NAME      READY   UP-TO-DATE   AVAILABLE   AGE

mynginx   1/1     1            1           66s

PS C:\\Users\\manda> kubectl get pods

NAME                       READY   STATUS    RESTARTS   AGE

mynginx-645865c456-65v66   1/1     Running   0          73s

PS C:\\Users\\manda>







&nbsp;kubectl describe pods

Name:             mynginx-645865c456-65v66

Namespace:        default

Priority:         0

Service Account:  default

Node:             minikube/192.168.49.2

Start Time:       Tue, 18 Nov 2025 11:55:18 +0530

Labels:           app=mynginx

&nbsp;                 pod-template-hash=645865c456

Annotations:      <none>

Status:           Running

IP:               10.244.0.4

IPs:

&nbsp; IP:           10.244.0.4

Controlled By:  ReplicaSet/mynginx-645865c456

Containers:

&nbsp; nginx:

&nbsp;   Container ID:   docker://24f45468661b046806d140f1f8485601114806803019c8004b39859390d55603

&nbsp;   Image:          nginx

&nbsp;   Image ID:       docker-pullable://nginx@sha256:b5b9e01613537b740e597a1aca6b8670a48f2f46493be50775567b09a61465a5

&nbsp;   Port:           <none>

&nbsp;   Host Port:      <none>

&nbsp;   State:          Running

&nbsp;     Started:      Tue, 18 Nov 2025 11:55:50 +0530

&nbsp;   Ready:          True

&nbsp;   Restart Count:  0

&nbsp;   Environment:    <none>

&nbsp;   Mounts:

&nbsp;     /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-ww2gt (ro)

Conditions:

&nbsp; Type                        Status

&nbsp; PodReadyToStartContainers   True

&nbsp; Initialized                 True

&nbsp; Ready                       True

&nbsp; ContainersReady             True

&nbsp; PodScheduled                True

Volumes:

&nbsp; kube-api-access-ww2gt:

&nbsp;   Type:                    Projected (a volume that contains injected data from multiple sources)

&nbsp;   TokenExpirationSeconds:  3607

&nbsp;   ConfigMapName:           kube-root-ca.crt

&nbsp;   ConfigMapOptional:       <nil>

&nbsp;   DownwardAPI:             true

QoS Class:                   BestEffort

Node-Selectors:              <none>

Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s

&nbsp;                            node.kubernetes.io/unreachable:NoExecute op=Exists for 300s

Events:

&nbsp; Type    Reason     Age    From               Message

&nbsp; ----    ------     ----   ----               -------

&nbsp; Normal  Scheduled  2m44s  default-scheduler  Successfully assigned default/mynginx-645865c456-65v66 to minikube

&nbsp; Normal  Pulling    2m43s  kubelet            Pulling image "nginx"

&nbsp; Normal  Pulled     2m14s  kubelet            Successfully pulled image "nginx" in 29.118s (29.118s including waiting). Image size: 151862173 bytes.

&nbsp; Normal  Created    2m12s  kubelet            Created container: nginx

&nbsp; Normal  Started    2m12s  kubelet            Started container nginx

PS C:\\Users\\manda>









for other image-8080

for nginx- =80

using nginx>kubectl expose deployment mynginx --type=NodePort --port=80 --target-port=80

output-

service/mynginx exposed







>kubectl get service mynginx

NAME      TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE

mynginx   NodePort   10.96.69.255   <none>        80:32496/TCP   104s







kubectl scale deployment mynginx --replicas=4

deployment.apps/mynginx scaled

PS C:\\Users\\manda>





&nbsp;kubectl scale deployment mynginx --replicas=4

deployment.apps/mynginx scaled

PS C:\\Users\\manda> kubectl get deployment

NAME      READY   UP-TO-DATE   AVAILABLE   AGE

mynginx   4/4     4            4           27m

PS C:\\Users\\manda> kubectl get pods

NAME                       READY   STATUS    RESTARTS   AGE

mynginx-645865c456-5fkx9   1/1     Running   0          27s

mynginx-645865c456-65v66   1/1     Running   0          27m

mynginx-645865c456-fmmxz   1/1     Running   0          27s

mynginx-645865c456-qrxkl   1/1     Running   0          27s

PS C:\\Users\\manda>













