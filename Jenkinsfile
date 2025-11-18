pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        echo 'Cloning repository...'
        // explicit git clone of the repo you specified
        git url: 'https://github.com/shreyap-gif/security-demo.git', branch: 'main'
      }
    }

    stage('Build') {
      steps {
        echo 'Building with Maven...'
        // runs mvn clean package and includes tests (change -DskipTests if you want)
        sh 'mvn -B -DskipTests=false clean package'
      }
    }

    stage('Security Scan - OWASP Dependency Check') {
      steps {
        echo 'Running OWASP Dependency-Check (Maven plugin)...'
        // this runs the plugin configured in pom.xml and writes reports to target/dependency-check-report
        sh 'mvn org.owasp:dependency-check-maven:check -Ddependency-check.skip=false'
      }
    }

    stage('Publish Reports') {
      steps {
        echo 'Publishing dependency-check HTML report and archiving artifacts...'
        // publish HTML report inside Jenkins (requires HTML Publisher plugin)
        publishHTML([
          reportDir: 'target/dependency-check-report',
          reportFiles: 'dependency-check-report.html',
          reportName: 'OWASP Dependency-Check Report',
          keepAll: true
        ])
        // archive report files (JSON, SARIF, HTML, etc.)
        archiveArtifacts artifacts: 'target/dependency-check-report/**', allowEmptyArchive: true
      }
    }
  }

  post {
    always {
      echo "Pipeline finished — check build artifacts and OWASP Dependency-Check Report link in the job page."
    }
  }
}
