node{

    stage('SCM Checkout')
    {
        git url: 'https://github.com/s-naidu/online-shop-master.git'
    }
    
    stage('Run Docker Compose File')
    {
        sh 'sudo docker-compose build'
        sh 'sudo docker-compose up -d'
    }
  stage('PUSH image to Docker Hub')
    {
            //docker.withRegistry( 'https://registry.hub.docker.com', 'DockerHubPassword' ) {
             
             sh 'sudo docker login -u "sudarshandn" -p "DockerHub@2016" docker.io'
             sh 'sudo docker tag ecommerce_demo_site_web sudarshandn/ecommerce_01'
             sh 'sudo docker push sudarshandn/ecommerce_01:latest'
           
          
    }
     stage('Deploying App to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deploymentservice.yml", kubeconfigId: "kubernetes")
        }
      }
    }
}
