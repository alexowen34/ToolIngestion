String URL = URL_FOR_TOOL
String sharedDrivePath = "C:\\Users\\rootadmin\\SHARED DRIVE"

pipeline {
    
    agent {label 'Windows'}

    stages {
        stage('Jira: Notify Issue Build Started') {
            steps {
                script{
                    jiraAddComment comment: "Jenkins build: " + BUILD_NUMBER + ", has started.", idOrKey: JIRA_ISSUE_KEY, site: 'Jira'
                }
            }
        }
        stage('Jira: Issue Infomation') {
            steps {
                echo 'This job relates to JIRA issue: ' + JIRA_ISSUE_KEY
                echo 'Requested by: ' + REPORTER
                echo 'Approved by: ' + ASSIGNEE
                echo 'This job will attempt to download the file from the following URL: ' + URL
            }
        }
        stage('wget: Pull software from web into shared drive') {
            steps {
                dir(sharedDrivePath) {
                    bat 'C:\\ProgramData\\chocolatey\\lib\\Wget\\tools\\wget.exe ' + URL
                }
            }
        }
        stage ("Jira: Update Issue Status"){
            steps {
                script {
                    def transitionInput = [transition: [id: '41']]
                    jiraTransitionIssue idOrKey: JIRA_ISSUE_KEY, input: transitionInput, site: 'Jira'
                    jiraAddComment comment: "Jenkins build: " + BUILD_NUMBER + ", complete successfully, tool has been stored in: " + sharedDrivePath, idOrKey: JIRA_ISSUE_KEY, site: 'Jira'
                }
            }
        }
    }

}