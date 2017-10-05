---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un account Batch | Documentazione Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un account Batch
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 698978fd717091c49a1375e222f46f4325431223
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-batch-account-with-the-azure-cli"></a><span data-ttu-id="645ea-103">Creare un account Batch con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="645ea-103">Create a Batch account with the Azure CLI</span></span>

<span data-ttu-id="645ea-104">Questo script crea un account Batch di Azure e illustra come le varie proprietà dell'account possono essere sottoposte a query e aggiornate.</span><span class="sxs-lookup"><span data-stu-id="645ea-104">This script creates an Azure Batch account and shows how various properties of the account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="645ea-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="645ea-105">Prerequisites</span></span>

<span data-ttu-id="645ea-106">Installare l'interfaccia della riga di comando di Azure usando le istruzioni presenti nella [Guida all'installazione dell'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), se questa operazione non è stata ancora eseguita.</span><span class="sxs-lookup"><span data-stu-id="645ea-106">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="645ea-107">Script di esempio per un account Batch</span><span class="sxs-lookup"><span data-stu-id="645ea-107">Batch account sample script</span></span>

<span data-ttu-id="645ea-108">Quando si crea un account Batch, per impostazione predefinita i relativi nodi di calcolo sono assegnati internamente dal servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="645ea-108">When you create a Batch account, by default its compute nodes are assigned internally by the Batch service.</span></span> <span data-ttu-id="645ea-109">I nodi di calcolo allocati saranno soggetti a una quota di memoria centrale separata e l'account può essere autenticato tramite le credenziali a chiave condivisa o un token di Azure Active Dirctory.</span><span class="sxs-lookup"><span data-stu-id="645ea-109">Allocated compute nodes will be subject to a separate core quota and the account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

<span data-ttu-id="645ea-110">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Creare un account")]</span><span class="sxs-lookup"><span data-stu-id="645ea-110">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]</span></span>

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="645ea-111">Account Batch con lo script di esempio della sottoscrizione utente</span><span class="sxs-lookup"><span data-stu-id="645ea-111">Batch account using user subscription sample script</span></span>

<span data-ttu-id="645ea-112">È possibile anche fare in modo che Batch crei i nodi di calcolo nella propria sottoscrizione di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="645ea-112">You can also opt to have Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="645ea-113">Gli account che allocano i nodi di calcolo nella propria sottoscrizione devono essere autenticati tramite un token di Azure Active Directory e i nodi di calcolo allocati verranno considerati ai fini della quota di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="645ea-113">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and the compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="645ea-114">Per creare un account in questa modalità, è necessario specificare un riferimento Key Vault durante la creazione dell'account.</span><span class="sxs-lookup"><span data-stu-id="645ea-114">To create an account in this mode, one must specify a Key Vault reference when creating the account.</span></span>

<span data-ttu-id="645ea-115">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Creare un account mediante una sottoscrizione utente")]</span><span class="sxs-lookup"><span data-stu-id="645ea-115">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="645ea-116">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="645ea-116">Clean up deployment</span></span>

<span data-ttu-id="645ea-117">Dopo l'esecuzione di uno degli script dell'esempio precedente, eseguire il comando seguente per rimuovere il gruppo di risorse e tutte le risorse correlate (inclusi gli account Batch, gli account di archiviazione di Azure e gli insiemi di credenziali delle chiavi di Azure).</span><span class="sxs-lookup"><span data-stu-id="645ea-117">After you run either of the above sample scripts, run the following command to remove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="645ea-118">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="645ea-118">Script explanation</span></span>

<span data-ttu-id="645ea-119">Questo script usa i comandi seguenti per creare un gruppo di risorse, l'account Batch e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="645ea-119">This script uses the following commands to create a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="645ea-120">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="645ea-120">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="645ea-121">Comando</span><span class="sxs-lookup"><span data-stu-id="645ea-121">Command</span></span> | <span data-ttu-id="645ea-122">Note</span><span class="sxs-lookup"><span data-stu-id="645ea-122">Notes</span></span> |
|---|---|
| [<span data-ttu-id="645ea-123">az group create</span><span class="sxs-lookup"><span data-stu-id="645ea-123">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="645ea-124">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="645ea-124">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="645ea-125">az batch account create</span><span class="sxs-lookup"><span data-stu-id="645ea-125">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="645ea-126">Crea l'account Batch.</span><span class="sxs-lookup"><span data-stu-id="645ea-126">Creates the Batch account.</span></span>  |
| [<span data-ttu-id="645ea-127">az batch account set</span><span class="sxs-lookup"><span data-stu-id="645ea-127">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="645ea-128">Aggiorna le proprietà dell'account Batch.</span><span class="sxs-lookup"><span data-stu-id="645ea-128">Updates properties of the Batch account.</span></span>  |
| [<span data-ttu-id="645ea-129">az batch account show</span><span class="sxs-lookup"><span data-stu-id="645ea-129">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="645ea-130">Recupera i dettagli dell'account Batch specificato.</span><span class="sxs-lookup"><span data-stu-id="645ea-130">Retrieves details of the specified Batch account.</span></span>  |
| [<span data-ttu-id="645ea-131">az batch account keys list</span><span class="sxs-lookup"><span data-stu-id="645ea-131">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="645ea-132">Recupera le chiavi d'accesso dell'account Batch specificato.</span><span class="sxs-lookup"><span data-stu-id="645ea-132">Retrieves the access keys of the specified Batch account.</span></span>  |
| [<span data-ttu-id="645ea-133">az batch account login</span><span class="sxs-lookup"><span data-stu-id="645ea-133">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="645ea-134">Effettua l'autenticazione con l'account Batch specificato per un'ulteriore interazione con l'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="645ea-134">Authenticates against the specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="645ea-135">az storage account create</span><span class="sxs-lookup"><span data-stu-id="645ea-135">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="645ea-136">Crea un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="645ea-136">Creates a storage account.</span></span> |
| [<span data-ttu-id="645ea-137">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="645ea-137">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="645ea-138">Crea un insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="645ea-138">Creates a key vault.</span></span> |
| [<span data-ttu-id="645ea-139">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="645ea-139">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="645ea-140">Aggiornare i criteri di sicurezza dell'insieme di credenziali delle chiavi specificato.</span><span class="sxs-lookup"><span data-stu-id="645ea-140">Update the security policy of the specified key vault.</span></span> |
| [<span data-ttu-id="645ea-141">az group delete</span><span class="sxs-lookup"><span data-stu-id="645ea-141">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="645ea-142">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="645ea-142">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="645ea-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="645ea-143">Next steps</span></span>

<span data-ttu-id="645ea-144">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="645ea-144">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="645ea-145">Altri esempi di script dell'interfaccia della riga di comando di Batch sono disponibili nella [documentazione dell'interfaccia della riga di comando di Azure Batch](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="645ea-145">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
