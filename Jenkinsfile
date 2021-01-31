String URL = URL_FOR_TOOL

pipeline {
    
    agent {label 'Windows'}

    stages {
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
                dir('C:\\Users\\rootadmin\\SHARED DRIVE') {
                    bat 'C:\\ProgramData\\chocolatey\\lib\\Wget\\tools\\wget.exe ' + URL
                }
            }
        }
        stage ("Jira: Update Issue Status"){
            steps {
                script {
                    def fixedInBuild = [fields: [customfield_10011: 'Build is successful. Find additional comments in Comment Box']]
                    def transitionInput = [transition: [id: '81']]

                    jiraTransitionIssue idOrKey: JIRA_ISSUE_KEY, input: transitionInput, site: 'Jira'
                    jiraEditIssue idOrKey: JIRA_ISSUE_KEY, issue: fixedInBuild, site: 'Jira'
                    
                    messaging = input message: 'Any additional comments?', parameters: [text(defaultValue: '', description: 'Enter any additional comments', name: 'COMMENT')]
                    jiraAddComment comment: messaging, idOrKey: JIRA_ISSUE_KEY, site: 'Jira'
                }
            }
        }
    }

}