---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Aggiungere un'applicazione a Batch | Documentazione Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Aggiungere un'applicazione a Batch
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
ms.openlocfilehash: 5d057eaf32867aedc95d58c5185e2be1f9385ec0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="adding-applications-to-azure-batch-with-azure-cli"></a><span data-ttu-id="d34a0-103">Aggiunta di applicazioni ad Azure Batch con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="d34a0-103">Adding applications to Azure Batch with Azure CLI</span></span>

<span data-ttu-id="d34a0-104">Questo script illustra come configurare un'applicazione per l'uso con un pool è un'attività di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="d34a0-104">This script demonstrates how to set up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="d34a0-105">Per configurare un'applicazione, creare il pacchetto dell'eseguibile, insieme a eventuali dipendenze, come file .zip.</span><span class="sxs-lookup"><span data-stu-id="d34a0-105">To set up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="d34a0-106">In questo esempio il file zip eseguibile è chiamato "my-application-exe.zip".</span><span class="sxs-lookup"><span data-stu-id="d34a0-106">In this example the executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d34a0-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d34a0-107">Prerequisites</span></span>

- <span data-ttu-id="d34a0-108">Installare l'interfaccia della riga di comando di Azure usando le istruzioni presenti nella [Guida all'installazione dell'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), se questa operazione non è stata ancora eseguita.</span><span class="sxs-lookup"><span data-stu-id="d34a0-108">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="d34a0-109">Creare un account Batch, se non è già disponibile.</span><span class="sxs-lookup"><span data-stu-id="d34a0-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="d34a0-110">Vedere [Creare un account Batch con l'interfaccia della riga di comando di Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) per uno script di esempio che crea un account.</span><span class="sxs-lookup"><span data-stu-id="d34a0-110">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="d34a0-111">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="d34a0-111">Sample script</span></span>

<span data-ttu-id="d34a0-112">[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Aggiungi applicazione")]</span><span class="sxs-lookup"><span data-stu-id="d34a0-112">[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]</span></span>

## <a name="clean-up-application"></a><span data-ttu-id="d34a0-113">Pulizia dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="d34a0-113">Clean up application</span></span>

<span data-ttu-id="d34a0-114">Dopo aver eseguito lo script di esempio precedente, eseguire i comandi seguenti per rimuovere l'applicazione e tutti i relativi pacchetti dell'applicazione caricati.</span><span class="sxs-lookup"><span data-stu-id="d34a0-114">After you run the above sample script, run the following commands to remove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="d34a0-115">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="d34a0-115">Script explanation</span></span>

<span data-ttu-id="d34a0-116">Questo script usa i comandi seguenti per creare un'applicazione e caricare un pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d34a0-116">This script uses the following commands to create an application and upload an application package.</span></span>
<span data-ttu-id="d34a0-117">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="d34a0-117">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="d34a0-118">Comando</span><span class="sxs-lookup"><span data-stu-id="d34a0-118">Command</span></span> | <span data-ttu-id="d34a0-119">Note</span><span class="sxs-lookup"><span data-stu-id="d34a0-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d34a0-120">az batch application create</span><span class="sxs-lookup"><span data-stu-id="d34a0-120">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="d34a0-121">Crea un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d34a0-121">Creates an application.</span></span>  |
| [<span data-ttu-id="d34a0-122">az batch application set</span><span class="sxs-lookup"><span data-stu-id="d34a0-122">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="d34a0-123">Aggiorna le proprietà di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d34a0-123">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="d34a0-124">az batch application package create</span><span class="sxs-lookup"><span data-stu-id="d34a0-124">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="d34a0-125">Aggiunge un pacchetto di applicazione per l'applicazione specificata.</span><span class="sxs-lookup"><span data-stu-id="d34a0-125">Adds an application package to the specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="d34a0-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d34a0-126">Next steps</span></span>

<span data-ttu-id="d34a0-127">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d34a0-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d34a0-128">Altri esempi di script dell'interfaccia della riga di comando di Batch sono disponibili nella [documentazione dell'interfaccia della riga di comando di Azure Batch](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d34a0-128">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
