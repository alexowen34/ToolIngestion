String URL = URL_FOR_TOOL
String sharedDrivePath = "C:\\Users\\rootadmin\\SHARED DRIVE"

pipeline {
    
    agent {label 'Windows'}

    stages {
        stage('Jira: Notify Issue Build Started') {
            steps {
                script{
                    jiraAddComment comment: "Jenkins build: " + BUILD_NUMBER + " has started: " + BUILD_URL, idOrKey: JIRA_ISSUE_KEY, site: 'Jira'
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
    }

    post {
        success {
            updateIssueStatus('DONE', "Jenkins build: " + BUILD_NUMBER + " complete successfully. The tool has been stored in: " + sharedDrivePath)
        }
        failure {
            updateIssueStatus('BLOCKED', 'Jenkins build: ' + BUILD_NUMBER + ' has failed. Please see the "Console Output" in Jenkins for more information.')
        }
    }

}

void updateIssueStatus(String transition, String comment) {
    
    String transitionID = null
    switch(transition) {
        case 'DONE': transitionID = '41'
        break
        case 'BLOCKED': transitionID = '21'
        break
    }

    def transitionInput = [transition: [id: transitionID]]
    jiraTransitionIssue idOrKey: JIRA_ISSUE_KEY, input: transitionInput, site: 'Jira'
    jiraAddComment comment: comment, idOrKey: JIRA_ISSUE_KEY, site: 'Jira'

}