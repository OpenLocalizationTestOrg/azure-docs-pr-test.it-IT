---
title: 'aaaAzure CLI Script di esempio: creazione del Cluster Windows ACS Kubernetes | Documenti Microsoft'
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un cluster Kubernetes Windows del servizio contenitore di Azure
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
ms.openlocfilehash: afbaf17fb1d5310b50a2f181061339cb2ab87fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-container-service-kubernetes-windows-cluster"></a><span data-ttu-id="d5240-104">Creare un cluster Kubernetes Windows del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="d5240-104">Create an Azure Container Service Kubernetes Windows Cluster</span></span>

<span data-ttu-id="d5240-105">Questo esempio consente di creare un cluster del servizio contenitore di Azure che esegue Kubernetes per Windows.</span><span class="sxs-lookup"><span data-stu-id="d5240-105">This sample creates an Azure Container Service cluster running Kubernetes for Windows based containers.</span></span>

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d5240-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="d5240-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type kubernetes \
  --resource-group myResourceGroup \
  --name myK8SCluster \
  --generate-ssh-keys \
  --admin-username azureuser \
  --admin-password Password12 \
  --windows
```

## <a name="clean-up-deployment"></a><span data-ttu-id="d5240-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="d5240-107">Clean up deployment</span></span> 

<span data-ttu-id="d5240-108">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="d5240-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d5240-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="d5240-109">Script explanation</span></span>

<span data-ttu-id="d5240-110">Questo script utilizza hello dopo la distribuzione di comandi toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="d5240-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="d5240-111">Ogni elemento nella documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="d5240-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d5240-112">Comando</span><span class="sxs-lookup"><span data-stu-id="d5240-112">Command</span></span> | <span data-ttu-id="d5240-113">Note</span><span class="sxs-lookup"><span data-stu-id="d5240-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d5240-114">az group create</span><span class="sxs-lookup"><span data-stu-id="d5240-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d5240-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="d5240-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d5240-116">az acs create</span><span class="sxs-lookup"><span data-stu-id="d5240-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="d5240-117">Crea un cluster del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5240-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d5240-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d5240-118">Next steps</span></span>

<span data-ttu-id="d5240-119">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d5240-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d5240-120">Esempi di script aggiuntivi CLI servizio contenitore di Azure sono reperibile in hello [documentazione del servizio di contenitore di Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d5240-120">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>
