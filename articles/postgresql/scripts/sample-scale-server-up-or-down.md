---
title: aaa "Database Azure Script scala CLI di Azure per PostgreSQL | Documenti di Microsoft"
description: "Azure CLI Script di esempio - Database Azure scalabilità a livello di prestazioni diverse PostgreSQL server tooa dopo l'esecuzione di query metriche hello."
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
ms.openlocfilehash: 678b28941dbb4334cb374d4888991a00b44966b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a><span data-ttu-id="02d18-103">Monitorare e scalare un singolo server PostgreSQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="02d18-103">Monitor and scale a single PostgreSQL server using Azure CLI</span></span>
<span data-ttu-id="02d18-104">Questo script di esempio CLI ridimensiona un singolo Database di Azure a livello di prestazioni diverse PostgreSQL server tooa dopo l'esecuzione di query metriche hello.</span><span class="sxs-lookup"><span data-stu-id="02d18-104">This sample CLI script scales a single Azure Database for PostgreSQL server tooa different performance level after querying hello metrics.</span></span> 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="02d18-105">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="02d18-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="02d18-106">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="02d18-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="02d18-107">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="02d18-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="02d18-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="02d18-108">Sample script</span></span>
<span data-ttu-id="02d18-109">In questo esempio, modificare hello evidenziato righe toocustomize hello admin username e password.</span><span class="sxs-lookup"><span data-stu-id="02d18-109">In this sample script, change hello highlighted lines toocustomize hello admin username and password.</span></span> <span data-ttu-id="02d18-110">Sostituire l'id sottoscrizione hello utilizzato nei comandi di monitoraggio az hello con il proprio id sottoscrizione.[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]</span><span class="sxs-lookup"><span data-stu-id="02d18-110">Replace hello subscription id used in hello az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="02d18-111">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="02d18-111">Clean up deployment</span></span>
<span data-ttu-id="02d18-112">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="02d18-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="02d18-113">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="02d18-113">Script explanation</span></span>
<span data-ttu-id="02d18-114">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="02d18-114">This script uses hello following commands.</span></span> <span data-ttu-id="02d18-115">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="02d18-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="02d18-116">**Comando**</span><span class="sxs-lookup"><span data-stu-id="02d18-116">**Command**</span></span> | <span data-ttu-id="02d18-117">**Note**</span><span class="sxs-lookup"><span data-stu-id="02d18-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="02d18-118">az group create</span><span class="sxs-lookup"><span data-stu-id="02d18-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="02d18-119">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="02d18-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="02d18-120">az postgres server create</span><span class="sxs-lookup"><span data-stu-id="02d18-120">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="02d18-121">Crea un server PostgreSQL che ospita i database hello.</span><span class="sxs-lookup"><span data-stu-id="02d18-121">Creates a PostgreSQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="02d18-122">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="02d18-122">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="02d18-123">Elenco hello valore metrico per le risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="02d18-123">List hello metric value for hello resources.</span></span> |
| [<span data-ttu-id="02d18-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="02d18-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="02d18-125">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="02d18-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="02d18-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="02d18-126">Next steps</span></span>
- <span data-ttu-id="02d18-127">Altre informazioni su hello CLI di Azure: [documentazione CLI di Azure](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="02d18-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="02d18-128">Provare a eseguire altri script: [esempi dell'interfaccia della riga di comando di Azure per il database di Azure per PostgreSQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="02d18-128">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="02d18-129">Altre informazioni sul ridimensionamento: [Livelli di servizio](../concepts-service-tiers.md) e [Unità di calcolo e unità di archiviazione](../concepts-compute-unit-and-storage.md)</span><span class="sxs-lookup"><span data-stu-id="02d18-129">Read more information on scaling: [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md)</span></span>
