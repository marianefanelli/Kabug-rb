pipeline{
    agent{  //antes tava any (qualquer agente)
        docker{  // estou dizendo que quero um agente docker
            image 'ruby'   // que tenha a imagem ruby, ou seja quero um container que tenha ruby instalado
        }
    }
    
    // isso é necessário porque quando o jenkins executa os estágios ele não tem o Ruby instalado, e sem o
    // Ruby instalado nenhum dos comandos irá funcionar, pode fazer este teste acessando o container pelo console e digitando ruby -v de version.
    // o Jenkins não roda mais, o Jenkins cria e sobe um container temporário com a imagem ruby para rodar este job

    stages{
        stage('Build'){
            steps{
                echo 'Building or Resolve Dependencies!'
                sh 'bunddle install' // executa uma shell = sh 'shell'  
            }
        }
        stage('Test'){
            steps{
                echo 'Running regression tests'
            }
        }
        stage('UAT'){
            steps{
                echo 'Wait for User Acceptance'
                input(message: 'Go to Production?', ok: 'Yes')
            }
        }
        stage('Prod'){
            steps{
                echo 'WebApp is ready! :)'
            }
        }
    }
}