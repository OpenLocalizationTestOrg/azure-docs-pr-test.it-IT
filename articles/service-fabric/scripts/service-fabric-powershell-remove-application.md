---
title: Esempio di script di Azure PowerShell - Rimuovere un'applicazione da un cluster | Microsoft Docs
description: Esempio di script di Azure PowerShell - Rimuovere un'applicazione da un cluster di Service Fabric.
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 05851132c7e5e5877884d29f04bce6c0717ce411
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="2cdc4-103">Rimuovere un'applicazione da un cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2cdc4-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="2cdc4-104">Questo script di esempio elimina un'istanza di applicazione di Service Fabric in esecuzione, annulla la registrazione di un tipo di applicazione e della versione dal cluster ed elimina il pacchetto dell'applicazione dall'archivio immagini del cluster.</span><span class="sxs-lookup"><span data-stu-id="2cdc4-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from the cluster, and deletes the application package from the cluster image store.</span></span>  <span data-ttu-id="2cdc4-105">L'eliminazione dell'istanza dell'applicazione elimina anche tutte le istanze del servizio associate a questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="2cdc4-105">Deleting the application instance also deletes all the running service instances associated with that application.</span></span> <span data-ttu-id="2cdc4-106">Personalizzare i parametri in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="2cdc4-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="2cdc4-107">Se necessario, installare il modulo PowerShell in Service Fabric con il [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2cdc4-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="2cdc4-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="2cdc4-108">Sample script</span></span>

<span data-ttu-id="2cdc4-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Rimuovere un'applicazione da un cluster")]</span><span class="sxs-lookup"><span data-stu-id="2cdc4-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="2cdc4-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="2cdc4-110">Script explanation</span></span>

<span data-ttu-id="2cdc4-111">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="2cdc4-111">This script uses the following commands.</span></span> <span data-ttu-id="2cdc4-112">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="2cdc4-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2cdc4-113">Comando</span><span class="sxs-lookup"><span data-stu-id="2cdc4-113">Command</span></span> | <span data-ttu-id="2cdc4-114">Note</span><span class="sxs-lookup"><span data-stu-id="2cdc4-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2cdc4-115">Remove-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="2cdc4-115">Remove-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="2cdc4-116">Rimuove un'istanza di applicazione di Service Fabric in esecuzione dal cluster.</span><span class="sxs-lookup"><span data-stu-id="2cdc4-116">Removes a running Service Fabric application instance from the cluster.</span></span>  |
| [<span data-ttu-id="2cdc4-117">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="2cdc4-117">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="2cdc4-118">Annulla la registrazione di un tipo e una versione di applicazione di Service Fabric dal cluster.</span><span class="sxs-lookup"><span data-stu-id="2cdc4-118">Unregisters a Service Fabric application type and version from the cluster.</span></span> |
| [<span data-ttu-id="2cdc4-119">Remove-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="2cdc4-119">Remove-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="2cdc4-120">Rimuove il pacchetto dell'applicazione di Service Fabric dall'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="2cdc4-120">Removes a Service Fabric application package from the image store.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="2cdc4-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2cdc4-121">Next steps</span></span>

<span data-ttu-id="2cdc4-122">Per altre informazioni sul modulo PowerShell in Service Fabric, vedere la [documentazione di Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="2cdc4-122">For more information on the Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="2cdc4-123">Altri esempi di PowerShell per Azure Service Fabric sono disponibili in [Esempi di Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2cdc4-123">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
