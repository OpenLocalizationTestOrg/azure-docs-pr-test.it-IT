---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un cluster Kubernetes Windows del servizio contenitore di Azure | Microsoft Docs
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
ms.openlocfilehash: 9ca289817b54c39c59271f35a0af26bad2811da6
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="create-an-azure-container-service-kubernetes-windows-cluster"></a><span data-ttu-id="010f4-104">Creare un cluster Kubernetes Windows del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="010f4-104">Create an Azure Container Service Kubernetes Windows Cluster</span></span>

<span data-ttu-id="010f4-105">Questo esempio consente di creare un cluster del servizio contenitore di Azure che esegue Kubernetes per Windows.</span><span class="sxs-lookup"><span data-stu-id="010f4-105">This sample creates an Azure Container Service cluster running Kubernetes for Windows based containers.</span></span>

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="010f4-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="010f4-106">Sample script</span></span>

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

## <a name="clean-up-deployment"></a><span data-ttu-id="010f4-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="010f4-107">Clean up deployment</span></span> 

<span data-ttu-id="010f4-108">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="010f4-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="010f4-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="010f4-109">Script explanation</span></span>

<span data-ttu-id="010f4-110">Questo script usa i comandi seguenti per creare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="010f4-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="010f4-111">Ogni elemento della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="010f4-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="010f4-112">Comando</span><span class="sxs-lookup"><span data-stu-id="010f4-112">Command</span></span> | <span data-ttu-id="010f4-113">Note</span><span class="sxs-lookup"><span data-stu-id="010f4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="010f4-114">az group create</span><span class="sxs-lookup"><span data-stu-id="010f4-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="010f4-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="010f4-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="010f4-116">az acs create</span><span class="sxs-lookup"><span data-stu-id="010f4-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="010f4-117">Crea un cluster del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="010f4-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="010f4-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="010f4-118">Next steps</span></span>

<span data-ttu-id="010f4-119">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="010f4-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="010f4-120">Altri esempi di script dell'interfaccia della riga di comando del servizio contenitore di Azure sono disponibili nella [documentazione del servizio contenitore di Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="010f4-120">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>
