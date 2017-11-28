---
title: Esempio di script di Azure PowerShell - Aggiornare un'applicazione di Service Fabric | Microsoft Docs
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
ms.openlocfilehash: 454849f82ddb23ddb9d71459f86e3cf5a1589254
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="upgrade-a-service-fabric-application"></a><span data-ttu-id="5c715-103">Aggiornare un'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5c715-103">Upgrade a Service Fabric application</span></span>

<span data-ttu-id="5c715-104">Questo script di esempio aggiorna un'istanza di applicazione di Service Fabric in esecuzione alla versione 1.3.0.</span><span class="sxs-lookup"><span data-stu-id="5c715-104">This sample script upgrades a running Service Fabric application instance to version 1.3.0.</span></span> <span data-ttu-id="5c715-105">Lo script copia il nuovo pacchetto di applicazione nell'archivio immagini del cluster, registra il tipo di applicazione, avvia un aggiornamento monitorato e controlla continuamente lo stato dell'aggiornamento fino a quando l'aggiornamento non viene completato o viene eseguito il rollback.</span><span class="sxs-lookup"><span data-stu-id="5c715-105">The script copies the new application package to the cluster image store, registers the application type, starts a monitored upgrade, and continuously checks the upgrade status until the upgrade completes or rolls back.</span></span> <span data-ttu-id="5c715-106">Personalizzare i parametri in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="5c715-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="5c715-107">Se necessario, installare il modulo PowerShell in Service Fabric con il [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5c715-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5c715-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="5c715-108">Sample script</span></span>

<span data-ttu-id="5c715-109">[!code-powershell[principale](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Aggiornare un'applicazione")]</span><span class="sxs-lookup"><span data-stu-id="5c715-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="5c715-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="5c715-110">Script explanation</span></span>

<span data-ttu-id="5c715-111">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="5c715-111">This script uses the following commands.</span></span> <span data-ttu-id="5c715-112">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="5c715-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5c715-113">Comando</span><span class="sxs-lookup"><span data-stu-id="5c715-113">Command</span></span> | <span data-ttu-id="5c715-114">Note</span><span class="sxs-lookup"><span data-stu-id="5c715-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5c715-115">Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="5c715-115">Get-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="5c715-116">Ottiene tutte le applicazioni del cluster di Service Fabric o un'applicazione specifica.</span><span class="sxs-lookup"><span data-stu-id="5c715-116">Gets all the applications in the Service Fabric cluster or a specific application.</span></span>  |
| [<span data-ttu-id="5c715-117">Get-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="5c715-117">Get-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="5c715-118">Ottiene lo stato dell'aggiornamento di un'applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5c715-118">Gets the status of a Service Fabric application upgrade.</span></span> |
| [<span data-ttu-id="5c715-119">Get-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="5c715-119">Get-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="5c715-120">Ottiene i tipi di applicazioni di Service Fabric registrate nel cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5c715-120">Gets the Service Fabric application types registered on the Service Fabric cluster.</span></span> |
| [<span data-ttu-id="5c715-121">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="5c715-121">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="5c715-122">Annulla la registrazione del tipo di applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5c715-122">Unregisters a Service Fabric application type.</span></span>  |
| [<span data-ttu-id="5c715-123">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="5c715-123">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="5c715-124">Copia il pacchetto dell'applicazione di Service Fabric nell'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="5c715-124">Copies a Service Fabric application package to the image store.</span></span>  |
| [<span data-ttu-id="5c715-125">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="5c715-125">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="5c715-126">Registra un tipo di applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5c715-126">Registers a Service Fabric application type.</span></span> |
| [<span data-ttu-id="5c715-127">Start-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="5c715-127">Start-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="5c715-128">Aggiorna un'applicazione di Service Fabric alla versione del tipo di applicazione specificata.</span><span class="sxs-lookup"><span data-stu-id="5c715-128">Upgrades a Service Fabric application to the specified application type version.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="5c715-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5c715-129">Next steps</span></span>

<span data-ttu-id="5c715-130">Per altre informazioni sul modulo PowerShell in Service Fabric, vedere la [documentazione di Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="5c715-130">For more information on the Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="5c715-131">Altri esempi di PowerShell per Azure Service Fabric sono disponibili in [Esempi di Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5c715-131">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
