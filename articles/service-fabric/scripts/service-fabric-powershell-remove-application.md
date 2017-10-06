---
title: Esempio di Script di PowerShell - Rimuovi applicazione da un cluster aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: 3fe2082c2fbeffbff1622f206021d4d907197d19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="f63a1-103">Rimuovere un'applicazione da un cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f63a1-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="f63a1-104">Questo script di esempio elimina un'istanza di applicazione di Service Fabric in esecuzione, Annulla la registrazione di un tipo di applicazione e la versione dal cluster hello e pacchetto dell'applicazione hello dall'archivio di immagini cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f63a1-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster, and deletes hello application package from hello cluster image store.</span></span>  <span data-ttu-id="f63a1-105">Istanza dell'applicazione hello eliminazione elimina inoltre hello tutte le istanze del servizio associata all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f63a1-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="f63a1-106">Personalizzare i parametri di hello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="f63a1-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="f63a1-107">Se necessario, installare il modulo di PowerShell di Service Fabric hello con hello [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f63a1-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f63a1-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="f63a1-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a><span data-ttu-id="f63a1-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="f63a1-109">Script explanation</span></span>

<span data-ttu-id="f63a1-110">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="f63a1-110">This script uses hello following commands.</span></span> <span data-ttu-id="f63a1-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="f63a1-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f63a1-112">Comando</span><span class="sxs-lookup"><span data-stu-id="f63a1-112">Command</span></span> | <span data-ttu-id="f63a1-113">Note</span><span class="sxs-lookup"><span data-stu-id="f63a1-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f63a1-114">Remove-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="f63a1-114">Remove-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="f63a1-115">Rimuove un'istanza di applicazione di Service Fabric in esecuzione dal cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f63a1-115">Removes a running Service Fabric application instance from hello cluster.</span></span>  |
| [<span data-ttu-id="f63a1-116">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="f63a1-116">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="f63a1-117">Annulla la registrazione di un tipo di applicazione di Service Fabric e una versione da cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f63a1-117">Unregisters a Service Fabric application type and version from hello cluster.</span></span> |
| [<span data-ttu-id="f63a1-118">Remove-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="f63a1-118">Remove-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="f63a1-119">Rimuove un pacchetto di applicazione di Service Fabric dall'archivio immagini hello.</span><span class="sxs-lookup"><span data-stu-id="f63a1-119">Removes a Service Fabric application package from hello image store.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="f63a1-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f63a1-120">Next steps</span></span>

<span data-ttu-id="f63a1-121">Per ulteriori informazioni sul modulo PowerShell di Service Fabric hello, vedere [documentazione di Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="f63a1-121">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="f63a1-122">Ulteriori esempi di Powershell per Azure Service Fabric sono reperibile in hello [esempi di Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f63a1-122">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
