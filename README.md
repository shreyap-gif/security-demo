# security-demo
Simple Java app with OWASP Dependency Check Jenkins pipeline
Assignment A — Security Integration

This repository contains a minimal Maven project and a Jenkinsfile that:
- Builds the project (mvn clean package)
- Runs OWASP Dependency-Check (maven plugin)
- Generates HTML + JSON reports under target/dependency-check-report
- Publishes the HTML report in Jenkins (via HTML Publisher plugin)

How to run locally:
  mvn -B -DskipTests=false clean package
  mvn org.owasp:dependency-check-maven:check

Reports will be in target/dependency-check-report/
