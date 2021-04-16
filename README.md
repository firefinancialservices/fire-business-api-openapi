# Fire Business API OpenAPI Spec

The API is defined across multiple files using external $refs. To create a single flat YAML file use the following tool.
```bash
npm install json-refs --g
json-refs resolve --yaml -w ./fire-business-api-v1.yaml > ./fire-business-api-v1-flat.yaml
``` 
