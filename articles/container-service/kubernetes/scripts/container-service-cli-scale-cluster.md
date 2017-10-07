---
title: aaaAzure CLI Script di esempio - scala di un Cluster ACS | Documenti Microsoft
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
ms.openlocfilehash: 1e07518fc2ca67476d9ef64bb22d75f848a37e43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="f6b60-104">Ridimensionare un cluster del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="f6b60-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="f6b60-105">Questo esempio ridimensiona un cluster del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6b60-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f6b60-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="f6b60-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="f6b60-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="f6b60-107">Clean up deployment</span></span> 

<span data-ttu-id="f6b60-108">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="f6b60-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f6b60-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="f6b60-109">Script explanation</span></span>

<span data-ttu-id="f6b60-110">Questo script utilizza hello dopo la distribuzione di comandi toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="f6b60-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="f6b60-111">Ogni elemento nella documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="f6b60-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f6b60-112">Comando</span><span class="sxs-lookup"><span data-stu-id="f6b60-112">Command</span></span> | <span data-ttu-id="f6b60-113">Note</span><span class="sxs-lookup"><span data-stu-id="f6b60-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f6b60-114">az acs scale</span><span class="sxs-lookup"><span data-stu-id="f6b60-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="f6b60-115">Ridimensionare un cluster del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6b60-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f6b60-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f6b60-116">Next steps</span></span>

<span data-ttu-id="f6b60-117">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f6b60-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f6b60-118">Esempi di script aggiuntivi CLI servizio contenitore di Azure sono reperibile in hello [documentazione del servizio di contenitore di Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f6b60-118">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>

