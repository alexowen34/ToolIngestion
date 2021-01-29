pipeline {
    
    agent {label 'Windows'}

    stages {
        
        stage('Jira Issue ID') {
            steps {
                echo JIRA_ISSUE_KEY
            }
        }

        stage('Pull software from web using wget') {
            steps {
                dir('C:\\Users\\rootadmin\\SHARED DRIVE') {
                    bat 'C:\\ProgramData\\chocolatey\\lib\\Wget\\tools\\wget.exe https://github.com/git-for-windows/git/releases/download/v2.30.0.windows.2/Git-2.30.0.2-64-bit.exe'
                }
            }
        }

    }
}