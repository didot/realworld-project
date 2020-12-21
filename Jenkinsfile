#!/usr/bin/groovy

pipeline {
  agent {
    docker {
      image 'adoptopenjdk:8-jdk'
      alwaysPull true
    }
  }

  stages {
    stage('Build') {
      steps {
        sh './gradlew test'
        sh './gradlew assemble'
      }
    }
  }
}
