---
title: database SQL di Azure di esempio-monitor-scala-singolo aaaCLI | Documenti Microsoft
description: Scala un singolo database di SQL Azure e Azure toomonitor di script di esempio CLI
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 36031ddd46a947a80fe37884858a84eb66217270
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomonitor-and-scale-a-single-sql-database"></a><span data-ttu-id="a5296-103">Utilizzare toomonitor CLI e ridimensionare un singolo database SQL</span><span class="sxs-lookup"><span data-stu-id="a5296-103">Use CLI toomonitor and scale a single SQL database</span></span>

<span data-ttu-id="a5296-104">Questo esempio di script CLI di Azure ridimensiona un unico livello di prestazioni diverse tooa database SQL di Azure dopo l'esecuzione di query su informazioni sulle dimensioni hello del database hello.</span><span class="sxs-lookup"><span data-stu-id="a5296-104">This Azure CLI script example scales a single Azure SQL database tooa different performance level after querying hello size information of hello database.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a5296-105">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="a5296-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a5296-106">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="a5296-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a5296-107">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a5296-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a5296-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="a5296-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a5296-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="a5296-109">Clean up deployment</span></span>

<span data-ttu-id="a5296-110">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="a5296-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="a5296-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="a5296-111">Script explanation</span></span>

<span data-ttu-id="a5296-112">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="a5296-112">This script uses hello following commands.</span></span> <span data-ttu-id="a5296-113">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="a5296-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a5296-114">Comando</span><span class="sxs-lookup"><span data-stu-id="a5296-114">Command</span></span> | <span data-ttu-id="a5296-115">Note</span><span class="sxs-lookup"><span data-stu-id="a5296-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a5296-116">az group create</span><span class="sxs-lookup"><span data-stu-id="a5296-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a5296-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="a5296-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a5296-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="a5296-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="a5296-119">Crea un server logico che ospita un database.</span><span class="sxs-lookup"><span data-stu-id="a5296-119">Creates a logical server that hosts a database.</span></span> |
| [<span data-ttu-id="a5296-120">az sql db show-usage</span><span class="sxs-lookup"><span data-stu-id="a5296-120">az sql db show-usage</span></span>](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | <span data-ttu-id="a5296-121">Mostra le informazioni di utilizzo dimensioni hello per un database.</span><span class="sxs-lookup"><span data-stu-id="a5296-121">Shows hello size usage information for a database.</span></span> |
| [<span data-ttu-id="a5296-122">az sql db update</span><span class="sxs-lookup"><span data-stu-id="a5296-122">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="a5296-123">Aggiorna le proprietà di database (ad esempio livello di prestazioni o livello di servizio hello) o si sposta un database in, out di o tra pool elastico.</span><span class="sxs-lookup"><span data-stu-id="a5296-123">Updates database properties (such as hello service tier or performance level) or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="a5296-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="a5296-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="a5296-125">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="a5296-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="a5296-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a5296-126">Next steps</span></span>

<span data-ttu-id="a5296-127">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a5296-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a5296-128">Ulteriori esempi di script SQL Database CLI sono reperibile in hello [documentazione relativa al Database di SQL Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a5296-128">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
