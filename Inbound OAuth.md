# Inbound OAuth with Bruno

## Outline

1. Configure OAuth registry in ServiceNow
2. Configure request in Bruno
3. Get Access Token in Bruno

## ServiceNow

1. Navigate to System OAuth > Application Registry, and click "New"
2. Select "Create an OAuth API endpoint for external clients"
3. Enter a **Name**, and change **Default Grant type** to _Authorization Code_
4. Make a note of the Client ID and Client Secret

## Bruno

Pre-requiste: Bruno Workspace and Collection
1. Create a new request
   + Method: GET
   + URL: `{{base_url}}/api/now/table/sys_user?sys_id=javascript:gs.getUserID()`
     
 * **Auth tab**
   + Grant Type: Authorization Code
   + Callback URL: https://oauth.usebruno.com/callback
   + Authorization URL: `https://{{instance_name}}.service-now.com/oauth_auth.do`
   + Access Token URL: `https://{{instance_name}}.service-now.com/oauth_token.do`
   + Client ID: `{{client_id}}`
   + Client Secret: `{{client_secret}}`
   + Scope: useraccount
   + State: 12345
   + Refresh Token URL: `https://{{instance_name}}.service-now.com/oauth_auth.do`
2. Create a new environment
   + base_url
   + instance_name
   + client_id
   + client_secret

3. Get Access Token
   + Click "Get Access Token" (bottom of Auth tab)
   + Log in to ServiceNow as your desired user
   + (if this does not work, try setting "Use system browser for OAuth" to true)
  

  
