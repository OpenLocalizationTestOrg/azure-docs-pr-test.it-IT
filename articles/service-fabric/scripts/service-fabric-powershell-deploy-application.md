---
title: Esempio di Script di PowerShell - aaaAzure distribuire cluster di applicazione tooa | Documenti Microsoft
description: 'Script di Azure PowerShell di esempio: distribuire un cluster di Service Fabric application tooa.'
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
ms.openlocfilehash: b417c9908c72f016e930c43ff2d13e0cc5451f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="3d569-103">Distribuire un cluster di Service Fabric tooa applicazione</span><span class="sxs-lookup"><span data-stu-id="3d569-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="3d569-104">Questo script di esempio copia di un archivio di immagini dell'applicazione pacchetto tooa cluster, registra il tipo di applicazione hello cluster hello e crea un'istanza di applicazione dal tipo di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3d569-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span>  <span data-ttu-id="3d569-105">Se servizi predefiniti sono stati definiti nel manifesto dell'applicazione hello del tipo di applicazione di destinazione hello, tali servizi vengono creati in questo momento.</span><span class="sxs-lookup"><span data-stu-id="3d569-105">If any default services were defined in hello application manifest of hello target application type, then those services are created at this time.</span></span> <span data-ttu-id="3d569-106">Personalizzare i parametri di hello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="3d569-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="3d569-107">Se necessario, installare il modulo di PowerShell di Service Fabric hello con hello [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3d569-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3d569-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="3d569-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3d569-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="3d569-109">Clean up deployment</span></span> 

<span data-ttu-id="3d569-110">Dopo l'esecuzione di script di esempio hello, hello script [rimuovere un'applicazione](service-fabric-powershell-remove-application.md) possono essere utilizzati tooremove istanza dell'applicazione hello, annullare la registrazione del tipo di applicazione hello ed eliminare il pacchetto di applicazione hello dall'archivio immagini hello.</span><span class="sxs-lookup"><span data-stu-id="3d569-110">After hello script sample has been run, hello script in [Remove an application](service-fabric-powershell-remove-application.md) can be used tooremove hello application instance, unregister hello application type, and delete hello application package from hello image store.</span></span>

## <a name="script-explanation"></a><span data-ttu-id="3d569-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="3d569-111">Script explanation</span></span>

<span data-ttu-id="3d569-112">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="3d569-112">This script uses hello following commands.</span></span> <span data-ttu-id="3d569-113">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="3d569-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3d569-114">Comando</span><span class="sxs-lookup"><span data-stu-id="3d569-114">Command</span></span> | <span data-ttu-id="3d569-115">Note</span><span class="sxs-lookup"><span data-stu-id="3d569-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3d569-116">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="3d569-116">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="3d569-117">Copiare un archivio di immagini dell'applicazione pacchetto toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="3d569-117">Copy an application package toohello cluster image store.</span></span>  |
|[<span data-ttu-id="3d569-118">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="3d569-118">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| <span data-ttu-id="3d569-119">Registra un tipo di applicazione e la versione in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3d569-119">Registers an application type and version on hello cluster.</span></span> |
|[<span data-ttu-id="3d569-120">New-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="3d569-120">New-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| <span data-ttu-id="3d569-121">Crea un'applicazione da un tipo di applicazione registrata.</span><span class="sxs-lookup"><span data-stu-id="3d569-121">Creates an application from a registered application type.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3d569-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3d569-122">Next steps</span></span>

<span data-ttu-id="3d569-123">Per ulteriori informazioni sul modulo PowerShell di Service Fabric hello, vedere [documentazione di Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="3d569-123">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="3d569-124">Ulteriori esempi di Powershell per Azure Service Fabric sono reperibile in hello [esempi di Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3d569-124">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
