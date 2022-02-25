pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'build done'
        sh './gradlew clean build'
      }
    }

    stage('upload') {
      steps {
        echo 'upload done'
         sh 'aws s3 cp build/libs/application.war s3://springboot-cicd-gydnjs/application.war --region us-east-2'
      }
    }

    stage('deploy') {
      steps {
        echo 'deploy done'
        sh 'aws elasticbeanstalk create-application-version --region us-east-2 --application-name springboot-cicd-gydnjs --version-label ${BUILD_TAG} --source-bundle S3Bucket="springboot-cicd-gydnjs",S3Key="application.war"' 
        sh 'aws elasticbeanstalk update-environment --region us-east-2 --environment-name Springbootcicdgydnjs-env-1 --version-label ${BUILD_TAG}' 
      }
    }

  }
}