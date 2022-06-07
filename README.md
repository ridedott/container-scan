# GCP on-demand container scan

This repository contains script which can run GCP on-demand container vulnerability scan.

It solves the problem of being not able to know how secure or vulnerable your image is before pushing to Artifactory and deploying.

By design this script is made to be easily integrated with any Github Actions Workflows, where container build step exists.

## Integration
The ease of usage is explained below:

- Create slack webhook 
    
    You will need to create slack webhook for your preferred notification channel in slack workspace. To access App configuration page click here [Slack App Config].
> Note: New webhook can be created only by Workspace admins, therefore please contact your Engineering Manager to complete this step.
 
- Add the below code in to Github Actions workflow .yaml file, just after container build step has been completed

````
      - name: scan
        run: ./scan.sh
        working-directory: ./
        env:
          githubUrl: ${{ github.server_url }}/${{ github.repository }}/actions/runs/${{ github.run_id }}
          containerTag: localbuild/container
          slackWebhook: ${{ secrets.CONTAINER_SCAN_SLACK_WEBHOOK }}
````

> Note: Align indentation with your workflow, as this varies from project to project

## Variables
`githubUrl` - Full path to your Github Actions run

`containerTag` - Image name reference to what your docker build command tag the container you are intending to scan

`slackWebhook` - This is slack webhook url which will remain secret and can be accessed in Repository > Settings > Actions > Secrets 
> Note: In order to access Repository Settings section you would require special permissions such as - Organization administrators, repository administrators, and teams with the security manager role


## Prerequisites 
- Slack webhook with your preferred channel
- Existing Github Actions workflow with Docker build
- Ubuntu 22.04 LTS Github runner with jq tool pre-installed

## Features

- Scan container image using GCP CVE database
- Obtain scan results and output in the Github Actions Workflow
- Count the results and provide results summary
- Fail Github Actions Workflow if CRITICAL or/and HIGH vulnerabilities are found
- Send notification to your preferred Slack channel when CRITICAL or/and HIGH vulnerabilities are found (contains only summary of results and link to Github job accordingly)
- 
## Support

If you are having issues, please let us know on Slack #report-issue-platform


[Slack App Config]: <https://api.slack.com/apps/A03HZNNTMA4/incoming-webhooks>