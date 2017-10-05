---
title: Esempi di Azure PowerShell per Azure Cosmos DB | Microsoft Docs
description: Esempi di Azure PowerShell - Script per creare e gestire gli account di Azure Cosmos DB.
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 7698e03c0dc8d1c6d1e926f45e903a909bfd0c93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples-for-azure-cosmos-db"></a><span data-ttu-id="50eca-103">Esempi di Azure PowerShell per Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="50eca-103">Azure PowerShell samples for Azure Cosmos DB</span></span>

<span data-ttu-id="50eca-104">La tabella seguente include collegamenti a esempi di script di Azure PowerShell per Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="50eca-104">The following table includes links to sample Azure PowerShell scripts for Azure Cosmos DB.</span></span>

| |  |
|---|---|
|<span data-ttu-id="50eca-105">**Creare un account di Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="50eca-105">**Create an Azure Cosmos DB account**</span></span>||
|[<span data-ttu-id="50eca-106">Creare un account API di DocumentDB</span><span class="sxs-lookup"><span data-stu-id="50eca-106">Create a DocumentDB API account</span></span>](scripts/create-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="50eca-107">Crea un singolo account API di Azure Cosmos DB da usare con l'API di DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="50eca-107">Creates a single Azure Cosmos DB account to use with the DocumentDB API.</span></span> |
|<span data-ttu-id="50eca-108">**Ridimensionare Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="50eca-108">**Scale Azure Cosmos DB**</span></span>||
|[<span data-ttu-id="50eca-109">Replicare l'account di Azure Cosmos DB in più aree e configurare le priorità di failover</span><span class="sxs-lookup"><span data-stu-id="50eca-109">Replicate Azure Cosmos DB account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="50eca-110">Replica a livello globale i dati dell'account in più aree con una priorità di failover specificata.</span><span class="sxs-lookup"><span data-stu-id="50eca-110">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="50eca-111">**Proteggere Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="50eca-111">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="50eca-112">Ottenere le chiavi dell'account</span><span class="sxs-lookup"><span data-stu-id="50eca-112">Get account keys</span></span>](scripts/secure-get-account-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="50eca-113">Ottiene le chiavi di scrittura master primarie e secondarie e le chiavi di sola lettura primarie e secondarie per l'account.</span><span class="sxs-lookup"><span data-stu-id="50eca-113">Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.</span></span>|
| [<span data-ttu-id="50eca-114">Ottenere la stringa di connessione di MongoDB</span><span class="sxs-lookup"><span data-stu-id="50eca-114">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="50eca-115">Ottiene la stringa di connessione per connettere l'app MongoDB all'account di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="50eca-115">Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="50eca-116">Rigenerare le chiavi dell'account</span><span class="sxs-lookup"><span data-stu-id="50eca-116">Regenerate account keys</span></span>](scripts/secure-regenerate-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="50eca-117">Rigenera la chiave master o di sola lettura per l'account.</span><span class="sxs-lookup"><span data-stu-id="50eca-117">Regenerates the master or read-only key for the account.</span></span>|
|[<span data-ttu-id="50eca-118">Creare un firewall</span><span class="sxs-lookup"><span data-stu-id="50eca-118">Create a firewall</span></span>](scripts/create-firewall-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="50eca-119">Crea un criterio di controllo di accesso IP in ingresso per limitare l'accesso all'account da un set di macchine e/o servizi cloud approvati.</span><span class="sxs-lookup"><span data-stu-id="50eca-119">Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="50eca-120">**Disponibilità elevata, ripristino di emergenza, backup e ripristino**</span><span class="sxs-lookup"><span data-stu-id="50eca-120">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="50eca-121">Configurare i criteri di failover</span><span class="sxs-lookup"><span data-stu-id="50eca-121">Configure failover policy</span></span>](scripts/ha-failover-policy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="50eca-122">Imposta la priorità di failover di ogni area in cui l'account viene replicato.</span><span class="sxs-lookup"><span data-stu-id="50eca-122">Sets the failover priority of each region in which the account is replicated.</span></span>|
|||