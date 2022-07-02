def imageName = 'mlabouardy/movies-parser'
node('workers'){
    stage('Checkout'){
        checkout scm
   }
 
    def imageTest= docker.build("${imageName}-test", "-f Dockerfile.test .")
    stage('Quality Tests'){
        imageTest.inside{
            sh 'golint'
        }
    }
    stage('Unit Tests'){
        imageTest.inside{
            sh 'go test'
        }
    }
    
    stage('Security Tests'){
          imageTest.inside(‘-u root:root’){
             sh 'nancy /go/src/github/mlabouardy/movies-parser/Gopkg.lock'
           }
    }    
    
}
