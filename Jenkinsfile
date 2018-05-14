#!/usr/bin/env groovy

pipeline {

    agent {
        docker {
            image 'node'
            args '-u root'
        }
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                sh 'npm test'
            }
        }
        stage('Deploy') {
      wrap([$class: 'KubectlBuildWrapper', caCertificate: '''-----BEGIN CERTIFICATE-----
MIICyDCCAbCgAwIBAgIBADANBgkqhkiG9w0BAQsFADAVMRMwEQYDVQQDEwprdWJl
cm5ldGVzMB4XDTE4MDUxMzIwNTIwNloXDTI4MDUxMDIwNTIwNlowFTETMBEGA1UE
AxMKa3ViZXJuZXRlczCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBALXt
Y3530GwD5VBPjQ5WoKv0s6XUxDBp9Bwph4J7nVzNnSdL2v27lFDQedjCOeqAAR8S
DP/Ys+A62nJR/0DdmcInvAU5xV7hCNJHoR5JkjZD2CKy8ycuDWkF7A69xBQ4PUdu
1eioPPqWV1NKXptDsRYFFrkm0DI6geRuqWGASC+bpm2ca3LgwKdSaPYEG9nMMe8C
UPAnYcDo/Eys2Z5qyT+5b06JDKNGoDfTRgXznE+qDcKQLKfW4H54RGOH75fADBue
WyB5FgLRNp0BaJhtpmQXA98kiPccdPXO50aZ5OWU0gqxJCYXvS86y1Z4MwevG0cj
fCZChg1PnYR8WyXN9BkCAwEAAaMjMCEwDgYDVR0PAQH/BAQDAgKkMA8GA1UdEwEB
/wQFMAMBAf8wDQYJKoZIhvcNAQELBQADggEBAFe07BUzv5EHqygCExP8Pq+SA/Xa
33ykpocIUbSwx59oW2UvzuBPbAOrehQbRTBH5WqpRbCFvz5lIZ32ebuQprMy9vjd
sWi4wWo1AWM7XQamCLPicrphDRMDDuZZfzUJRnUHhn6otLVNBOSt9kvTMx5kZwQX
tsoK8IIl7+3gVXVtSshz2mlTTzps+IaxEv5wJ7afKFjUEsWm78RASCQ7VbtKwOe5
XapmPeJUA6jzWAu046/QzYrj49hC2RAx58QqV7pMKVmXw6bsT51+lW5+d0+ph32s
ydJHgvqMjgkt8jklxx18l4fBMI7TGAcSj5x7myZ/tn2d8xfq5jYQM7s01MM=
-----END CERTIFICATE-----''', credentialsId: 'kube-dev', serverUrl: 'https://10.136.1.81:6443']) {
  sh 'kubectl set image deployment $deploymentName $deploymentName=$imageName:$TAG --record'
       }
     }
  }
}
