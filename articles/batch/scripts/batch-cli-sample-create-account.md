---
title: aaaAzure CLI Script di esempio - creare un account Batch | Documenti Microsoft
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
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a><span data-ttu-id="ab7eb-103">Creare un account Batch con hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="ab7eb-103">Create a Batch account with hello Azure CLI</span></span>

<span data-ttu-id="ab7eb-104">Questo script crea un account Azure Batch e viene illustrato come le varie proprietà dell'account di hello possono eseguire query e aggiornate.</span><span class="sxs-lookup"><span data-stu-id="ab7eb-104">This script creates an Azure Batch account and shows how various properties of hello account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab7eb-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ab7eb-105">Prerequisites</span></span>

<span data-ttu-id="ab7eb-106">Installazione hello CLI di Azure utilizzando istruzioni hello fornite nella hello [Guida all'installazione di Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), se non è già stato fatto.</span><span class="sxs-lookup"><span data-stu-id="ab7eb-106">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="ab7eb-107">Script di esempio per un account Batch</span><span class="sxs-lookup"><span data-stu-id="ab7eb-107">Batch account sample script</span></span>

<span data-ttu-id="ab7eb-108">Quando si crea un account Batch, per impostazione predefinita i relativi nodi calcolo assegnati internamente dal servizio Batch hello.</span><span class="sxs-lookup"><span data-stu-id="ab7eb-108">When you create a Batch account, by default its compute nodes are assigned internally by hello Batch service.</span></span> <span data-ttu-id="ab7eb-109">Nodi di calcolo allocato sarà una quota di core separato tooa soggetto e account hello possono essere autenticati tramite le credenziali di autenticazione chiave condivisa o un token di Azure Active deve.</span><span class="sxs-lookup"><span data-stu-id="ab7eb-109">Allocated compute nodes will be subject tooa separate core quota and hello account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="ab7eb-110">Account Batch con lo script di esempio della sottoscrizione utente</span><span class="sxs-lookup"><span data-stu-id="ab7eb-110">Batch account using user subscription sample script</span></span>

<span data-ttu-id="ab7eb-111">È inoltre possibile scegliere toohave Batch creare nodi di calcolo nella sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7eb-111">You can also opt toohave Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="ab7eb-112">Gli account che allocano calcolano nodi nella sottoscrizione devono essere autenticati tramite un token di Azure Active Directory e i nodi di calcolo hello allocati verranno considerato come uno la quota della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ab7eb-112">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and hello compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="ab7eb-113">toocreate un account in questa modalità, uno deve specificare un riferimento di chiave dell'insieme di credenziali durante la creazione di account hello.</span><span class="sxs-lookup"><span data-stu-id="ab7eb-113">toocreate an account in this mode, one must specify a Key Vault reference when creating hello account.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ab7eb-114">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="ab7eb-114">Clean up deployment</span></span>

<span data-ttu-id="ab7eb-115">Dopo aver eseguito uno di hello sopra gli script di esempio, eseguire hello successivo comando tooremove il gruppo di risorse e tutte le relative risorse (inclusi gli account Batch, gli account di archiviazione di Azure e insiemi di credenziali chiave di Azure).</span><span class="sxs-lookup"><span data-stu-id="ab7eb-115">After you run either of hello above sample scripts, run hello following command tooremove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ab7eb-116">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="ab7eb-116">Script explanation</span></span>

<span data-ttu-id="ab7eb-117">Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, l'account di Batch e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="ab7eb-117">This script uses hello following commands toocreate a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="ab7eb-118">Ogni comando nella documentazione di hello tabella collegamenti toocommand specifica.</span><span class="sxs-lookup"><span data-stu-id="ab7eb-118">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="ab7eb-119">Comando</span><span class="sxs-lookup"><span data-stu-id="ab7eb-119">Command</span></span> | <span data-ttu-id="ab7eb-120">Note</span><span class="sxs-lookup"><span data-stu-id="ab7eb-120">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ab7eb-121">az group create</span><span class="sxs-lookup"><span data-stu-id="ab7eb-121">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ab7eb-122">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="ab7eb-122">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ab7eb-123">az batch account create</span><span class="sxs-lookup"><span data-stu-id="ab7eb-123">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="ab7eb-124">Crea account Batch hello.</span><span class="sxs-lookup"><span data-stu-id="ab7eb-124">Creates hello Batch account.</span></span>  |
| [<span data-ttu-id="ab7eb-125">az batch account set</span><span class="sxs-lookup"><span data-stu-id="ab7eb-125">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="ab7eb-126">Aggiorna le proprietà di hello account Batch.</span><span class="sxs-lookup"><span data-stu-id="ab7eb-126">Updates properties of hello Batch account.</span></span>  |
| [<span data-ttu-id="ab7eb-127">az batch account show</span><span class="sxs-lookup"><span data-stu-id="ab7eb-127">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="ab7eb-128">Recupera i dettagli di hello specificato l'account Batch.</span><span class="sxs-lookup"><span data-stu-id="ab7eb-128">Retrieves details of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="ab7eb-129">az batch account keys list</span><span class="sxs-lookup"><span data-stu-id="ab7eb-129">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="ab7eb-130">Recupera le chiavi di accesso hello di hello specificato l'account Batch.</span><span class="sxs-lookup"><span data-stu-id="ab7eb-130">Retrieves hello access keys of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="ab7eb-131">az batch account login</span><span class="sxs-lookup"><span data-stu-id="ab7eb-131">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="ab7eb-132">Esegue l'autenticazione con hello specificato per l'interazione di CLI ulteriormente l'account Batch.</span><span class="sxs-lookup"><span data-stu-id="ab7eb-132">Authenticates against hello specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="ab7eb-133">az storage account create</span><span class="sxs-lookup"><span data-stu-id="ab7eb-133">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="ab7eb-134">Crea un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ab7eb-134">Creates a storage account.</span></span> |
| [<span data-ttu-id="ab7eb-135">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="ab7eb-135">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="ab7eb-136">Crea un insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="ab7eb-136">Creates a key vault.</span></span> |
| [<span data-ttu-id="ab7eb-137">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="ab7eb-137">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="ab7eb-138">Aggiornare i criteri di sicurezza hello dell'insieme di credenziali di chiave specificato hello.</span><span class="sxs-lookup"><span data-stu-id="ab7eb-138">Update hello security policy of hello specified key vault.</span></span> |
| [<span data-ttu-id="ab7eb-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="ab7eb-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="ab7eb-140">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="ab7eb-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ab7eb-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ab7eb-141">Next steps</span></span>

<span data-ttu-id="ab7eb-142">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ab7eb-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ab7eb-143">Ulteriori esempi di script Batch CLI sono reperibile in hello [documentazione CLI di Azure Batch](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ab7eb-143">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
