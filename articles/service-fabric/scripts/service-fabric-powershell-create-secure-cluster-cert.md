---
title: aaaAzure Script di PowerShell di esempio - creare un cluster di Service Fabric | Documenti Microsoft
description: Esempio di script di Azure PowerShell - Creare un cluster di Service Fabric.
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 12fdc201bd51688cb850cd456b1e00442b79c22d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster"></a><span data-ttu-id="e8bcb-103">Creare un cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e8bcb-103">Create a Service Fabric cluster</span></span>

<span data-ttu-id="e8bcb-104">Questo script di esempio crea un cluster con cinque nodi di Service Fabric protetto con un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="e8bcb-104">This sample script creates a Service Fabric cluster a five-node cluster secured with an X.509 certificate.</span></span>  <span data-ttu-id="e8bcb-105">comando Hello crea un certificato autofirmato e caricarlo tooa nuovo insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="e8bcb-105">hello command creates a self-signed certificate and uploads it tooa new key vault.</span></span> <span data-ttu-id="e8bcb-106">certificato Hello è anche la directory locale tooa copiato.</span><span class="sxs-lookup"><span data-stu-id="e8bcb-106">hello certificate is also copied tooa local directory.</span></span>  <span data-ttu-id="e8bcb-107">Set hello *-OS* versione di hello toochoose parametri di Windows o Linux, che viene eseguito sui nodi del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e8bcb-107">Set hello *-OS* parameter toochoose hello version of Windows or Linux that runs on hello cluster nodes.</span></span>  <span data-ttu-id="e8bcb-108">Personalizzare i parametri di hello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="e8bcb-108">Customize hello parameters as needed.</span></span>

<span data-ttu-id="e8bcb-109">Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](/powershell/azure/overview) e quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="e8bcb-109">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e8bcb-110">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="e8bcb-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e8bcb-111">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="e8bcb-111">Clean up deployment</span></span> 

<span data-ttu-id="e8bcb-112">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello, cluster e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="e8bcb-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, cluster, and all related resources.</span></span>

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="e8bcb-113">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="e8bcb-113">Script explanation</span></span>

<span data-ttu-id="e8bcb-114">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="e8bcb-114">This script uses hello following commands.</span></span> <span data-ttu-id="e8bcb-115">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="e8bcb-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e8bcb-116">Comando</span><span class="sxs-lookup"><span data-stu-id="e8bcb-116">Command</span></span> | <span data-ttu-id="e8bcb-117">Note</span><span class="sxs-lookup"><span data-stu-id="e8bcb-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e8bcb-118">New-AzureRmServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="e8bcb-118">New-AzureRmServiceFabricCluster</span></span>](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | <span data-ttu-id="e8bcb-119">Crea un nuovo cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e8bcb-119">Creates a new Service Fabric cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e8bcb-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e8bcb-120">Next steps</span></span>

<span data-ttu-id="e8bcb-121">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e8bcb-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e8bcb-122">Esempi aggiuntivi di Azure Powershell per Azure Service Fabric sono reperibile in hello [esempi di Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e8bcb-122">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
