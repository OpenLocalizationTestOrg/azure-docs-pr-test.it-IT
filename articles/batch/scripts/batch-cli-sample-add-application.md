---
title: aaaAzure CLI Script di esempio - aggiungere un'applicazione in Batch | Documenti Microsoft
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
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a><span data-ttu-id="69e67-103">Aggiunta di applicazioni tooAzure Batch con l'interfaccia CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="69e67-103">Adding applications tooAzure Batch with Azure CLI</span></span>

<span data-ttu-id="69e67-104">Questo script viene illustrato come tooset di un'applicazione per l'utilizzo con un pool di Azure Batch o un'attività.</span><span class="sxs-lookup"><span data-stu-id="69e67-104">This script demonstrates how tooset up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="69e67-105">tooset di un'applicazione, il file eseguibile, insieme a eventuali dipendenze, in un file zip del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="69e67-105">tooset up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="69e67-106">In questo eseguibile zip hello di esempio viene chiamato file ' my-applicazione-exe.zip'.</span><span class="sxs-lookup"><span data-stu-id="69e67-106">In this example hello executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69e67-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="69e67-107">Prerequisites</span></span>

- <span data-ttu-id="69e67-108">Installazione hello CLI di Azure utilizzando istruzioni hello fornite nella hello [Guida all'installazione di Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), se non è già stato fatto.</span><span class="sxs-lookup"><span data-stu-id="69e67-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="69e67-109">Creare un account Batch, se non è già disponibile.</span><span class="sxs-lookup"><span data-stu-id="69e67-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="69e67-110">Vedere [creare un account Batch con hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) per uno script di esempio che crea un account.</span><span class="sxs-lookup"><span data-stu-id="69e67-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="69e67-111">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="69e67-111">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a><span data-ttu-id="69e67-112">Pulizia dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="69e67-112">Clean up application</span></span>

<span data-ttu-id="69e67-113">Dopo aver eseguito hello di sopra di script di esempio, eseguire hello tooremove comandi dopo l'applicazione e tutti i relativi pacchetti applicazione caricata.</span><span class="sxs-lookup"><span data-stu-id="69e67-113">After you run hello above sample script, run hello following commands tooremove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="69e67-114">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="69e67-114">Script explanation</span></span>

<span data-ttu-id="69e67-115">Questo script utilizza hello toocreate i comandi seguenti di un'applicazione e caricare un pacchetto di applicazione.</span><span class="sxs-lookup"><span data-stu-id="69e67-115">This script uses hello following commands toocreate an application and upload an application package.</span></span>
<span data-ttu-id="69e67-116">Ogni comando nella documentazione di hello tabella collegamenti toocommand specifica.</span><span class="sxs-lookup"><span data-stu-id="69e67-116">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="69e67-117">Comando</span><span class="sxs-lookup"><span data-stu-id="69e67-117">Command</span></span> | <span data-ttu-id="69e67-118">Note</span><span class="sxs-lookup"><span data-stu-id="69e67-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="69e67-119">az batch application create</span><span class="sxs-lookup"><span data-stu-id="69e67-119">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="69e67-120">Crea un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="69e67-120">Creates an application.</span></span>  |
| [<span data-ttu-id="69e67-121">az batch application set</span><span class="sxs-lookup"><span data-stu-id="69e67-121">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="69e67-122">Aggiorna le proprietà di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="69e67-122">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="69e67-123">az batch application package create</span><span class="sxs-lookup"><span data-stu-id="69e67-123">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="69e67-124">Aggiunge un toohello pacchetto di applicazione specificato dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="69e67-124">Adds an application package toohello specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="69e67-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="69e67-125">Next steps</span></span>

<span data-ttu-id="69e67-126">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="69e67-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="69e67-127">Ulteriori esempi di script Batch CLI sono reperibile in hello [documentazione CLI di Azure Batch](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="69e67-127">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
