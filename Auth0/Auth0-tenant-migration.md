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

<strong>Note that we need to change audience of API to new audience </strong>

### Import users data

Data format

The provided file from Auth0 is in NDJSON format (New line delimited JSON 5). If you open it with a text editor you will see one user object per line. E.g.:

```
{ ... one user... }
{ ... another user ... }
{ ... and so on ... }
```

Each user object will have some properties. Most of them are self-explanatory, but it’s good to clarify a couple of them related to the user id. A sample single user would look like this (formatted for better readability):

```
{
"\_id":{"$oid":"5dea9f9c82dd7c0e76e4ec93"},
  "email_verified":false,
  "email":"nico9090@nico.com",
  "passwordHash":"$2b$10$.qHPp/srqo1NAAAAAvlkmOdqAbH2Rg0qPv2Txj3ZwXfjJnewSjc4m",
"password_set_date":{"$date":"2019-12-06T18:36:12.412Z"},
"tenant":"nico-sabena",
"connection":"Username-Password-Authentication",
"\_tmp_is_unique":true,
"alt_id":"euclid"
}
```

Every user will have an <b>\_id </b> field, while the <b> alt_id </b> is optional. You’ll see an <b>alt_id </b> for users coming from a custom DB (where the custom DB script provides the user id) or when you create regular DB connection users with the Management API v2 and you provide your own user id.

If want to import the original user ids, you’ll need to provide a user_id field with the value found in the exported user’s alt_id (if present), or the $oid value.

the sample user above:

```
[
  {
    "user_id":"euclid", // if you want to keep the same user id
    "email_verified":false,
    "email":"nico9090@nico.com",
    "password_hash":"$2b$10$.qHPp/srqo1NAAAAAvlkmOdqAbH2Rg0qPv2Txj3ZwXfjJnewSjc4m"
  },
  {...} // other entries in the array, if you have more users
]
```

### Using jq to convert data

```
cat input.json | jq '{user_id: (if has("alt_id") then .alt_id else .\_id."$oid" end), email, username, email_verified, password_hash: .passwordHash}' | jq -s 'del(.[][] | nulls)' > output.json
```

After cover data, just using Import/Export Auth0 extention to import/export data
