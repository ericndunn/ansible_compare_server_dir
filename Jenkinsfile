pipeline {
    agent { label 'MASTER' }
        parameters {
            string(defaultValue: "MY_USERID", description: 'User ID', name: 'MY_USERID')
            string(defaultValue: "test_inventory", description: 'Ansible Host file', name: 'INV_FILE')
            string(defaultValue: "AA_PROD_WAS", description: 'Ansible Host Group', name: 'INV_GRP')
            string(defaultValue: "va10plvwbs443", description: 'Master Source Server to compare FROM', name: 'MASTER_SERVER')  
        }
    stages {
        //stage('Cleanup Jenkins Job Workspace'){
            //steps {
                //step([$class: 'WsCleanup'])
            //}
        //}       
        stage('Run Ansible Deploy operation'){        
            steps {            
            wrap([$class: 'AnsiColorBuildWrapper', colorMapName: "xterm"]) {
                    echo 'Validate Access'
                    ansiblePlaybook credentialsId: 'PASSKEY_TO_SERVER',
                    installation: 'ansible', 
                        inventory: '/Users/${MY_USERID}/${INV_FILE}',
                    limit: '${INV_GRP}',
                        playbook: '${WORKSPACE}/compare_server.yml',
                    colorized: false
                }
            }
        }
        stage('Demo Performance'){
            steps {
                echo 'ansible-playbook compare_server.yml -i ~/test_inventory --extra-vars "master=va10plvwbs443 my_userid=ag19884"'
            }
        }

    }
}
