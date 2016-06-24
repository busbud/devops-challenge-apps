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
1. The result of running the scripts should be two publicly available tiers: web and api
    1. Each tier should have either a dedicated subdomain (web.example.com, api.example.com, port 80 or 443 as you choose) or ports (host can be an IP address, with each port number of your choosing). In either case, please specify how we can access each service via curl
1. We should be able to run the script against our own AWS infrastructure and be able to launch the same tiers with minimal custom configuration or install steps. Please specify the command to execute and any setup required to ensure a successful run. Again, please specify how you would expect we can access each service via curl

#### Non-Functional Requirements
1. The scripts should be delivered as a public repo on Github or a pull-request made against the https://github.com/busbud/devops-challenge-apps repo
1. Assuming an uptime of 99.95% for EC2 instances (similar for RDS or other services) on a monthly basis, describe the expected uptime for the environment created by your scripts. Explain which steps you've taken to improve availability and quantify their impact.

## Part 2: Prose
For this section, we expect the main deliverable to prose, delivered via Github (you can also upload a PDF) or a Google Doc. We mainly expect a description of the approach to implement your solution, as opposed to the code to implement it. However, if coding is faster, then by all means, deliver code!

### 2. Canary deploy
> A "Canary Deployment" is a type of incremental release performed by deploying a new version of software side by side with its production version counterpart

#### Objective
Given the muti-tier application described in https://github.com/busbud/devops-challenge-apps, how would you implement a Canary Deploy for the web and api tiers?

Update your scripts to support it, or reference technologies, services, scripts and APIs as necessary. Add any supporting materials (diagrams, spreadsheets, PDFs, etc) as appropriate. 

Describe the lifecycle of a change, starting from the developer that authors it to it being the code that all production instances run.

#### Context
- The web and api tiers have multiple container instances
- Assume every commit and merge pushed to the https://github.com/busbud/devops-challenge-apps repo results in a test run through CircleCI (or TravisCI) providing unit test based code coverage and some functional tests, and build statuses on CI are integrated with Github as well
- Assume functional tests are run on a scheduled basis or on demand using Rainforest QA, and the tests can be executed against arbitrary environments (see [Full support for multiple Sites and Environments](https://www.rainforestqa.com/features/))
- Assume most developers would deliver changes as topic branches forked from master, and a branch is considered ready to ship to production once it has been reviewed, CI tests pass and functional tests pass
- Application real-time metrics are tracked via logs, New Relic, Data Dog, Sentry or any other system you believe should be added to support your solution. The business cares mainly about the number of correct responses (200s) and maintaining low latency (<100ms).

#### Functional Requirements
- The solution should support at least 5 to 10 deployments per day on each tier
- The solution should support deployments to each tier that are either simultaneous or not
- The solution should support manual rollbacks in addition to the canary process
- The solution should support a bypass of the canary process for emergencies
- The solution should describe how to handle database migrations with respect to the api app code deployment

### 3. Policy configuration
Performance tests have revealed that serving the image from the web tier consumes too many resources and we should instead use a CDN to serve it.

See
https://github.com/busbud/devops-challenge-apps/blob/master/web/views/index.jade#L6

The team wants the improved performance, but would also like to be able to periodically change the image and decides that using S3 to serve the original image is best (they would upload the new image and overwrite the same file in the bucket), but leaves you to choose the CDN against which the image request will be made.

Designers and marketing team members want to be able to update the image, and devs want to be sure it is optimized (and if it isn't, be able to fix it).

#### Functional requirements
- Describe the way you would configure AWS S3 and IAM to support this use case with multiple devs, designers and marketers.
- Describe the changes you would propose to the web app to have the image served from from S3 via a CDN (CDN choice is yours, some suggestions are Cloudfront, Fastly, and Imgix)

Add any supporting materials (diagrams, spreadsheets, PDFs, etc) as appropriate.

### 4. Monitoring
Visit [Busbud.com's search results page displaying bus departures](https://www.busbud.com/en/bus-schedules-results/djn4k5/dhwfxh?outbound_date=P2D&adults=1&children=0&seniors=0&child_ages=&senior_ages=&discount_code&utm_source=busbud&utm_medium=github&utm_campaign=devops-coding-challenge) - what are the top 10 metrics you would monitor for the systems you imagine would support this. Explain why you would choose those metrics.
