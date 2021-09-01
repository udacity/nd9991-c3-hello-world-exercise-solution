# hello-world

>**Before you proceed:** Fork this repository and set it up as a project in [CircleCI](https://app.circleci.com/projects/) dashboard. Feel free to submit PRs if you find any improvements. 


Here is the list of files and corresponding exercises. 
```bash
├── ansible.cfg             ### 4. Exercise: Config and Deployment
├── bucket.yml              ### 7. Exercise: Promote to Production
├── cloudfront.yml
├── error.html
├── index.html
├── inventory.txt           ### 2. Exercise: Remote Control Using Ansible
├── main1.yml               ### 1. Classroom Demo: Design an Ansible Playbook 
├── main2.yml               ### 1. Exercise: Define Ansible Playbook 
├── main3.yml               ### 2. Classroom Demo: Remote Control Using Ansible
├── main4.yml               ### 2. Exercise: Remote Control Using Ansible
├── roles                   ### Ansible exercises
│   ├── apache              ### 2. Classroom Demo: Remote Control Using Ansible
│   │   ├── files
│   │   │   └── index.html
│   │   └── tasks
│   │       └── main.yml
│   ├── configure-server    ### 1. Classroom Demo: Design an Ansible Playbook 
│   │   └── tasks
│   │       └── main.yml
│   ├── prepare             ### 2. Classroom Demo: Remote Control Using Ansible
│   │   └── tasks
│   │       └── main.yml
│   ├── print               ### 1. Exercise: Define Ansible Playbook 
│   │   └── tasks
│   │       └── main.yml
│   └── setup               ### 2. Exercise: Remote Control Using Ansible
│       ├── files
│       │   └── index.js
│       └── tasks
│           └── main.yml
└── template.yml            ### 3. Exercise: Infrastructure Creation
└── .circleci
    └── config.yml          ### CircleCI exercises
```

> **Note**: When you attempt any CircleCI exercise, you should comment out the Jobs and Workflows from other exercises. This will ensure that you do not end up creating unnecessary EC2, S3, CloudFront resources in your AWS console. 


### 1. Exercise: Define Ansible Playbook
Files relevant for this exercise are:
```bash
├── main2.yml   # Playbook file
└── roles
    └── print
        └── tasks
            └── main.yml
```

### 2. Exercise: Remote Control Using Ansible
**Prerequisite**: 
- A linux EC2 instance with port 3000 open for the inbound access. 
- Public IP address of an EC2 instance in your AWS account.
- A key pair to connect your EC2 instance

Files relevant for this exercise are:
```bash
├── main4.yml     # Playbook file
└── roles
    └── setup
        ├── files
        │   └── index.js
        └── tasks
            └── main.yml
```

### 3. Exercise: Infrastructure Creation
Files relevant for this exercise are:
```bash
└── template.yml            # Change the KeyName property value, as applicable to you
└── .circleci
    └── config.yml          # Look for the create_infrastructure Job
```


### 4. Exercise: Config and Deployment
**Prerequisite**: 
- Create an EC2 instance and note it's public IP address
- Add the contents of your PEM file to the SSH keys in your Circle CI account to get the fingerprints

Files relevant for this exercise are:
```bash        
├── ansible.cfg             
└── .circleci
    └── config.yml          # Look for the configure_infrastructure Job
```


### 5. Exercise: Smoke Testing
Files relevant for this exercise are:
```bash           
└── .circleci
    └── config.yml          # Look for the smoke_test Job
```


### 6. Exercise - Rollback
Files relevant for this exercise are:
```bash    
└── template.yml            # Change the KeyName property value, as applicable to you       
└── .circleci
    └── config.yml          # Look for the create_infrastructure Job and destroy_environment command. 
```


### 7. Exercise: Promote to Production
**Prerequisite**: 
- An S3 bucket (say `mybucket644752792305`) containing a sample `index.html` file created manually in your AWS console. 
- Enable the Static website hosting in that bucket.
- Use the command below to create a  CloudFront Distribution
```bash
 aws cloudformation deploy \
 --template-file cloudfront.yml \
 --stack-name production-distro \
 --parameter-overrides PipelineID="mybucket644752792305"
 ```
Files relevant for this exercise are:
```bash  
├── bucket.yml          # Creates a new bucket and bucket policy.       
├── cloudfront.yml      # Creates a Cloudfront Distribution that will connect to the existing ^ bucket.
├── error.html
├── index.html  
# Four Jobs: create_and_deploy_front_end, get_last_deployment_id, promote_to_production, and clean_up_old_front_end
└── .circleci
    └── config.yml
```
