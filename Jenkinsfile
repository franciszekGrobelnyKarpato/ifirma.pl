import groovy.json.JsonSlurperClassic
 
node {
 
	def SF_USERNAME
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
 
            stage('Authorize DevHub') {
                rc = command "${toolbelt}/sfdx force:auth:jwt:grant --instanceurl https://login.salesforce.com --clientid 3MVG9SOw8KERNN08F5bd7rMXDTh2JRdt17Ox8MsHo0q5ZdHp60biTzzdNyc6HvLrVzooMTmzXy9yRnJJkceDJ --username franciszek.grobelny@empathetic-impala-7m2b3p.com --jwtkeyfile 23bb5858-52fc-44c5-939e-f2fa690a6cb1 --setdefaultdevhubusername --setalias HubOrg"
                if (rc != 0) {
                    error 'Salesforce dev hub org authorization failed.'
                }
            }
	}
 
}