---
title: Esempio di Script di PowerShell - aaaAzure aggiornare un'applicazione di Service Fabric | Documenti Microsoft
description: Esempio di script di Azure PowerShell - Aggiornare un'applicazione di Service Fabric.
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
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 4f4777607bd6b35a76029e09ddb441006565d4cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-service-fabric-application"></a><span data-ttu-id="00d70-103">Aggiornare un'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="00d70-103">Upgrade a Service Fabric application</span></span>

<span data-ttu-id="00d70-104">Questo script di esempio aggiorna un tooversion 1.3.0 istanza dell'applicazione in esecuzione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="00d70-104">This sample script upgrades a running Service Fabric application instance tooversion 1.3.0.</span></span> <span data-ttu-id="00d70-105">script Hello copia hello nuovo applicazione toohello cluster immagine archivio pacchetti, registra il tipo di applicazione hello, avvia un aggiornamento monitorato e controlla continuamente lo stato dell'aggiornamento hello fino a quando non viene completato l'aggiornamento di hello o il rollback.</span><span class="sxs-lookup"><span data-stu-id="00d70-105">hello script copies hello new application package toohello cluster image store, registers hello application type, starts a monitored upgrade, and continuously checks hello upgrade status until hello upgrade completes or rolls back.</span></span> <span data-ttu-id="00d70-106">Personalizzare i parametri di hello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="00d70-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="00d70-107">Se necessario, installare il modulo di PowerShell di Service Fabric hello con hello [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="00d70-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="00d70-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="00d70-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a><span data-ttu-id="00d70-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="00d70-109">Script explanation</span></span>

<span data-ttu-id="00d70-110">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="00d70-110">This script uses hello following commands.</span></span> <span data-ttu-id="00d70-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="00d70-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="00d70-112">Comando</span><span class="sxs-lookup"><span data-stu-id="00d70-112">Command</span></span> | <span data-ttu-id="00d70-113">Note</span><span class="sxs-lookup"><span data-stu-id="00d70-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="00d70-114">Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="00d70-114">Get-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="00d70-115">Ottiene tutte le applicazioni in cluster di Service Fabric hello hello o un'applicazione specifica.</span><span class="sxs-lookup"><span data-stu-id="00d70-115">Gets all hello applications in hello Service Fabric cluster or a specific application.</span></span>  |
| [<span data-ttu-id="00d70-116">Get-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="00d70-116">Get-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="00d70-117">Ottiene lo stato di hello di un aggiornamento dell'applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="00d70-117">Gets hello status of a Service Fabric application upgrade.</span></span> |
| [<span data-ttu-id="00d70-118">Get-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="00d70-118">Get-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="00d70-119">Ottiene i tipi di applicazioni di Service Fabric hello registrati nel cluster di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="00d70-119">Gets hello Service Fabric application types registered on hello Service Fabric cluster.</span></span> |
| [<span data-ttu-id="00d70-120">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="00d70-120">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="00d70-121">Annulla la registrazione del tipo di applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="00d70-121">Unregisters a Service Fabric application type.</span></span>  |
| [<span data-ttu-id="00d70-122">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="00d70-122">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="00d70-123">Copia un'immagine di toohello Service Fabric pacchetto dell'applicazione nell'archivio.</span><span class="sxs-lookup"><span data-stu-id="00d70-123">Copies a Service Fabric application package toohello image store.</span></span>  |
| [<span data-ttu-id="00d70-124">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="00d70-124">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="00d70-125">Registra un tipo di applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="00d70-125">Registers a Service Fabric application type.</span></span> |
| [<span data-ttu-id="00d70-126">Start-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="00d70-126">Start-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="00d70-127">Consente di aggiornare una versione di tipo Service Fabric applicazione toohello applicazione specificata.</span><span class="sxs-lookup"><span data-stu-id="00d70-127">Upgrades a Service Fabric application toohello specified application type version.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="00d70-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="00d70-128">Next steps</span></span>

<span data-ttu-id="00d70-129">Per ulteriori informazioni sul modulo PowerShell di Service Fabric hello, vedere [documentazione di Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="00d70-129">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="00d70-130">Ulteriori esempi di Powershell per Azure Service Fabric sono reperibile in hello [esempi di Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="00d70-130">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
