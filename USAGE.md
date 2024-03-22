# Subgraph

 1. [Credentials](#credentials)
 2. [Endpoints](#endpoints)
 3. [Deployment](#deployment)
 4. [Monitoring](#monitoring)

## Credentials

In order to start using **The Graph - Hosted** infrastructure you will need the appropiate credentiales to authenticate against the required endpoints.

You should've received by email:

- USERNAME
- PASSWORD
- BASIC AUTH

## Endpoints

|  Component |                           URL                          |
|:----------:|:------------------------------------------------------:|
| Index Node | https://index-${USERNAME}.protofire-thegraph.com       |
| Query Node | https://query-${USERNAME}.protofire-thegraph.com       |
| Grafana    | https://grafana-hosted.protofire-thegraph.com          |
| IPFS       | https://ipfs-hosted.protofire-thegraph.com             |

## Deployment

Once you have proper credentials you'll two options to deploy your subgraph to **The Graph - Hosted** infrastructure:

 1. [Manually](#manually)
 2. [Automatically](#automatically)

### Manually

Please follow these steps:

> **NOTE**: please create and deploy your subgraph following the pattern `${USERNAME}/${SUBGRAPH}` to ensure proper access.

1. Build your subgraph:

   ```bash
   yarn install && yarn codegen && yarn build
   ```

2. Create your subgraph:

   ```bash
   graph create --node https://${USERNAME}:${PASSWORD}@index-${USERNAME}.protofire-thegraph.com ${USERNAME}/${SUBGRAPH}
   ```

3. Deploy your subgraph:

   ```bash
   graph deploy --version-label ${USERNAME}/${SUBGRAPH} --headers "{\"Authorization\": \"Basic ${BASIC_AUTH}\"}" --ipfs https://ipfs-hosted.protofire-thegraph.com --node https://${USERNAME}:${PASSWORD}@index-${USERNAME}.protofire-thegraph.com ${USERNAME}/${SUBGRAPH}
   ```

### Automatically

You can use the following workflow template deploy your subgraph automatically: [LINK](./subgraph-deploy.yaml)

You'll need to copy the workflow to your subgraph repository and run it manually; the pipeline will ask you the following input data:

- USERNAME
- PASSWORD
- BASIC AUTH
- SUBGRAPH

> **NOTE**: you can customize the workflow in order to include additional steps based on your subgraph code; and you can also make it run autoamtically after a specific event (such as push, tag, label)

## Monitoring

Once you have created and deployed your subgraph you can use the same credentials (USERNAME & PASSWORD) to access the ***Indexing Status Overview*** dashboard in [Grafana](https://grafana-hosted.protofire-thegraph.com).