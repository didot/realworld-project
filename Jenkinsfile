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
      recordIssues(enabledForFailure: true, tool: spotBugs(pattern: 'build/reports/spotbugs/*.xml'))
    }
  }
}
