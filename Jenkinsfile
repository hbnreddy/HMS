currentBuild.displayName="HMSt-#"+currentBuild.number
pipeline{
	agent any
   triggers {
		     pollSCM ignorePostCommitHooks: true, scmpoll_spec: '* * * * *'  
	     }
       stages{
            stage("Checkout-SCM"){
                steps{
                        
			checkout([$class: 'GitSCM', 
					branches: [[name: '*/master']], 
					doGenerateSubmoduleConfigurations: false, 
					extensions: [],
					submoduleCfg: [], 
					userRemoteConfigs: [[credentialsId: 'gitHUB_credentials', 
					url: 'https://github.com/hbnreddy/Hospital-Management-System.git']]])  
                }
            }
            stage("Build"){
                steps{
                    sh 'mvn package'
                }
            } 
            stage("ArchiveArtifacts"){
                steps{
                    archiveArtifacts '**/*.war'
                }
            }
	       stage("DeploytoTomcat"){
                steps{
                   sh 'scp /var/lib/jenkins/workspace/HMS-Project/target/HMS-3.4.war root@172.31.31.172:/root/tomcat8/webapps'
                }
            }
         }
      }
