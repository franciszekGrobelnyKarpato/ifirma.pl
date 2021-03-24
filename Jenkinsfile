import groovy.json.JsonSlurperClassic
 
node {
 
	def HUB_ORG=env.HUB_ORG_DH
	def SFDC_HOST=env.SFDC_HOST_DH
	def JWT_KEY_CRED_ID='ba7b34c5-377a-494a-a869-6c92823f942b'
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
			println "${jwt_key_file}"
            stage('Authorize DevHub') {
                rc = command "${toolbelt}/sfdx auth:jwt:grant --instanceurl ${SFDC_HOST} --clientid ${CONNECTED_APP_CONSUMER_KEY} --username ${HUB_ORG} --jwtkeyfile ${jwt_key_file}"
                if (rc != 0) {
                    error 'Salesforce dev hub org authorization failed.'
                }
            }
	}
 
}