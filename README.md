# Fire Payments API OpenAPI Spec

## What's this?

This is the OpenAPI spec of the Fire Payments API. You can download this file to use for your own testing and making API calls. 

If you want more detailed information on using the Fire Payments API, you can find guides and references on https://docs.fire.com/docs/getting-started. 


## Using this file 

First, set up your shell. 

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

The publish step runs the resolve refs process twice as some $refs remain after the first run. 

That tests the OpenAPI and creates the flat file in the dist folder. 
