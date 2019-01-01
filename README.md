# Nexmo-Stitch-Msg-JS
This repo will create a basic online chat app with Node.JS and Nexmo API

## Get ready:
0.1 Register a Nexmo account
0.2 Install Node.JS on local machine
0.3 Install and initialize Nexmo CLI
$ npm install -g nexmo-cli@beta
$ nexmo setup <your_api_key> <your_api_secret>
0.4 Create a project foler and work from there
0.5 Add the Nexmo Stitch SDK
$ npm install nexmo-stitch
0.6 Install and run http-server
$ sudo npm install http-server -g
$ http-server
Ctrl + C to terminate the server from running

## Stub out:
1.1 - Create a Nexmo Application
$ nexmo app:create "Stitch SMS JS" https://example.com/answer https://example.com/event --type=rtc --keyfile=private.key
db36abf2-edf9-4a73-9dbd-1092fe0b632f

1.2 - Create a Conversation
$ nexmo conversation:create display_name="Stitch SMS JS"
CON-a462fc56-cab4-455d-938e-bfb5ea121b3b

1.3 - Create a User
$  nexmo user:create name="Alice"
USR-1c8efc3e-849e-44f5-9363-8a2b492d9566
$ nexmo user:create name="Bill"
USR-edf7f9fa-d855-43d1-82cb-4bb0a54253d8

1.4 - Add the User to the Conversation
$ nexmo member:add CON-a462fc56-cab4-455d-938e-bfb5ea121b3b action=join channel='{"type":"app"}' user_id=USR-1c8efc3e-849e-44f5-9363-8a2b492d9566
MEM-eb994b87-3199-4e2c-9330-a538073be353
$ nexmo member:list CON-a462fc56-cab4-455d-938e-bfb5ea121b3b -v
$ nexmo member:add CON-a462fc56-cab4-455d-938e-bfb5ea121b3b action=join channel='{"type":"app"}' user_id=USR-edf7f9fa-d855-43d1-82cb-4bb0a54253d8
MEM-acf4330d-9195-46b0-a038-cab698ca507b
$ nexmo member:list CON-a462fc56-cab4-455d-938e-bfb5ea121b3b -v

1.5 Generate a User JWT
$ USER_JWT="$(nexmo jwt:generate ./private.key sub=Alice exp=$(($(date +%s)+86400)) acl='{"paths":{"/v1/users/**":{},"/v1/conversations/**":{},"/v1/sessions/**":{},"/v1/devices/**":{},"/v1/image/**":{},"/v3/media/**":{},"/v1/applications/**":{},"/v1/push/**":{},"/v1/knocking/**":{}}}' application_id=db36abf2-edf9-4a73-9dbd-1092fe0b632f)"
$ echo $USER_JWT

1.6 Create a static index.html file
https://github.com/Nexmo/stitch-js-quickstart/blob/master/simple-conversation/index.html
Replace the consts of USER_JWT and YOUR_CONVERSATION_ID

Test:
2.1 Open two browser windows, enable their developer tools, and keep consoles open
2.2 Navigate to http://127.0.0.1:8080 on the two browser, log in with Alice and send some messages
2.3 Confirm the input from two browswers is updated

Notice:
1. Console log is visiable in the browser's developer tool, but not in the terminal
2. The user name should be exactly the same in Create a User and Generate a Uer JWT
3. Following files and folders are gitignored in this repo but should be there in yours
* .nexmo-app
* .gitignore
* node_modules/
* private.key
4. User Bill is created for testing the Nexmo CLI but never used for log in
5. Just use http-server with its default port 8080 and current home location
6. Sweet of this repo is all in the omitted script code, go there for fun
