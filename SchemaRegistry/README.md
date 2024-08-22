# Schema Registry

Deploy via `kubectl apply -f ./SchemaRegistry/schemaregistry.yaml -n confluent`

## Schema Management

* [Manage Schemas for Confluent Platform Using Confluent for Kubernetes](https://docs.confluent.io/operator/current/co-manage-schemas.html)
* [Data Contracts for Schema Registry on Confluent Platform](https://docs.confluent.io/platform/current/schema-registry/fundamentals/data-contracts.html)

We want to deploy a schema with Data Contracts as a CR.
Therefore, we add to the config map

```yaml
data:
 schema: |
  {
    "type": "record",
    "name": "SensorData",
    "namespace": "com.pneffExample",
    "fields": [
      {"name": "sensorId", "type": "string"},
      {"name": "type", "type": "string"},
      {"name": "value", "type": "float"},
      {"name": "unit", "type": "string"},
      {"name": "timestamp","type": "string"}
      ]
   }
  properties: {"owner": "Patrick Neff","email": "pneff@confluent.io"}
```


```shell
kubectl apply -f ./SchemaRegistry/schemaConfig.yaml -n confluent
kubectl apply -f ./SchemaRegistry/schema.yaml -n confluent
```

> [!NOTE]
> Unfortunately, it is not possible as of today (August 2024)
> We receive the following error in the CFK operator logs:
> ```
> {"level":"ERROR","time":"2024-08-22T12:18:15.568Z","name":"schema","caller":"log/log.go:35","msg":"error creating schema","name":"sensor-value" [...]
> [...] properties: {\"owner\": \"Patrick Neff\",\"email\": \"pneff@confluent.io\"}\n} with refs [] of type AVRO, details: dangling content after end of schema: properties: {\"owner\": \"Patrick Neff\",\"email\": \"pneff@confluent.io\"} (42201)"}
> ```
