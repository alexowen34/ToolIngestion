String URL = URL_FOR_TOOL
String sharedDrivePath = "C:\\Users\\rootadmin\\SHARED DRIVE"

pipeline {
    
    agent {label 'Windows'}

    stages {
        stage('Jira: Notify Issue Build Started') {
            steps {
                script{
                    jiraAddComment comment: "Jenkins build: " + BUILD_NUMBER + " has started.", idOrKey: JIRA_ISSUE_KEY, site: 'Jira'
                }
            }
        }
        stage('Jira: Issue Information') {
            steps {
                echo 'This job relates to JIRA issue: ' + JIRA_ISSUE_KEY
                echo 'Requested by: ' + REPORTER
                echo 'Approved by: ' + ASSIGNEE
                echo 'This job will attempt to download the file from the following URL: ' + URL
            }
        }
        stage('Wget: Download Software Into Shared Drive') {
            steps {
                dir(sharedDrivePath) {
                    bat 'C:\\ProgramData\\chocolatey\\lib\\Wget\\tools\\wget.exe ' + URL
                }
            }
        }
        stage ("Jira: Update Issue Status") {
            steps {
                script {
                    updateIssueStatus('41', "Jenkins build: " + BUILD_NUMBER + " complete successfully. The tool has been stored in: " + sharedDrivePath)                
                }
            }
        }
    }

    post {
        failure {
            updateIssueStatus(21, 'Jenkins build: ' + BUILD_NUMBER + ' has failed. Please see the "Console Output" in Jenkins for more information.')
        }
    }

}



void updateIssueStatus(String id, String comment) {
    def transitionInput = [transition: [id: id]]
    jiraTransitionIssue idOrKey: JIRA_ISSUE_KEY, input: transitionInput, site: 'Jira'
    jiraAddComment comment: comment, idOrKey: JIRA_ISSUE_KEY, site: 'Jira'
}