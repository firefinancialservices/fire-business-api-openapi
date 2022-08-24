# Fire Business API OpenAPI Spec

The API is defined across multiple files using external $refs. To create a single flat YAML file use the following command before commit.
```bash
npm install 
npm run publish
npm run test 
``` 
That tests the OpenAPI and creates the flat file in the dist folder. 
