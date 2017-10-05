---
title: Esempio di script di Azure PowerShell - Creare un cluster di Service Fabric | Microsoft Docs
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
ms.openlocfilehash: 7cbeb3da695af3815ba660f9cc2e3388abb6f87d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-service-fabric-cluster"></a><span data-ttu-id="fd151-103">Creare un cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fd151-103">Create a Service Fabric cluster</span></span>

<span data-ttu-id="fd151-104">Questo script di esempio crea un cluster con cinque nodi di Service Fabric protetto con un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="fd151-104">This sample script creates a Service Fabric cluster a five-node cluster secured with an X.509 certificate.</span></span>  <span data-ttu-id="fd151-105">Il comando crea un certificato autofirmato e lo carica in un nuovo insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="fd151-105">The command creates a self-signed certificate and uploads it to a new key vault.</span></span> <span data-ttu-id="fd151-106">Il certificato viene copiato anche in una directory locale.</span><span class="sxs-lookup"><span data-stu-id="fd151-106">The certificate is also copied to a local directory.</span></span>  <span data-ttu-id="fd151-107">Impostare il parametro *-OS* per scegliere la versione di Windows o Linux che viene eseguita sui nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="fd151-107">Set the *-OS* parameter to choose the version of Windows or Linux that runs on the cluster nodes.</span></span>  <span data-ttu-id="fd151-108">Personalizzare i parametri in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="fd151-108">Customize the parameters as needed.</span></span>

<span data-ttu-id="fd151-109">Se necessario, installare Azure PowerShell usando l'istruzione presente nella [Guida di Azure PowerShell](/powershell/azure/overview) e quindi eseguire `Login-AzureRmAccount` per creare una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="fd151-109">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="fd151-110">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="fd151-110">Sample script</span></span>

<span data-ttu-id="fd151-111">[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Creare un cluster di Service Fabric")]</span><span class="sxs-lookup"><span data-stu-id="fd151-111">[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="fd151-112">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="fd151-112">Clean up deployment</span></span> 

<span data-ttu-id="fd151-113">Dopo avere eseguito lo script di esempio, usare il comando seguente per rimuovere il gruppo di risorse, il cluster e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="fd151-113">After the script sample has been run, the following command can be used to remove the resource group, cluster, and all related resources.</span></span>

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="fd151-114">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="fd151-114">Script explanation</span></span>

<span data-ttu-id="fd151-115">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="fd151-115">This script uses the following commands.</span></span> <span data-ttu-id="fd151-116">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="fd151-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fd151-117">Comando</span><span class="sxs-lookup"><span data-stu-id="fd151-117">Command</span></span> | <span data-ttu-id="fd151-118">Note</span><span class="sxs-lookup"><span data-stu-id="fd151-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fd151-119">New-AzureRmServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="fd151-119">New-AzureRmServiceFabricCluster</span></span>](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | <span data-ttu-id="fd151-120">Crea un nuovo cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fd151-120">Creates a new Service Fabric cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fd151-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fd151-121">Next steps</span></span>

<span data-ttu-id="fd151-122">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fd151-122">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="fd151-123">Altri esempi di Azure PowerShell per Azure Service Fabric sono disponibili in [Esempi di Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fd151-123">Additional Azure Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
