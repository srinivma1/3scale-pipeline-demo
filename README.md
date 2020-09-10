# 3scale-pipeline-demo

# Introduction

In this demo, we would be automating the deployment of 3scale API from staging to production. Following steps will be performed as part of this automation

 a. Import OpenAPI specification
 
 b. Create Application Plan
 
 c. Create Application
 
 d. Perform Integration Tests in the staging environment.
 
 e. Promote to Production Environment.
 
 


# Prerequisites

1. Install 3scale-toolbox.

  a. Install Ruby
  
  ```
  sudo yum install git-core zlib zlib-devel gcc-c++ patch readline readline-devel libyaml-devel libffi-devel openssl-devel make bzip2 autoconf automake libtool bison curl sqlite-devel
  
  curl -sL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-installer | bash -
  
  echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
  echo 'eval "$(rbenv init -)"' >> ~/.bashrc
  source ~/.bashrc
  
  rbenv install 2.5.1
  rbenv global 2.5.1
  
  ruby -v
  ```
  
  b. Install 3scale-toolbox
  
  ```
  gem install 3scale_toolbox
  
  ```
  
  2. Install Jenkins on Openshift
  ```
  oc new-app jenkins-ephemeral
  ```
  
  3. Install backend API application. Refer to following git URL for installing the backend API application :
  
       https://github.com/srinivma1/CamelK-customerAPI.git

  # Pipeline Demo
  
  Initialize 3scale toolbox with actual tenant to be used as shown below:
  ```
   3scale -k remote add dha-tenant https://<TENANT_ACCESS_TOKEN>@<TENANT_ADMIN_URL>

   ```
  
  Create Jenkins build pipeline using below commands:
  
  ```
  oc apply -f 3scale-build-pipeline.yaml
  
  ```
  Above command creates BuildConfig object in Openshift.
  
  Start the build
  
