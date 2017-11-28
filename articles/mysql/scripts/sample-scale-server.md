---
title: esempi di aaaAzure CLI tooscale un Database di Azure per il server MySQL | Documenti Microsoft
description: Questo script di esempio CLI Ridimensiona i Database di Azure a livello di prestazioni diverse tooa di MySQL server dopo l'esecuzione di query metriche hello.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 05/31/2017
ms.openlocfilehash: 721ef9db35a5f3be7a38438c1abb724187b18b75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="26f2f-103">Monitorare a scalare un database di Azure per il server MySQL usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="26f2f-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="26f2f-104">Questo script di esempio CLI ridimensiona un singolo Database di Azure a livello di prestazioni diverse tooa di MySQL server dopo l'esecuzione di query metriche hello.</span><span class="sxs-lookup"><span data-stu-id="26f2f-104">This sample CLI script scales a single Azure Database for MySQL server tooa different performance level after querying hello metrics.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="26f2f-105">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="26f2f-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="26f2f-106">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="26f2f-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="26f2f-107">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="26f2f-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="26f2f-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="26f2f-108">Sample script</span></span>
<span data-ttu-id="26f2f-109">In questo esempio, modificare hello evidenziato righe toocustomize hello admin username e password.</span><span class="sxs-lookup"><span data-stu-id="26f2f-109">In this sample script, change hello highlighted lines toocustomize hello admin username and password.</span></span> <span data-ttu-id="26f2f-110">Sostituire l'id sottoscrizione hello utilizzato nei comandi di monitoraggio az hello con il proprio id sottoscrizione.[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span><span class="sxs-lookup"><span data-stu-id="26f2f-110">Replace hello subscription id used in hello az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="26f2f-111">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="26f2f-111">Clean up deployment</span></span>
<span data-ttu-id="26f2f-112">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="26f2f-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="26f2f-113">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="26f2f-113">Script explanation</span></span>
<span data-ttu-id="26f2f-114">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="26f2f-114">This script uses hello following commands.</span></span> <span data-ttu-id="26f2f-115">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="26f2f-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="26f2f-116">**Comando**</span><span class="sxs-lookup"><span data-stu-id="26f2f-116">**Command**</span></span> | <span data-ttu-id="26f2f-117">**Note**</span><span class="sxs-lookup"><span data-stu-id="26f2f-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="26f2f-118">az group create</span><span class="sxs-lookup"><span data-stu-id="26f2f-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="26f2f-119">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="26f2f-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="26f2f-120">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="26f2f-120">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="26f2f-121">Crea un server di MySQL che ospita i database hello.</span><span class="sxs-lookup"><span data-stu-id="26f2f-121">Creates a MySQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="26f2f-122">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="26f2f-122">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="26f2f-123">Elenco hello valore metrico per le risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="26f2f-123">List hello metric value for hello resources.</span></span> |
| [<span data-ttu-id="26f2f-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="26f2f-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="26f2f-125">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="26f2f-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="26f2f-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="26f2f-126">Next steps</span></span>
- <span data-ttu-id="26f2f-127">Altre informazioni su hello CLI di Azure: [documentazione CLI di Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="26f2f-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="26f2f-128">Provare a eseguire altri script: [esempi dell'interfaccia della riga di comando di Azure per il database di Azure per MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="26f2f-128">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="26f2f-129">Per altre informazioni sul ridimensionamento, vedere [Livelli di servizio](../concepts-service-tiers.md) e [Unità di calcolo e unità di archiviazione](../concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="26f2f-129">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span></span>
