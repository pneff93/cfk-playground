# Connect


## Plugins
* [Configure Kafka Connect for Confluent Platform Using Confluent for Kubernetes](https://docs.confluent.io/operator/current/co-configure-connect.html#install-connector-plugin).

In CFK, we can add Connector plugins directly via Confluent Hub or by providing a custom URL

A Confluent Hub example with MongoDB Source and Sink Connector. You find the information also in the connector manifest.
```yaml
- name: kafka-connect-mongodb
  owner: mongodb
  version: 1.12.0
```

A custom URL example with the Salesforce connector:
* We add the zip to the plugins folder.
* We provide the archive path
    * Test: If you paste the path to your browser the .zip should automatically be downloaded
* Create the checksum via `sha512sum /Users/pneff/Repos/cfk-playground/Connect/plugin/confluentinc-kafka-connect-salesforce-2.0.20.zip`

```yaml
- name: kafka-connect-salesforce
  archivePath: https://raw.githubusercontent.com/pneff93/cfk-aks/main/plugins/confluentinc-kafka-connect-salesforce-2.0.20.zip
  checksum: 1f4e448a6f1d3a6e3280de148562218dd970b2e9d4b2669b8775db08a5bd201a078186bd6aab3c217c8dd30c6c7d6c59721382aac3c18dfb9f91d400d49f6a94
```

* Deploy the Connect cluster via `kubectl apply -f .Connect/connect.yaml -n confluent`
* Port forward connect and check if plugins are existing
`curl -s -XGET http://localhost:8083/connector-plugins | jq '.[].class'`