pipeline {
    agent any
    stages {
        stage('scm') {
            steps {
                git branch: 'master', url:'https://github.com/Raghu-acer/game-of-life.git'        
            }
        }
        stage('build') {
            steps {
                    sh script: 'mvn clean package'
            }
        }
        stage('deploy to jfrog') {
            steps {
                     rtUpload (
                         serverId: 'ARTIFACTORY',
                           spec: '''{
                           "files": [
                                {
                                    "pattern": "gameoflife-web/target/gameoflife.war",
                                    "target": "golrepo"
                            }
                        ]
                    }'''
                )
            }
        }
        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: 'ARTIFACTORY'
                )
            }
        }

    }
}