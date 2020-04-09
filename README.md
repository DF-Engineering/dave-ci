# dave-ci
Listens to a queue and performs certain actions based on the content in the message.

## Workflow

When 'dave-launcher' starts, it runs 'listener.sh' script in a loop. 
listener.sh script does the following: 
  - Downloads the Kubernetes configuration
  - Download templates from 'dave-core' Repo locally
  - Starts a 'while' loop to listens over a queue
    - if message found in queue, the message is pushed to a cache
    - execute 'job_launcher.py' script with the cache data as input argument
    - The 'job_launcher.py' performs the following action :
      - Parse the queue message
      - Identify the action to perform ( create / destroy)
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
      - Based on the information collected from queue message, 'dave-launcher' renders a values file.
      - This values file can be used with dave-deploy, to provision the container environment in Kubernetes.
  
