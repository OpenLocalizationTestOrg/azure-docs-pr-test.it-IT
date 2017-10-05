---
title: Esempi dell'interfaccia della riga di comando di Azure per scalare un database di Azure per il server MySQL | Documentazione Microsoft
description: Questo esempio di script dell'interfaccia della riga di comando di Azure scala un database di Azure per il MySQL a un diverso livello di prestazioni dopo le query sulle metriche.
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
ms.openlocfilehash: 33316ff3db382d25a444d55772c6ee4d7b7ac418
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="2f113-103">Monitorare a scalare un database di Azure per il server MySQL usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="2f113-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="2f113-104">Questo esempio di script dell'interfaccia della riga di comando di Azure scala un singolo database di Azure per il server MySQL a un diverso livello di prestazioni dopo le query sulle metriche.</span><span class="sxs-lookup"><span data-stu-id="2f113-104">This sample CLI script scales a single Azure Database for MySQL server to a different performance level after querying the metrics.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2f113-105">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="2f113-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2f113-106">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="2f113-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="2f113-107">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2f113-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="2f113-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="2f113-108">Sample script</span></span>
<span data-ttu-id="2f113-109">In questo script di esempio modificare le righe evidenziate per personalizzare nome utente e password amministratore.</span><span class="sxs-lookup"><span data-stu-id="2f113-109">In this sample script, change the highlighted lines to customize the admin username and password.</span></span> <span data-ttu-id="2f113-110">Sostituire l'ID sottoscrizione utilizzato nei comandi di monitoraggio az con il proprio ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="2f113-110">Replace the subscription id used in the az monitor commands with your own subscription id.</span></span>
<span data-ttu-id="2f113-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Creare e scalare il database di Azure per MySQL.")]</span><span class="sxs-lookup"><span data-stu-id="2f113-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2f113-112">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="2f113-112">Clean up deployment</span></span>
<span data-ttu-id="2f113-113">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="2f113-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="2f113-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Eliminare il gruppo di risorse.")]</span><span class="sxs-lookup"><span data-stu-id="2f113-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="2f113-115">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="2f113-115">Script explanation</span></span>
<span data-ttu-id="2f113-116">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="2f113-116">This script uses the following commands.</span></span> <span data-ttu-id="2f113-117">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="2f113-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2f113-118">**Comando**</span><span class="sxs-lookup"><span data-stu-id="2f113-118">**Command**</span></span> | <span data-ttu-id="2f113-119">**Note**</span><span class="sxs-lookup"><span data-stu-id="2f113-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="2f113-120">az group create</span><span class="sxs-lookup"><span data-stu-id="2f113-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="2f113-121">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="2f113-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2f113-122">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="2f113-122">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="2f113-123">Crea un server MySQL che ospita i database.</span><span class="sxs-lookup"><span data-stu-id="2f113-123">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="2f113-124">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="2f113-124">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="2f113-125">Elencare il valore metrico per le risorse.</span><span class="sxs-lookup"><span data-stu-id="2f113-125">List the metric value for the resources.</span></span> |
| [<span data-ttu-id="2f113-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="2f113-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="2f113-127">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="2f113-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2f113-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2f113-128">Next steps</span></span>
- <span data-ttu-id="2f113-129">Altre informazioni sull'interfaccia della riga di comando di Azure: [documentazione sull'interfaccia della riga di comando di Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2f113-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="2f113-130">Provare a eseguire altri script: [esempi dell'interfaccia della riga di comando di Azure per il database di Azure per MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="2f113-130">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="2f113-131">Per altre informazioni sul ridimensionamento, vedere [Livelli di servizio](../concepts-service-tiers.md) e [Unità di calcolo e unità di archiviazione](../concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="2f113-131">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span></span>
