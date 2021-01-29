# ToolIngestion

This repo supplies a Jenkinsfile that gets triggered upon status changes to issues in Jira. The Jenkinsfile then uses the URL field in the Jira issue (this is the URL to the tool that should be downloaded) and pulls the tool from the web into specificed folder inside a VM. Jenkins then adds a comment to the Jira issue with a link to the Jenkins build.
