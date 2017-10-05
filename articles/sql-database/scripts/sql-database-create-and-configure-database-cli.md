---
title: Esempio dell'interfaccia della riga di comando - Creare un database SQL di Azure | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure per creare un database SQL
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 908898ca691d2b53b9f54afa60c41e091163bd50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-create-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="ef6c6-103">Usare l'interfaccia della riga di comando per creare un singolo database SQL di Azure e configurare una regola del firewall</span><span class="sxs-lookup"><span data-stu-id="ef6c6-103">Use CLI to create a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="ef6c6-104">Questo script di esempio dell'interfaccia della riga di comando di Azure crea un database SQL di Azure e configura una regola del firewall a livello di server.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-104">This Azure CLI script example creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="ef6c6-105">Dopo aver eseguito correttamente lo script, è possibile accedere al database SQL da tutti i servizi di Azure e dall'indirizzo IP configurato.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ef6c6-106">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ef6c6-107">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="ef6c6-108">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ef6c6-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ef6c6-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="ef6c6-109">Sample script</span></span>

<span data-ttu-id="ef6c6-110">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Creare database SQL")]</span><span class="sxs-lookup"><span data-stu-id="ef6c6-110">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ef6c6-111">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="ef6c6-111">Clean up deployment</span></span>

<span data-ttu-id="ef6c6-112">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ef6c6-113">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="ef6c6-113">Script explanation</span></span>

<span data-ttu-id="ef6c6-114">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-114">This script uses the following commands.</span></span> <span data-ttu-id="ef6c6-115">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ef6c6-116">Comando</span><span class="sxs-lookup"><span data-stu-id="ef6c6-116">Command</span></span> | <span data-ttu-id="ef6c6-117">Note</span><span class="sxs-lookup"><span data-stu-id="ef6c6-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ef6c6-118">az group create</span><span class="sxs-lookup"><span data-stu-id="ef6c6-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="ef6c6-119">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ef6c6-120">az sql server create</span><span class="sxs-lookup"><span data-stu-id="ef6c6-120">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="ef6c6-121">Consente di creare un server logico che ospita il database SQL.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-121">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="ef6c6-122">az sql server firewall create</span><span class="sxs-lookup"><span data-stu-id="ef6c6-122">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="ef6c6-123">Consente di creare una regola del firewall per consentire l'accesso a tutti i database SQL presenti sul server dall'intervallo di indirizzi IP immesso.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-123">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="ef6c6-124">az sql db create</span><span class="sxs-lookup"><span data-stu-id="ef6c6-124">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="ef6c6-125">Consente di creare il database SQL nel server logico.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-125">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="ef6c6-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="ef6c6-126">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="ef6c6-127">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="ef6c6-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ef6c6-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ef6c6-128">Next steps</span></span>

<span data-ttu-id="ef6c6-129">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ef6c6-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ef6c6-130">Per altri esempi di script dell'interfaccia della riga di comando per database SQL, vedere la [documentazione del database SQL di Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ef6c6-130">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

