[![Codacy Badge](https://api.codacy.com/project/badge/Grade/19bf967611ae44fd9f33301572b91266)](https://app.codacy.com/gh/yuvalpress/version-notifier?utm_source=github.com&utm_medium=referral&utm_content=yuvalpress/version-notifier&utm_campaign=Badge_Grade_Settings)
# Version Notifier</br>[![Codacy Badge](https://api.codacy.com/project/badge/Grade/a3bbaf5dc7534b4a9bf9eaef49e41b34)](https://app.codacy.com/gh/yuvalpress/version-notifier?utm_source=github.com\&utm_medium=referral\&utm_content=yuvalpress/version-notifier\&utm_campaign=Badge_Grade_Settings) [![Docker Build](https://github.com/yuvalpress/version-notifier/workflows/Docker%20Build/badge.svg)](https://github.com/yuvalpress/version-notifier/actions?query=workflow%3ADocker%20Build) [![Chart Release](https://github.com/yuvalpress/version-notifier/workflows/Chart%20Release/badge.svg)](https://github.com/yuvalpress/version-notifier/actions?query=workflow%3A%22Chart+Release%22)
🕷 **Version Notifier** - your Friendly Neighborhood Spiderman, only geeker 🤓

Version Notifier is a modern solution for the "being notified" aspect of each Techy's day-to-day work.
</br>By using it, you'll be notified for any new global GitHub repository release you choose, directly to your Slack channel.</br></br>

## Getting Started 🏁
You can deploy the application in one of two ways:
  * **HELM**
</br> Download the latest release and deploy it to your Kubernetes cluster </br>
  ```shell
    
  ```

  * **Docker Image**
</br> Create a dockerfile from the Version-Notifier base image and deploy it in as a standalone container:
  ```dockerfile
    # Name this file Dockerfile
    FROM yuvalpress/version-notifier:latest
    
    # You MUST Set this environment variables for the application to send notification to slack
    ENV SLACK_CHANNEL {{ value }}
    ENV SLACK_TOKEN {{ value }}
    
    # Optional
    ENV NOTIFY {{ value }}
  ```
  
  Build and Deploy:
  ```shell
    # Run this command from the Dockerfile dir
    docker build -t {{ value }} .
    docker run --name {{ value }}
  ```

## Configuration Options 🕹
`NOTIFY` - List represented as string with the following possible keywords: `major, minor, patch, all`
</br></br> Possible combinations:
  * "all" - `all` must be set alone
  * "major, patch" - only notify for `major` and `patch` version changes
  * "minor" - only notify about `minor` version changes

If not set, NOTIFY will be automatically set to `all`</br></br>

## Verification of Success 🎯
If the deployment was successful, you'll see the logs rolling out of your container: </br></br>
### Using Docker
If you executed Version Notifier using Docker, you'll see the logs roll after you run the container.
![Docker Run](./docs/docker.gif)
### Watch logs with kubernetes
```shell
pod=$(kubectl get pods -n notifier -l app=version-notifier -o yaml | yq '.items[0].metadata.name') && kubectl logs $pod -n notifier -f
```
