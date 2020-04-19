# generate-it-asyncapi-rabbitmq

A set of templates to automate RabbitMQ connections and queues with an async api file.

## Sending data to the exchange
Each channel operation id emitted to the nodejs event bus from the [nodegen typescript server](https://github.com/acrontum/openapi-nodegen-typescript-server/blob/master/src/utils/eventBus.ts). When the event [is heard](https://github.com/acrontum/generate-it-asyncapi-rabbitmq/blob/master/generated/channels.ts.njk#L23) the payload is passed to the exchange and the opId as the routing key.

## Receiving data from RabbitMQ
Data consumed from the queue you set-up with will be passed to the domain named by the operationId. For every operationId there is a domain file. For each domain function the payload type passed calculated by the schema defined in the AsyncApi file.

## nodegenrc
The definition of the nodegen file for the ids is as follows:
```json
  asyncApi: {
    includedOperationIds?: string[];
    excludedOperationIds?: string[];
    stubChannelType: string[];
  }; 
```

#### stubChannelType
By default, this is set to subscribe as the domain files will perform the business logic of parsing the data from the rabbitmq payload

#### includedOperationIds
An array of operationIds to include. If this is set, only the operation ids included in this array will be used from the asyncapi file

#### includedOperationIds
An array of operationIds to exclude. If this is set, only the operation ids in this array will be not used from the asyncapi file
