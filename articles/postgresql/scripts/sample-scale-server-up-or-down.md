---
title: Script dell'interfaccia della riga di comando - Scalare un database di Azure per PostgreSQL | Documentazione Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Scalare il database di Azure per il server PostgreSQL a un diverso livello di prestazioni dopo le query sulle metriche.
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: b847abb336cce5dd5516469dca58002d3ba265f0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a><span data-ttu-id="87d83-103">Monitorare e scalare un singolo server PostgreSQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="87d83-103">Monitor and scale a single PostgreSQL server using Azure CLI</span></span>
<span data-ttu-id="87d83-104">Questo esempio di script dell'interfaccia della riga di comando di Azure scala un singolo database di Azure per il server PostgreSQL a un diverso livello di prestazioni dopo le query sulle metriche.</span><span class="sxs-lookup"><span data-stu-id="87d83-104">This sample CLI script scales a single Azure Database for PostgreSQL server to a different performance level after querying the metrics.</span></span> 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="87d83-105">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="87d83-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="87d83-106">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="87d83-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="87d83-107">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="87d83-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="87d83-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="87d83-108">Sample script</span></span>
<span data-ttu-id="87d83-109">In questo script di esempio modificare le righe evidenziate per personalizzare nome utente e password amministratore.</span><span class="sxs-lookup"><span data-stu-id="87d83-109">In this sample script, change the highlighted lines to customize the admin username and password.</span></span> <span data-ttu-id="87d83-110">Sostituire l'ID sottoscrizione usato nei comandi az monitor con il proprio ID sottoscrizione. [!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Creare e ridimensionare un database di Azure per PostgreSQL.")]</span><span class="sxs-lookup"><span data-stu-id="87d83-110">Replace the subscription id used in the az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="87d83-111">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="87d83-111">Clean up deployment</span></span>
<span data-ttu-id="87d83-112">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="87d83-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="87d83-113">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Eliminare il gruppo di risorse.")]</span><span class="sxs-lookup"><span data-stu-id="87d83-113">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="87d83-114">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="87d83-114">Script explanation</span></span>
<span data-ttu-id="87d83-115">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="87d83-115">This script uses the following commands.</span></span> <span data-ttu-id="87d83-116">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="87d83-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="87d83-117">**Comando**</span><span class="sxs-lookup"><span data-stu-id="87d83-117">**Command**</span></span> | <span data-ttu-id="87d83-118">**Note**</span><span class="sxs-lookup"><span data-stu-id="87d83-118">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="87d83-119">az group create</span><span class="sxs-lookup"><span data-stu-id="87d83-119">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="87d83-120">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="87d83-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="87d83-121">az postgres server create</span><span class="sxs-lookup"><span data-stu-id="87d83-121">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="87d83-122">Crea un server PostgreSQL che ospita i database.</span><span class="sxs-lookup"><span data-stu-id="87d83-122">Creates a PostgreSQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="87d83-123">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="87d83-123">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="87d83-124">Elencare il valore metrico per le risorse.</span><span class="sxs-lookup"><span data-stu-id="87d83-124">List the metric value for the resources.</span></span> |
| [<span data-ttu-id="87d83-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="87d83-125">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="87d83-126">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="87d83-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="87d83-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="87d83-127">Next steps</span></span>
- <span data-ttu-id="87d83-128">Altre informazioni sull'interfaccia della riga di comando di Azure: [documentazione sull'interfaccia della riga di comando di Azure](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="87d83-128">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="87d83-129">Provare a eseguire altri script: [esempi dell'interfaccia della riga di comando di Azure per il database di Azure per PostgreSQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="87d83-129">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="87d83-130">Altre informazioni sul ridimensionamento: [Livelli di servizio](../concepts-service-tiers.md) e [Unità di calcolo e unità di archiviazione](../concepts-compute-unit-and-storage.md)</span><span class="sxs-lookup"><span data-stu-id="87d83-130">Read more information on scaling: [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md)</span></span>
