# ToolIngestion

This repo supplies a Jenkinsfile that gets triggered upon status changes to issues in Jira via a webhook. The Jenkinsfile then uses the URL field in the Jira issue (this is the URL to the tool that should be downloaded) and pulls the tool from the web into a specificed folder inside a VM. If completed successfully, Jenkins updates the JIRA issue to be in 'Complete' status, if the build fails the JIRA issue moves to 'Blocked' status. Jenkins also adds comments to the JIRA issue throughout this process.
