pipeline {
  agent { label "jenkins-node" }

  stages {
    stage('Checkout') {
      steps {
        // Git 저장소에서 main 브랜치 체크아웃
        git branch: 'main',
            url: 'https://github.com/journiyoon/source-maven-java-spring-hello-webapp.git'
      }
    }

    stage('Build') {
      steps {
        // Maven 빌드 명령어 실행 (예: mvn clean package)
        sh 'mvn clean package'
      }
    }

    stage('Test') {
      steps {
        // Maven 테스트 명령어 실행 (예: mvn test)
        sh 'mvn test'
      }
    }

    stage('Deploy') {
      steps {
        // WAR 파일을 Tomcat9에 배포
        deploy adapters: [
          tomcat9(
            credentialsId: 'tomcat-manager',
            url: 'http://192.168.56.102:8080'
          )
        ],
        contextPath: null,     // contextPath 지정 필요 시 수정
        war: 'target/hello-world.war'     // 빌드된 WAR 파일 경로 지정 (예: target/myapp.war)
      }
    }
  }
}
