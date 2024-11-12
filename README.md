# Fire Business API OpenAPI Spec
## Set up environment 

In order to run the below commands, you must first (assuming wsl usage):

-Install npm

-Install speccy 
```bash
sudo npm install speccy -g
```

 
The API is defined across multiple files using external $refs. To create a single flat YAML file use the following command before commit.
```bash
npm install 
npm run publish
npm run test 
``` 

The publish step runs the resolve refs process twice as some $refs remain after the first run. Not sure why.... 

That tests the OpenAPI and creates the flat file in the dist folder. 

Once you commit to github, the automatic workflows push the change to Readme. 

From the commandline, you can push the changes to Readme as follows:

```bash
# API Ref in v1.0 of Readme: (https://dash.readme.com/project/fire-business-api/v1.0/reference)
rdme openapi ./fire-business-api-v1.yaml  --key=$README_KEY --id=6136360239a7a64894f1c269

# API Ref in v1.0-qa of Readme (https://dash.readme.com/project/fire-business-api/v1.0-qa/reference)
rdme openapi ./fire-business-api-v1.yaml  --key=$README_KEY --id=6422b12bda8f98007a57366d

# Documentation in v1.0 of ReadMe
rdme docs guides --key=$README_KEY --version=v1.0
```