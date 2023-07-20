# Training Workshop Kit

> [Docker ](Dockerfile) : Open platform for developers and sysadmins to build, ship, and run distributed applications as containers, whether on laptops, data center VMs, or the cloud.

> [CircleCI ](https://circleci.foc.zone/gh/Servicing/dolphin-api) : Continuous Integration (CI) and Continuous Deployments (CD) tool

> [AWS Elastic Container Service (ECS) ](https://aws.amazon.com/ecs/) : Orchestration of Docker containers on EC2 instances. This runs the code, auto-scales containers and the EC2's they run on up and down, as well as handling the infrastructure side of deploying new code.

> [HAL9000 ](https://hal9000/applications/933/status) : QL in-house application that handles deployments and releases to various environments (including AWS). It also handles a lot of the encrypted configuration values which are passed to the code as Environment Variables.

> [Terraform ](https://www.terraform.io/) : Terraform is Infrastructure-As-Code (IAC) that can build out highly QL-specific infrastructure components in a repeatable way. Instead of a lot of click-and-configure, we can run terraform scripts to create approved infrastructure stacks on-demand in minutes.

# Prerequisites

**These are the prereqs which are needed prior to coming to a workshop. The following should be completed and ready to go:**

- Docker installed locally ( **Install through Software Center (PC) or Self Service (Mac)** - If you install from the Docker web site, you will be missing key network policies needed )
    * If using a Windows PC, make sure right-click the Docker icon in your system tray and make sure it's set to use LINUX containers. In other words, it should set "Switch to Windows containers", which means it's currently on Linux containers.
    * Once the above steps are complete (regardless of operating system), open a command prompt/terminal window, enter the following command, and wait for it to complete: "docker pull microsoft/dotnet:2.1-sdk"
- VSCode or similar file editor ( https://code.visualstudio.com/download )
- AWSCLI installed ( https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html )
- Request AWS account access to Training Lab Account (418023852230). Navigate to myaccess/ in your browser, click "Add/Remove Access", and search for `AWS-SSO-TrainingIAC-NonProd-ServerEngineer`. Click the checkbox and request it for your dash account. Then click "Review and Submit", then "Submit".
- Terraform ( https://www.terraform.io/ )
    * If using a Windows PC, wherever you download Terraform to, make sure to add that path to your PATH variable. See here for how: https://helpdeskgeek.com/windows-10/add-windows-path-environment-variable/
    * If Mac, see here: https://osxdaily.com/2014/08/14/add-new-path-to-path-command-line/
    * Effectively, you want to be in any folder on your computer and be able to call that binary. To test, go to the command line of your OS and type "terraform version": you should get the version back. If not, see someone from IT Team Sudo.
- Create demo repository under your personal QL GIT org ( https://git.rockfin.com/YOURNAME/999999-YOURNAME-iac )
- If you've never used HAL before, go to hal9000/ in your browser and login with your dash account. This will create your account in HAL.
- Clone example GIT project locally ( see below )

## Setting up GIT

1. Clone this repo locally to your laptop ( https://git.rockfin.com/training-iac/training-starter-kit.git )

2. Rename the folder to this naming standard: **999999-YOURNAME-iac**, where YOURNAME is your AD network login (first initial, last name). Then, delete the **.git** folder at the root; this allows you to associate this folder with a different git repo. This will become the base for the Git repo for your application's infrastructure.

3. Make a repo with the same name as what you called the folder in step 2 under your personal Git organization. https://git.rockfin.com/YOUR-NAME/999999-YOURNAME-iac. For example, https://git.rockfin.com/jsmith/999999-jsmith-iac

4. Follow the instructions given to you post-creation in your browser to upload your modified clone of the starter-kit to your applications new IAC repo. The one difference is instead of "git add README.md", type "git add -A" instead to add everything.

You are all set if you have a custom-named version of the starter kit uploaded and ready to go in your personal (QL-owned) GIT org.


## Peter's Docker Notes (Josh Noble):
1.  Training PDFs: https://git.rockfin.com/training-iac/presentation_pdfs
2.  Build the app (dir: /Users/pvarga/projects/999999-pvarga-iac/workshop_materials/Docker/sample-container): 
        docker build -t pvarga -f  Dockerfile  .
3.  Run the container, detached, access on port 5001 and listening on 80: docker run -d -p 5001:80 pvarga  // http://localhost:5001/
4.  List the containers: docker ps
5.  Stop the container: docker stop <ID>
6.  Kill it: docker rmi <img name> --force
7.  Enter the container, interactively: docker exec -it <img name hash> /bin/sh
8.  To exit a container that you're "in", type "exit" in the docker container prompt: exit
9.  Docs: https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#env
10. Voting App: https://github.com/peterquicken/example-voting-app
11. Voting App Docs: https://medium.com/better-programming/dockers-voting-app-on-swarm-kubernetes-and-nomad-8835a82050cf 

## Peter's AWS Notes (Jason Billiau):
1.  EC2 Docs: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html 
2.  ECS Docs: https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html 
3.  Lambda Docs: https://docs.aws.amazon.com/lambda/latest/dg/welcome.html
4.  QL Certs: https://git.rockfin.com/sudoers/ssm-instance-connect/blob/master/files/qlcerts.pem (put it into ~/.aws directory: Example: /Users/pvarga/.aws)
5.  aws pvarga$ aws configure > access key: XXX / secret: XXX
6.  Once configured, paste this in (V2): aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 418023852230.dkr.ecr.us-east-2.amazonaws.com
7.  Once pushed you can see if your docker container is here: https://us-east-2.console.aws.amazon.com/ecr/repositories/training-ecr/?region=us-east-2
8.  AWS DOCS: https://git.rockfin.com/training-iac/training-starter-kit/tree/master/docs/AWS
9.  Auth Token decrypter: JWT.io 
10. Docs: https://git.rockfin.com/training-iac/training-starter-kit/tree/master/docs/AWS

## Peter's Terraform Notes (Howard Luck):
1.  Terraform Init
2.  Terraform Plan (HAL Build)
3.  Terraform Apply (HAL Push)
4.  MS Teams Channel: IT Team Community Cloud
5.  Modules: Terraform folders/files: http://shorty/tf-example 
6.  Docs: https://git.rockfin.com/training-iac/training-starter-kit/tree/master/docs/terraform 
7.  TF Samples: https://git.rockfin.com/terraform 
8.  Lab1: http://shorty/tf-lab-1 
9.  TF Docs: https://www.terraform.io/docs/index.html 
10. Lab2: http://shorty/tf-lab-2

## Peter's CI/CD (HAL + CircleCI) Notes (Bryce Anderson):
1.  Docker containers > Cloud (AWS) > IAC (Terraform) > Deploying Stuff (HAL) > CI/CD
2.  SonarQube http://sonar/ & https://shorty/sonardocs 
3.  Quality Gates: https://shorty/qg
4.  CircleCI: https://circleci.foc.zone/
5.  Lab: http://shorty/circle-lab-1 
6.  Docs: https://aws.amazon.com/blogs/containers/aws-codedeploy-now-supports-linear-and-canary-deployments-for-amazon-ecs/ 
7.  Persist Workspace: https://circleci.com/docs/2.0/configuration-reference/#persist_to_workspace 
8.  Setup Remote Docker: https://circleci.com/docs/2.0/configuration-reference/#setup_remote_docker 
9.  Building Docker Images: https://circleci.com/docs/2.0/building-docker-images/
10. Pre-Built Docker images: https://circleci.com/docs/2.0/circleci-images/​​​​​​​
11. http://git.rockfin.com/sudoers/ssm-instance-connect
12. Route53 "All The Things!" (easier maintenance)
13. https://accelerators.foc.zone/ 
