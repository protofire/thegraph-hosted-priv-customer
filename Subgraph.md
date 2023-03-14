# Subgraph

 1. [Credentials](#credentials)
 2. [Endpoints](#endpoints)
 3. [Deployment](#deployment)
 4. [Monitoring](#monitoring)

## [Credentials](#subgraph)

In order to start to use **TheGraph-Hosted** infrastructure you will receive the credentials to be able to authenticate in the endpoints. These include:
 - Username
 - Password
 - Basic Authentication

## [Endpoints](#subgraph)

| Repository                                     | Component      |
| ---------------------------------------------  | -------------- |
| https://ipfs.hosted.protofire-thegraph.com     | IPFS Endpoint  |
| https://index.hosted.protofire-thegraph.com    | Index Endpoint |
| https://query.hosted.protofire-thegraph.com    | Query Endpoint |
| https://grafana.hosted.protofire-thegraph.com  | Grafana        |

## [Deployment](#subgraph)

Once you have received your credentials you'll be able to deploy your subgraph in **TheGraph-Hosted** infrastructure in two ways:

 1. [Manually](#manually)
 2. [Automatically](#automatically)

### [Manually](#deployment)

Please follow the above steps:

 1. Graph Create
 ```bash
 graph create <CUSTOMER_NAME>/<SUBGRAPH_NAME> --version-label <CUSTOMER_NAME>/<SUBGRAPH_NAME> --headers "{\"Authorization\": \"Basic <BASIC_AUTH>\"}" --ipfs https://ipfs.hosted.protofire-thegraph.com --node https://<USERNAME>:<PASSWORD>@index.hosted.protofire-thegraph.com
 
 Created subgraph: <CUSTOMER_NAME>/<SUBGRAPH_NAME>
 ```
 > Note: On graph-cli version 0.42.1 and above you only need to set the _--node_ flag
 ```bash
 graph create <CUSTOMER_NAME>/<SUBGRAPH_NAME> --node https://<USERNAME>:<PASSWORD>@index.hosted.protofire-thegraph.com
 ```

 2. Graph Deploy
 ```bash
 graph deploy <CUSTOMER_NAME>/<SUBGRAPH_NAME> --version-label <CUSTOMER_NAME>/<SUBGRAPH_NAME> --headers "{\"Authorization\": \"Basic <BASIC_AUTH>\"}" --ipfs https://ipfs.hosted.protofire-thegraph.com --node https://<USERNAME>:<PASSWORD>@index.hosted.protofire-thegraph.com
 ```
 
 > **_NOTE_**: Please create and deploy your subgraph following the pattern `<CUSTOMER_NAME>/<SUBGRAPH_NAME>` as this will be used in the customized grafana dashboard.
 
 > **_NOTE_**: Depending on your subgraph code you may also need to run:
 >  
 >  yarn install
 >
 >  yarn codegen
 >
 >  yarn build
 >  

### [Automatically](#deployment)

You can use the workflow template with all the basic steps to deploy your subgraph automatically.

You need to copy the workflow to your subgraph repository and run it manually. The pipeline will ask you the following input data:

 - Username
 - Password
 - Basic_Auth
 - Subgraph_Name

> **_NOTE_**: You can customize the workflow in order to include additional steps based on your subgraph code. You can also modify it in order to be triggered based on a specific event (such as push, tag, label)

## [Monitoring](#subgraph)

Once you have created and deployed your subgraph you can see the ***Indexing Status Overview*** dashboard in grafana.

Using the same credentials (Username & Password) you previously received you can access Grafana portal in the following URL:

https://grafana.hosted.protofire-thegraph.com

You can also check the logs for your subgraph, filtering it by the subgraphID

```bash
curl -u "USERNAME:PASSWORD" -XGET "https://kibana.hosted.protofire-thegraph.com/subgraph-logs/_search" -H 'Content-Type: application/json' -d '{"query": {"match_phrase": {"subgraphId": "SUBGRAPHID"}}}' 2>null | jq .
```

> **_NOTE_**: You can get the ***SUBGRAPHID*** from the _Indexing status_ panel in the grafana dashboard.