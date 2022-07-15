def getImages (APPS) {
  return "APPS"
}


// ['copy_app','build_node','database','start_app']

 parameters {
   choice(
         choices: getImages( APPS ),
         name: 'CODE_REPO'
     )

 }

pipeline {
    agent any
    environment {
           CREDS= 'ssh_key'
    //     VDS_TOKEN     = credentials('clo')

    //
     }







    parameters {
      choice(
          choices: ['robo','geeks'],
          name: 'APPS'
      )

      choice(
          choices: ['robo','geeks','odoo'],
          name: 'APPS'
      )
      booleanParam(
        name: 'DOCKER',
        defaultValue: true,
        description: 'Build image'
      )

     //            string(
     //             name: 'CODE_REPO',
     //             defaultValue: 'git@github.com:RoboInterativo/robointerativo_site.git',
     //             description: ''
     //             )
      string(
       name: 'BRANCH',
       defaultValue: 'feature/init',
       description: 'BRANCH'
     )

//copy_app','build_node','database','start_app
     booleanParam(
       name: 'copy_app',
       defaultValue: false,
       description: 'copy_app'
     )
     booleanParam(
       name: 'build_node',
       defaultValue: false,
       description: 'build_node'
     )
     booleanParam(
       name: 'database',
       defaultValue: false,
       description: 'database'
     )
     booleanParam(
       name: 'start_app',
       defaultValue: false,
       description: 'start_app'
     )

     }

      stages() {





        stage('Select STAGES' ) {
        steps {
          script {
                // withCredentials([string(credentialsId: 'vault_secret', variable: 'NEXUS_PASSWORD')]) {
                //     sh "echo \"${NEXUS_PASSWORD}\" > ./.ansible_vault_file"
                // }
            def task_params = []







                withCredentials([sshUserPrivateKey(credentialsId: CREDS,
                                                  keyFileVariable: 'JENKINS_PRIVATE_KEY', passphraseVariable: 'PASSPHRASE',
                                                   usernameVariable: 'USERNAME')]) {

                playbook_name = "playbook1.yml"
                // tags='createnginx'
                ansiblePlaybook extras:   "  -u root    --private-key ${JENKINS_PRIVATE_KEY} -vv --extra-vars  \"  workspace=${WORKSPACE}   ssh_key=${JENKINS_PRIVATE_KEY} inventory_dir=\"inventories/dev/\"\" ",
                installation: 'ansible29',
                inventory: "${WORKSPACE}/inventories/dev/inventory",
                playbook: "${WORKSPACE}/${playbook_name}"


             }






      }
      }










        }





    }

    post {
        success {

            archiveArtifacts allowEmptyArchive: true, artifacts: '${WORKSPACE}/simple-back-front/front/*.zip', fingerprint: true

        }
      }
}
