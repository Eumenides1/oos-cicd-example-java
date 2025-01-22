pipeline {
    agent any

    environment {
        // 定义环境变量
        JAVA_HOME = '/path/to/java'
        MAVEN_HOME = '/path/to/maven'
        PATH = "${MAVEN_HOME}/bin:${JAVA_HOME}/bin:${PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                // 从 Git 仓库拉取代码
                git branch: 'main', url: 'https://github.com/your-repo/your-spring-boot-app.git'
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
                sh 'scp target/your-spring-boot-app.jar user@your-server:/path/to/deploy'
                sh 'ssh user@your-server "nohup java -jar /path/to/deploy/your-spring-boot-app.jar &"'
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