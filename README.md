1. Resource Group
	Resource Group Name: cms

2. SQL Database
	DB name: cms
	Server: cms.database.windows.net
	DB region: us-east
	Admin login: cmsadmin
	Admin password: CMS4dmin
	Resource group: cms
	DB workload env: Development
	DB compute + storage: DTU - Basic
	Press the "Next: Networking" button, then select "Public Endpoint", and set both of the Firewall rules that appear to "Yes".
	Set everything else to default
	Run SQL queries in sql_scripts/ directory after completion, starting from the users table. Don't forget to take screenshots.


3. Storage Account
	Resource group: cms
	Storage account name: images1361
	Advanced - Allow enabling anonymous access on individual containers: Enable
	Advanced - Access tier: Cool
	Network access: Enable public access from all networks (the default)
	Create container named "images". Set its access level to Container.
	From Security + networking > Access keys:
	Blob Storage key: kfy3XCCGzq8NQ//XOzmOz3w/IN/xQsChJLwzIipiU+x2PFpPczPAnd1TL16b7s1as1ybCllbtXRN+AStuN8hmw==

4. Microsoft Entra ID
5. App Registration
	Name: cmsEntraID
	Who can use? "Accounts in any organizational directory (Any Microsoft Entra ID tenant - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)"
6. Secret Creation
	Secret description: project 5
	Secret Key: eb301be6-aa99-47f0-aee1-c7e8c55b626e
	Client Secret: z6.8Q~4ntal_xyYD17dw9ipjvu8hhU-4TMznddkQ
	Application (client) ID: 21a4f621-c022-45a1-80cb-12ee3e51e049
7. OPTION 2: Web App (easier)
	Name: udacitycms1.azurewebsites.net
	Runtime stack: Python 3.10
	
	Pricing Plan: Free F1
	If you are getting a "Validation failed for a resource" error, pick a different region.
	
	After creation:
	Settings -> Environment variables - Add the following variables (sample values are included, replace them with your values):
	BLOB_ACCOUNT: images1361
	BLOB_CONTAINER: images
	BLOB_STORAGE_KEY: kfy3XCCGzq8NQ//XOzmOz3w/IN/xQsChJLwzIipiU+x2PFpPczPAnd1TL16b7s1as1ybCllbtXRN+AStuN8hmw==
	SQL_SERVER: cms.database.windows.net
	SQL_DATABASE: cms
	SQL_USER_NAME: cmsadmin
	SQL_PASSWORD: CMS4dmin
	CLIENT_SECRET: z6.8Q~4ntal_xyYD17dw9ipjvu8hhU-4TMznddkQ
	SECRET_KEY: eb301be6-aa99-47f0-aee1-c7e8c55b626e
	CLIENT_ID: 21a4f621-c022-45a1-80cb-12ee3e51e049
	Deployment Center
	Source: GitHub
	Pick the repo that contains the starter files.
8. Setting up OAuth2
	At this point, your application should already be running. You should already be able to log in with username admin and password pass and you can create new posts or update existing ones.
	The next part is getting the OAuth2 login to work.
	Go to Microsoft Entra ID > App Registrations, click on the App Registration created earlier, and then pick Authentication from the left sidebar.
9. Microsoft Entra ID - Authentication - Add a Platform - Web
	
	Redirect URIs: https://[IP ADDRESS FROM VM or WEB APP ADDRESS]/getAToken
	logout URL: https://[IP ADDRESS FROM VM or WEB APP ADDRESS]/login