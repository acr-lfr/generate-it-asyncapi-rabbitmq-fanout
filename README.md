# generate-it-asyncapi-rabbitmq

It is expected that this set of templates will be used with the openapi-nodegen-typescript-server templates.

## Example
Within an existing server add a new script (point it to your own entry yml file):
```
    "generate:rabbitmq": "generate-it ../ms_rabbitmq_d/build/rabbitmq_asyncapi_1.0.1.yml -t https://github.com/acrontum/generate-it-asyncapi-rabbitmq.git -o src/events"
```

Read and change the example `.nodegenrc` generated:
```json
{
  "nodegenDir": "generated",
  "nodegenMockDir": "/__mocks__",
  "nodegenType": "server",
  "helpers": {
    "operationNames": {
      "include": ["ms-auth"]
    }
  }
}
```

It is expected that your asyncapi yaml file's channels follow a path like feel eg: https://github.com/acrontum/generate-it/blob/master/test_asyncapi.yml

The `.nodegenrc` file's helpers.operationNames.include|exclude will include or exclude channels from the yaml file based on the 1st segment.

By default, the templates only include an example 1st segment "ms-auth", it is quite unlikely that your yaml file contains this 1st segment so after the 1st generation you will need to update the the .nodegenrc file to include or exclude the correct 1st segments.

As this set of templates follow a very simple fanout pattern, the concept here is that any item published is pushed to all other q's:
