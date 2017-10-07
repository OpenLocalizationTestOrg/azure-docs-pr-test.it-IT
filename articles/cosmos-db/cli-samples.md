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
# <a name="azure-cli-samples-for-azure-cosmos-db"></a>Esempi dell'interfaccia della riga di comando di Azure Cosmos DB

Hello nella tabella seguente include collegamenti toosample CLI di Azure gli script di Azure Cosmos DB. Pagine di riferimento per tutti i comandi CLI di Azure Cosmos DB sono disponibili in hello [Azure CLI 2.0 riferimento](https://docs.microsoft.com/cli/azure/cosmosdb).

| |  |
|---|---|
|**Creare account di database e contenitori di Azure Cosmos DB**||
|[Creare un account API DocumentDB, API Graph o API di tabella](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| Crea un singolo account Azure Cosmos DB API, database e contenitore per l'utilizzo con hello DocumentDB, grafico o le API di tabella. |
| [Creare un account di API MongoDB](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Crea un singolo account di API MongoDB, database e raccolta di Azure Cosmos DB. |
|**Scalare Azure Cosmos DB**||
| [Scalare la velocità effettiva del contenitore](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Hello modifiche provisioning througput in un contenitore.|
|[Replicare l'account di database di Azure Cosmos DB in più aree e configurare le priorità di failover](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Replica a livello globale i dati dell'account in più aree con una priorità di failover specificata.|
|**Proteggere Azure Cosmos DB**||
| [Ottenere le chiavi dell'account](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Ottiene le chiavi primarie e secondarie scrittura master hello e primarie e secondarie chiavi di sola lettura per account hello.|
| [Ottenere la stringa di connessione di MongoDB](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Ottiene tooconnect stringa di connessione hello il tooyour app MongoDB account Azure Cosmos DB.|
|[Rigenerare le chiavi dell'account](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Rigenera chiave di sola lettura per conto di hello o master hello.|
|[Creare un firewall](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| Crea un in ingresso IP accesso controllo criteri toolimit accesso toohello account da un set di computer e/o i servizi cloud approvato.|
|**Disponibilità elevata, ripristino di emergenza, backup e ripristino**||
|[Configurare i criteri di failover](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Set di hello priorità di failover di ogni area in cui viene replicato l'account di hello.|
|**Connettere Azure Cosmos DB alle risorse**||
|[Connettersi a un tooAzure app web Cosmos DB](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|Creare e collegare un database Azure Cosmos DB e un'app Web di Azure.|
|||
