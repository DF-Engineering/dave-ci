# dave-ci
Docker container listening to a single API method to deploy a Kubernetes job.

## Workflow

When 'dave-ci' container starts, it runs a script in loop. 

Script does the following: 
  - Downloads the Kubernetes configuration
  - Downloads deployment templates from Github repo
  - Starts a 'while' loop to listens for POST request
    - The 'py' script performs the following action :
      - Parse the message
      - Parse the action to perform ( create / destroy)
      - Parse the message for :
        - registry
        - image
        - userid
        - groupid
        - namespace
        - cpulimits
        - memlimits
        - cpurequests
        - memrequests
        - producttag
        - containerport
        - randomstring
      - Based on the information collected from message, 'dave-vi' renders a values file.
      - This values file can be used with "dave-deploy", to easily provision containers in Kubernetes environment.
        (GitHub Repo: https://github.com/DF-Engineering/dave-deploy.git)
  
