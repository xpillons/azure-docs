---
title: How to manually register an Entra ID application for Open OnDemand authentication
description: How to manually register an Entra ID application for Open OnDemand authentication
author: xpillons
ms.date: 03/17/2025
ms.author: xpillons
---

# How to manually register an Entra ID application for Open OnDemand authentication
User authentication on the Open OnDemand front end is defined to use Entra ID with the Open ID Connector configured for it. Because registering an Entra Application is not possible when deploying from the marketplace or if registering that application needs to be done by a different teamp that the one building the environment, you need to execute the command below to register such application.

```
resource_group=ENTER_RG_NAME; az deployment group create -g $resource_group --template-uri https://raw.githubusercontent.com/Azure/cyclecloud-slurm-workspace/refs/tags/2025.03.12/bicep/ood/oodEntraApp.json --parameters "$(az deployment group show -g $resource_group -n pid-b3313305-4e26-4c98-93c5-06d5412cb53d-partnercenter --query properties.outputs | jq '.oodManualRegistration.value | with_entries(.value |= {value: .})')"
```