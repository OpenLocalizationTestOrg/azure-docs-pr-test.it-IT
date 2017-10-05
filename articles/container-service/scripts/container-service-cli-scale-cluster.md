---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Ridimensionare un cluster del servizio contenitore di Azure | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Ridimensionare un cluster del servizio contenitore di Azure
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenitori, Micro-Service, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: nepeters
ms.openlocfilehash: 0ea2c73436e650fdb37535538baccc565369fa9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="75555-104">Ridimensionare un cluster del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="75555-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="75555-105">Questo esempio ridimensiona un cluster del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="75555-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="75555-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="75555-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="75555-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="75555-107">Clean up deployment</span></span> 

<span data-ttu-id="75555-108">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="75555-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="75555-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="75555-109">Script explanation</span></span>

<span data-ttu-id="75555-110">Questo script usa i comandi seguenti per creare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="75555-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="75555-111">Ogni elemento della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="75555-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="75555-112">Comando</span><span class="sxs-lookup"><span data-stu-id="75555-112">Command</span></span> | <span data-ttu-id="75555-113">Note</span><span class="sxs-lookup"><span data-stu-id="75555-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="75555-114">az acs scale</span><span class="sxs-lookup"><span data-stu-id="75555-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="75555-115">Ridimensionare un cluster del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="75555-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="75555-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="75555-116">Next steps</span></span>

<span data-ttu-id="75555-117">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="75555-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="75555-118">Altri esempi di script dell'interfaccia della riga di comando del servizio contenitore di Azure sono disponibili nella [documentazione del servizio contenitore di Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="75555-118">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>

