---
title: Esempi di CLI di Azure Cosmos DB aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: d6eefc3274e0b66eec4e69166bb7d4ddd58a522e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a><span data-ttu-id="eec92-103">Esempi dell'interfaccia della riga di comando di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="eec92-103">Azure CLI samples for Azure Cosmos DB</span></span>

<span data-ttu-id="eec92-104">Hello nella tabella seguente include collegamenti toosample CLI di Azure gli script di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="eec92-104">hello following table includes links toosample Azure CLI scripts for Azure Cosmos DB.</span></span> <span data-ttu-id="eec92-105">Pagine di riferimento per tutti i comandi CLI di Azure Cosmos DB sono disponibili in hello [Azure CLI 2.0 riferimento](https://docs.microsoft.com/cli/azure/cosmosdb).</span><span class="sxs-lookup"><span data-stu-id="eec92-105">Reference pages for all Azure Cosmos DB CLI commands are available in hello [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb).</span></span>

| |  |
|---|---|
|<span data-ttu-id="eec92-106">**Creare account di database e contenitori di Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="eec92-106">**Create Azure Cosmos DB account, database, and containers**</span></span>||
|[<span data-ttu-id="eec92-107">Creare un account API DocumentDB, API Graph o API di tabella</span><span class="sxs-lookup"><span data-stu-id="eec92-107">Create a DocumentDB API, Graph, or Table API account</span></span>](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="eec92-108">Crea un singolo account Azure Cosmos DB API, database e contenitore per l'utilizzo con hello DocumentDB, grafico o le API di tabella.</span><span class="sxs-lookup"><span data-stu-id="eec92-108">Creates a single Azure Cosmos DB API account, database, and container for use with hello DocumentDB, Graph, or Table APIs.</span></span> |
| [<span data-ttu-id="eec92-109">Creare un account di API MongoDB</span><span class="sxs-lookup"><span data-stu-id="eec92-109">Create a MongoDB API account</span></span>](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="eec92-110">Crea un singolo account di API MongoDB, database e raccolta di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="eec92-110">Creates a single Azure Cosmos DB MongoDB API account, database, and collection.</span></span> |
|<span data-ttu-id="eec92-111">**Scalare Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="eec92-111">**Scale Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="eec92-112">Scalare la velocità effettiva del contenitore</span><span class="sxs-lookup"><span data-stu-id="eec92-112">Scale container throughput</span></span>](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="eec92-113">Hello modifiche provisioning througput in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="eec92-113">Changes hello provisioned througput on a container.</span></span>|
|[<span data-ttu-id="eec92-114">Replicare l'account di database di Azure Cosmos DB in più aree e configurare le priorità di failover</span><span class="sxs-lookup"><span data-stu-id="eec92-114">Replicate Azure Cosmos DB database account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="eec92-115">Replica a livello globale i dati dell'account in più aree con una priorità di failover specificata.</span><span class="sxs-lookup"><span data-stu-id="eec92-115">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="eec92-116">**Proteggere Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="eec92-116">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="eec92-117">Ottenere le chiavi dell'account</span><span class="sxs-lookup"><span data-stu-id="eec92-117">Get account keys</span></span>](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="eec92-118">Ottiene le chiavi primarie e secondarie scrittura master hello e primarie e secondarie chiavi di sola lettura per account hello.</span><span class="sxs-lookup"><span data-stu-id="eec92-118">Gets hello primary and secondary master write keys and primary and secondary read-only keys for hello account.</span></span>|
| [<span data-ttu-id="eec92-119">Ottenere la stringa di connessione di MongoDB</span><span class="sxs-lookup"><span data-stu-id="eec92-119">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="eec92-120">Ottiene tooconnect stringa di connessione hello il tooyour app MongoDB account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="eec92-120">Gets hello connection string tooconnect your MongoDB app tooyour Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="eec92-121">Rigenerare le chiavi dell'account</span><span class="sxs-lookup"><span data-stu-id="eec92-121">Regenerate account keys</span></span>](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="eec92-122">Rigenera chiave di sola lettura per conto di hello o master hello.</span><span class="sxs-lookup"><span data-stu-id="eec92-122">Regenerates hello master or read-only key for hello account.</span></span>|
|[<span data-ttu-id="eec92-123">Creare un firewall</span><span class="sxs-lookup"><span data-stu-id="eec92-123">Create a firewall</span></span>](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="eec92-124">Crea un in ingresso IP accesso controllo criteri toolimit accesso toohello account da un set di computer e/o i servizi cloud approvato.</span><span class="sxs-lookup"><span data-stu-id="eec92-124">Creates an inbound IP access control policy toolimit access toohello account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="eec92-125">**Disponibilità elevata, ripristino di emergenza, backup e ripristino**</span><span class="sxs-lookup"><span data-stu-id="eec92-125">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="eec92-126">Configurare i criteri di failover</span><span class="sxs-lookup"><span data-stu-id="eec92-126">Configure failover policy</span></span>](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="eec92-127">Set di hello priorità di failover di ogni area in cui viene replicato l'account di hello.</span><span class="sxs-lookup"><span data-stu-id="eec92-127">Sets hello failover priority of each region in which hello account is replicated.</span></span>|
|<span data-ttu-id="eec92-128">**Connettere Azure Cosmos DB alle risorse**</span><span class="sxs-lookup"><span data-stu-id="eec92-128">**Connect Azure Cosmos DB to resources**</span></span>||
|[<span data-ttu-id="eec92-129">Connettersi a un tooAzure app web Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="eec92-129">Connect a web app tooAzure Cosmos DB</span></span>](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="eec92-130">Creare e collegare un database Azure Cosmos DB e un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="eec92-130">Create and connect an Azure Cosmos DB database and an Azure web app.</span></span>|
|||
