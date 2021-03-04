pipeline {
    agent any

    triggers {
        cron('0 1 * * *')
    }

    stages {
        stage ('Build') {
            when {
                expression {
                    // When last build has failed
                    !hudson.model.Result.SUCCESS.equals(currentBuild.rawBuild.getPreviousBuild()?.getResult()) == true
                }
            }

            steps {
                sh "./myjob.sh"
            }

            post {
                failure {
                    // If the current job has failed, trigger it without
                    // waiting.
                    build job: "${JOB_NAME}", wait: false
                }
            }
        }
    }
}
