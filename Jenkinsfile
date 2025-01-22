pipeline {
    agent any
    tools {
        maven 'jenkins_maven'
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
                // 部署到服务器（示例：复制 JAR 文件到目标服务器）
                sh 'scp target/sample-spring-1.0-SNAPSHOT.jar user@your-server:/path/to/deploy'
                sh 'ssh user@your-server "nohup java -jar /path/to/deploy/sample-spring-1.0-SNAPSHOT.jar &"'
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