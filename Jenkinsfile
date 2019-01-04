node('RS_slave_227') {
    
        step([$class: 'WsCleanup'])
       
        stage("Removing existing container") {
        sh '''
                echo 'Multiline'
                echo 'Example'
                if [ "$(docker ps -aq -f name=checklistSample)" ]; then
                docker rm -f checklistSample
                fi
             '''
        }
        
        stage("Main build") {

           sh 'git clone -b blr-dev ssh://tfsemea1.ta.philips.com:22/tfs/TPC_Region13/PARAM/_git/checklist'
		       sh 'docker run --name checklistSample -d -v $WORKSPACE/checklist:/home/ubuntu/ -it pbas/react'	
        }

		    stage("Building App"){
		
		       echo 'App Build' 
		       sh 'docker exec checklistSample bash -l /home/ubuntu/circle-package-application.sh'
		}
    
}
