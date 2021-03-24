import groovy.json.JsonSlurperClassic
 
node {
 
	def SF_USERNAME
	def HUB_ORG=env.HUB_ORG_DH
	def SFDC_HOST=env.SFDC_HOST_DH
	def JWT_KEY_CRED_ID=env.JWT_KEY_CRED_ID_DH
	def CONNECTED_APP_CONSUMER_KEY=env.CONNECTED_APP_CONSUMER_KEY_DH
 
    def toolbelt = tool 'toolbelt'
	
	println 'env variables'
	println CONNECTED_APP_CONSUMER_KEY
	println JWT_KEY_CRED_ID
	println SFDC_HOST
	println HUB_ORG
	
	stage('checkout source') {
        checkout scm
    }
	withCredentials([file(credentialsId: JWT_KEY_CRED_ID, variable: 'jwt_key_file')]) {
 
            // ------------------------------------------------------------------------
            // Authorize the Dev Hub org with JWT key and give it an alias.
            // ------------------------------------------------------------------------
 
            stage('Authorize DevHub') {
                rc = command "${toolbelt}/sfdx auth:jwt:grant --instanceurl ${SFDC_HOST} --clientid ${CONNECTED_APP_CONSUMER_KEY} --username ${SF_USERNAME} --jwtkeyfile ${server_key_file} --setdefaultdevhubusername --setalias HubOrg"
                if (rc != 0) {
                    error 'Salesforce dev hub org authorization failed.'
                }
            }
	}
 
}