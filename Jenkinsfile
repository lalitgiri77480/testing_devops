pipeline {
environment {
JobName = "currentBuild.fullDisplayName"
recipients = "lalitgiri396@gmail.com"
usermail = "admin@admin.com"
git_branch = "Prod"
git_url = "https://github.com/lalitgiri77480/testing_devops.git"
}

agent { label 'deploy' }
stages {

stage('Pull Source') {
steps {
git credentialsId: 'a95f7f45-1d92-4cf6-8c19-c230d2b7e7d6', branch: "${git_branch}", url: "${git_url}"
}
}

stage('Email Approval')
{
steps {
script {
def userAborted = false
emailext body: ''' Please go to console output of ${BUILD_URL} input to approve or reject <br> ''',
mimeType: 'text/html',
subject: "[Jenkins]${JobName} Build Approval Request",
from: "${usermail}",
to: "${recipients}"
try {
userInput = input submitter: 'vagrant' , message: 'Do you approve?'
} catch (org.jenkinsci.plugins.workflow.steps.FlowInterruptedException e) {
cause = e.causes.get(0)
echo "Aborted by " + cause.getUser().toString()
userAborted = true
echo "SYSTEM aborted , Aborting..."
}
if (userAborted) {
currentBuild.result = 'ABORTED'
}
else {
echo "Testing"
}
}
}
}

stage('Deploy')
{
steps {
sh "echo Stage deployment"
}
}

}
}
