pipeline {
    agent any

    triggers {
        pollSCM('H/30 * * * *')
    }

    tools {
        maven '3.5.3'
    }

    stages {
        stage('Build & Deploy') {
            steps {
                sh 'mvn clean deploy -U'
                step([$class: 'JacocoPublisher',
                      execPattern: '**/target/*.exec',
                      classPattern: '**/target/classes',
                      sourcePattern: '**/src/main/java',
                      inclusionPattern: '**/trackunit/**/*.class',
                      exclusionPattern: '**/src/test*,**/*Main.*'
                ])
            }
        }
    }
}
