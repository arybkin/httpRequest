pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                withCredentials([string(credentialsId: 'uuid', variable: 'UUID')]) {
                script {
                    println "Hello world"
                    def rp_url = "https://beta.demo.reportportal.io/api/v1/arybkin_personal"
                    println "Check zip functionality"
                    println "Check file existance"
                    println (fileExists("junit.zip"))
                    zip zipFile: "junit.zip", archive: false, glob: "*.xml"
                    println "Check file existance"
                    println (fileExists("junit.zip"))

                    println "Send request"
                    try{
                    def http_request = httpRequest httpMode: 'POST', url: "${rp_url}/launch/import",
                            acceptType: 'APPLICATION_JSON',
                            //contentType: 'APPLICATION_ZIP',
                            customHeaders:[[name:'Authorization', value:"bearer 7633547b-06d6-4399-a1f7-aecd0be8c814"]],
                            uploadFile: "junit.zip",  multipartName: "junit.zip", timeout: 900
                     } catch(Exception ex){
                        println ex
                     }
                    def http_request = httpRequest httpMode: 'POST', url: "${rp_url}/launch/import",
                            acceptType: 'APPLICATION_JSON',
                            //contentType: 'APPLICATION_ZIP',
                            customHeaders:[[name:'Authorization', value:"bearer ${UUID}"]],
                            uploadFile: "junit.zip",  multipartName: "junit.zip", timeout: 900
                }
              }
            }
        }
    }
}