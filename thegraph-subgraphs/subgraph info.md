---
sidebar_position: 1
title: Subgraph Data Introduction
---

# Hop Subgraph Introduction

Hop has a GraphQL API Endpoint hosted by [The Graph](https://thegraph.com/docs/about/introduction#what-the-graph-is) called a subgraph for indexing and organizing data from the Sablier smart contracts.

This subgraph is can be used to query Hop data.

Subgraph information is serviced by a decentralized group of server operators called Indexers.

## Ethereum Mainnet

[Creating an API Key Video Tutorial](https://www.youtube.com/watch?v=UrfIpm-Vlgs)

- [Explorer Page](https://thegraph.com/explorer/subgraph?id=Cjv3tykF4wnd6m9TRmQV7weiLjizDnhyt6x2tTJB42Cy&view=Playground)
- Graphql Endpoint: https://gateway.thegraph.com/api/[api-key]/subgraphs/id/Cjv3tykF4wnd6m9TRmQV7weiLjizDnhyt6x2tTJB42Cy
- [Code Repo](https://github.com/hop-protocol/subgraph)

## Subgraph links

- [Mainnet](https://thegraph.com/hosted-service/subgraph/hop-protocol/hop-mainnet)
- [Polygon](https://thegraph.com/hosted-service/subgraph/hop-protocol/hop-polygon)
- [XDai](https://thegraph.com/hosted-service/subgraph/hop-protocol/hop-xdai)
- [Arbitrum](https://thegraph.com/hosted-service/subgraph/hop-protocol/hop-arbitrum)
- [Optimism](https://thegraph.com/hosted-service/subgraph/hop-protocol/hop-optimism)

## Transfers

Use these subgraphs for querying L2->L2 or L2->L1 transfers (query for transferSent entities)

- hop-protocol/hop-polygon
- hop-protocol/hop-xdai
- hop-protocol/hop-arbitrum
- hop-protocol/hop-optimism

Use this subgraph for L1->L2 transfers (query for transferSentToL2 entities)

- hop-protocol/hop-mainnet
