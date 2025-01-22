pipeline {
    agent any
    tools {
        maven 'jenkins_maven'
    }
    environment {
        GIT_PATH = '/usr/bin/git' // 指定 Git 的路径
    }
    stages {
        stage('Checkout') {
            steps {
                // 从 Git 仓库拉取代码
                git branch: 'main', url: 'https://github.com/Eumenides1/oos-cicd-example-java.git'
            }
        }

        stage('Build') {
            steps {
                // 使用 Maven 构建项目
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                // 运行单元测试
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                sshPublisher(
                    publishers: [
                        sshPublisherDesc(
                            configName: 'deploy-server',  // 与 Jenkins 中配置的名称一致
                            transfers: [
                                sshTransfer(
                                    sourceFiles: 'target/sample-spring-1.0-SNAPSHOT.jar',  // 要传输的文件
                                    remoteDirectory: '',  // 目标路径
                                    execCommand: '''
                                        cd /opt/app
                                        nohup java -jar sample-spring-1.0-SNAPSHOT.jar > app.log 2>&1 &
                                    '''  // 运行 JAR 文件
                                )
                            ]
                        )
                    ]
                )
            }
        }
    }

    post {
        success {
            // 构建成功后的操作
            echo 'Build and deployment successful!'
        }
        failure {
            // 构建失败后的操作
            echo 'Build or deployment failed!'
        }
    }
}