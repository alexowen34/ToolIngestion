# ToolIngestion

This repo supplies a Jenkinsfile that gets triggered upon status changes to issues in Jira. The Jenkinsfile then uses the URL specified in the Jira issues to download the contents into a specificed folder inside a VM. Jenkins then adds a comment to the Jira issue with a link to the Jenkins build.
