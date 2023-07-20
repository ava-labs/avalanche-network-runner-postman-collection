# Avalanche Network Runner Postman Collection

Postman collection for [the Avalanche Network Runner](https://github.com/ava-labs/avalanche-network-runner).

## Installation

1. Download [Postman](https://www.postman.com)
2. Import the Avalanche Network Runner Postman Collection. Import -> Upload Files -> `Avalanche_Network_Runner.postman_collection.json`
3. Import the Example Avalanche Network Runner Postman Environment. Settings -> Import -> Choose Files -> `Example_Avalanche_Environment.postman_environment.json`
4. Call any Avalanche Network Runner endpoint

## Workflow

Create an Avalanche Subnet with 5 validators running and instance of the Subnet EVM in 60 seconds.

### Begin

Fire up a server. This should be the only command-line step 👏

```json
avalanche-network-runner server \
--log-level debug \
--port=":8080" \
--grpc-gateway-port=":8081"
```

### start

Now, in Postman, paste the following into the POST body for Controls/Start.

```json
{
  "execPath": "{{avalanchego_exec_path}}",
  "numNodes": {{num_modes}},
  "logLevel": "{{log_level}}",
  "pluginDir": "{{avalanchego_plugin_path}}",
  "blockchainSpecs": [
    {
      "vm_name": "{{vm_name}}",
      "genesis": "{{vm_config_path}}"
    }
  ]
}

# check in the response for the subnet id
...
"subnets": {
    "p433wpuXyJiDhyazPYyZMJeaoPSW76CBZ2x7wrVPLgvokotXz": {
...
```

### createsubnets

Paste the following into the POST body for Controls/CreateSubnets.

```json
{
    "participants": [
        "node1",
        "node2",
        "node3",
        "node4",
        "node5"
    ]
}
```

#### createblockchains

Paste the following to Control/CreateBlockchains to create an instance of the Subnet EVM.

```json
{
  "pluginDir": "{{avalanchego_plugin_path}}",
  "blockchainSpecs": [
    {
      "vm_name": "{{vm_name}}",
      "genesis": "{{genesis_path}}", 
      "subnet_id": "{{subnet_id}}"
    }
  ]
}
```

## Contributing

First create a feature branch by branching off of `main`, next make the improvements on your feature branch and lastly create a pull request to merge your work back in to `main`.
