# container-scan

This repository contains scripts which can run GCP on-demand container vulnerability scan and send findings summary if there are CRITICAL and HIGH vulnerabilities found.

# prerequisites 
- slack webhook with your preferred channel
- existing Github Actions workflow with Docker build
- Ubuntu 22.04 LTS Github runner with jq tool pre-installed

# script integration with your workflow

add the below code just after container build step has been completed:
````
- name:
  run: script.sh
  (TODO: more details to be added)