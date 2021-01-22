pipeline{
    agent{  //antes tava any (qualquer agente)
        docker{  // estou dizendo que quero um agente docker
            image 'qaninja/rubywd'   // que tenha a imagem ruby, ou seja quero um container que tenha ruby instalado
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
                sh 'rm -f Gemfile.lock' //remove a file gemfile.lock que estava associada a outra imagem q estavamos, como mudamos a imagem removemos essa gemfile.lock para que o jenkins crie outra para esta imagem
                sh 'bundle exec cucumber -p ci' // para executar com o parâmetro CI em Headless, Jenkins tem q ser em headless
                // no windows pode por só cucumber -p ci, mas como o docker é um ambiente linux, nosso container é linux então precisa por o bundle exec na frente
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