---
title: Esempi dell'interfaccia della riga di comando di Azure Cosmos DB | Documentazione Microsoft
description: Esempi dell'interfaccia della riga di comando di Azure - Creare e gestire account, database, contenitori, aree e firewall di Azure Cosmos DB.
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 06/07/2017
ms.author: mimig
ms.openlocfilehash: 709d2ccce0f4b9827a8076f683c7e0f74cbdd4ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a><span data-ttu-id="08ce0-103">Esempi dell'interfaccia della riga di comando di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="08ce0-103">Azure CLI samples for Azure Cosmos DB</span></span>

<span data-ttu-id="08ce0-104">La tabella seguente include collegamenti a esempi di script di interfaccia della riga di comando di Azure per Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="08ce0-104">The following table includes links to sample Azure CLI scripts for Azure Cosmos DB.</span></span> <span data-ttu-id="08ce0-105">Per tutti i comandi dell'interfaccia della riga di comando di Azure Cosmos DB sono disponibili pagine di riferimento in [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb) (Informazioni di riferimento sull'interfaccia della riga di comando di Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="08ce0-105">Reference pages for all Azure Cosmos DB CLI commands are available in the [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb).</span></span>

| |  |
|---|---|
|<span data-ttu-id="08ce0-106">**Creare account di database e contenitori di Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="08ce0-106">**Create Azure Cosmos DB account, database, and containers**</span></span>||
|[<span data-ttu-id="08ce0-107">Creare un account API DocumentDB, API Graph o API di tabella</span><span class="sxs-lookup"><span data-stu-id="08ce0-107">Create a DocumentDB API, Graph, or Table API account</span></span>](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="08ce0-108">Consente di creare un account, un database e un contenitore dell'API Azure Cosmos DB da usare con le API DocumentDB, Graph o di tabella.</span><span class="sxs-lookup"><span data-stu-id="08ce0-108">Creates a single Azure Cosmos DB API account, database, and container for use with the DocumentDB, Graph, or Table APIs.</span></span> |
| [<span data-ttu-id="08ce0-109">Creare un account di API MongoDB</span><span class="sxs-lookup"><span data-stu-id="08ce0-109">Create a MongoDB API account</span></span>](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="08ce0-110">Crea un singolo account di API MongoDB, database e raccolta di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="08ce0-110">Creates a single Azure Cosmos DB MongoDB API account, database, and collection.</span></span> |
|<span data-ttu-id="08ce0-111">**Scalare Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="08ce0-111">**Scale Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="08ce0-112">Scalare la velocità effettiva del contenitore</span><span class="sxs-lookup"><span data-stu-id="08ce0-112">Scale container throughput</span></span>](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="08ce0-113">Modifica la velocità effettiva con provisioning in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="08ce0-113">Changes the provisioned througput on a container.</span></span>|
|[<span data-ttu-id="08ce0-114">Replicare l'account di database di Azure Cosmos DB in più aree e configurare le priorità di failover</span><span class="sxs-lookup"><span data-stu-id="08ce0-114">Replicate Azure Cosmos DB database account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="08ce0-115">Replica a livello globale i dati dell'account in più aree con una priorità di failover specificata.</span><span class="sxs-lookup"><span data-stu-id="08ce0-115">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="08ce0-116">**Proteggere Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="08ce0-116">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="08ce0-117">Ottenere le chiavi dell'account</span><span class="sxs-lookup"><span data-stu-id="08ce0-117">Get account keys</span></span>](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="08ce0-118">Ottiene le chiavi di scrittura master primarie e secondarie e le chiavi di sola lettura primarie e secondarie per l'account.</span><span class="sxs-lookup"><span data-stu-id="08ce0-118">Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.</span></span>|
| [<span data-ttu-id="08ce0-119">Ottenere la stringa di connessione di MongoDB</span><span class="sxs-lookup"><span data-stu-id="08ce0-119">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="08ce0-120">Ottiene la stringa di connessione per connettere l'app MongoDB all'account di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="08ce0-120">Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="08ce0-121">Rigenerare le chiavi dell'account</span><span class="sxs-lookup"><span data-stu-id="08ce0-121">Regenerate account keys</span></span>](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="08ce0-122">Rigenera la chiave master o di sola lettura per l'account.</span><span class="sxs-lookup"><span data-stu-id="08ce0-122">Regenerates the master or read-only key for the account.</span></span>|
|[<span data-ttu-id="08ce0-123">Creare un firewall</span><span class="sxs-lookup"><span data-stu-id="08ce0-123">Create a firewall</span></span>](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="08ce0-124">Crea un criterio di controllo di accesso IP in ingresso per limitare l'accesso all'account da un set di macchine e/o servizi cloud approvati.</span><span class="sxs-lookup"><span data-stu-id="08ce0-124">Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="08ce0-125">**Disponibilità elevata, ripristino di emergenza, backup e ripristino**</span><span class="sxs-lookup"><span data-stu-id="08ce0-125">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="08ce0-126">Configurare i criteri di failover</span><span class="sxs-lookup"><span data-stu-id="08ce0-126">Configure failover policy</span></span>](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="08ce0-127">Imposta la priorità di failover di ogni area in cui l'account viene replicato.</span><span class="sxs-lookup"><span data-stu-id="08ce0-127">Sets the failover priority of each region in which the account is replicated.</span></span>|
|<span data-ttu-id="08ce0-128">**Connettere Azure Cosmos DB alle risorse**</span><span class="sxs-lookup"><span data-stu-id="08ce0-128">**Connect Azure Cosmos DB to resources**</span></span>||
|[<span data-ttu-id="08ce0-129">Connettere un'app Web ad Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="08ce0-129">Connect a web app to Azure Cosmos DB</span></span>](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="08ce0-130">Creare e collegare un database Azure Cosmos DB e un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="08ce0-130">Create and connect an Azure Cosmos DB database and an Azure web app.</span></span>|
|||
