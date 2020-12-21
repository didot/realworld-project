#!/usr/bin/groovy

pipeline {
  agent {
    docker {
      image 'adoptopenjdk:8-jdk'
      alwaysPull true
    }
  }

  options {
    timestamps()
    disableConcurrentBuilds()
  }

  stages {
    stage('Build') {
      steps {
        sh './gradlew compileJava compileTestJava'
      }
    }
    stage('Check') {
      steps {
        sh './gradlew check'
      }
    }
    stage('Assemble') {
      steps {
        sh './gradlew assemble'
      }
    }
  }

  post {
    always {
      recordIssues(
              enabledForFailure: true,
              tool: spotBugs(pattern: 'build/reports/spotbugs/*.xml'),
              referenceJobName: "${env.JOB_NAME.substring(0, env.JOB_NAME.lastIndexOf('/') + 1) + 'main'}")
      recordIssues(
              enabledForFailure: true,
              tool: checkstyle(pattern: 'build/reports/checksyle/*.xml'),
              referenceJobName: "${env.JOB_NAME.substring(0, env.JOB_NAME.lastIndexOf('/') + 1) + 'main'}")
    }
  }
}
