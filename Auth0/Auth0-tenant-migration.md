## Auth0 tenant migration

To migrate Auht0 tenant settings from one to another, we have 2 tasks to do:

- Tenant settings migration
- User migration

### Using Auth0 Deploy CLI Tool to migrate settings:

- Install the Deploy CLI Tool:

```
npm i -g auth0-deploy-cli
```

- Configure the Deploy CLI Tool:

Create config-app-cli application as machine to machine app and config.json file:

```

{
  "AUTH0_DOMAIN": "AUTH0_DOMAIN",
  "AUTH0_CLIENT_ID": "AUTH0_CLIENT_ID",
  "AUTH0_CLIENT_SECRET": "AUTH0_CLIENT_SECRET",
  "AUTH0_KEYWORD_REPLACE_MAPPINGS": {
    "AUTH0_TENANT_NAME": "AUTH0_TENANT_NAME"
  },
  "AUTH0_ALLOW_DELETE": false,
  "AUTH0_EXCLUDED_RULES": []
}
```

Export tenant settings

```
a0deploy export --config_file config.json --format yaml --output_folder <your repo directory>
```

Import tenant settings

Create other config file for the tenant will be updated, supposes it's named config2.json  
Run next comand:

```
a0deploy import --config_file config2.json --input_file tenant.yaml
```

<strong>Note that we need to change audience of API to new audience  </strong>
