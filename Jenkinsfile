String url = URL_FOR_TOOL

pipeline {
    agent {label 'Windows'}

    stages {
        stage('Jira Issue Infomation') {
            steps {
                echo 'This job relates to JIRA issue: ' + JIRA_ISSUE_KEY
                echo 'Requested by '
                echo 'This job will attempt to download the file from the following URL: ' + url
            }
        }
        stage('Pull software from web into shared drive') {
            steps {
                dir('C:\\Users\\rootadmin\\SHARED DRIVE') {
                    bat 'C:\\ProgramData\\chocolatey\\lib\\Wget\\tools\\wget.exe ' + url
                }
            }
        }
    }
}