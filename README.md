# devops-challenge-apps
This repo contains code for a multi-tier application.

The application overview is as follows

```
web <=> api <=> db
```

The folders `web` and `api` respectively describe how to install and run each app.

# Busbud DevOps Challenge
## Part 1: Code
For this section, we expect the main deliverable to be code, delivered via Github.

### 1. Infrastructure setup
#### Objective
Create the scripts (Terraform, Ansible or other) to deploy the multi-tier application with source code hosted at https://github.com/busbud/devops-challenge-apps

#### Functional Requirements
1. The web and api tiers must have multiple container instances.
1. The API needs one database (PostgreSQL) and this service needs be in a container.
1. The solution should support docker image versioning
1. The solution should write all the logs to the Rsyslog service (Operating System and containers included)
1. The solution must handle instance and container failures
1. The result of running the scripts should be two publicly available tiers: web and api
    1. Each tier should have either a dedicated subdomain (web.example.com, api.example.com, port 80 or 443 as you choose) or ports (host can be an IP address, with each port number of your choosing). In either case, please specify how we can access each service via curl
1. We should be able to run the script against our own AWS infrastructure and be able to launch the same tiers with minimal custom configuration or install steps. Please specify the command to execute and any setup required to ensure a successful run. Again, please specify how you would expect we can access each service via curl

#### Non-Functional Requirements
1. The scripts should be delivered as a public repo on Github or a pull-request made against the https://github.com/busbud/devops-challenge-apps repo

## Part 2: Prose
For this section, we expect the main deliverable to be prose, delivered via Github (you can also upload a PDF) or a Google Doc. We mainly expect a description of the approach to implement your solution, as opposed to the code to implement it. However, if coding is faster, then by all means, deliver code!

### 2.1 Monitoring
Suggest any solution to improve monitoring beyond the basics offered by AWS Cloudwatch.

### 2.2 Database Migrations
Describe how to handle database migrations with respect to the api app code deployment.
