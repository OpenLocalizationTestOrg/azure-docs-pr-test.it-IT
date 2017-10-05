---
title: Esempio di script di Azure PowerShell - Distribuire un'applicazione in un cluster | Microsoft Docs
description: 'Esempio di script di Azure PowerShell: Distribuire un''applicazione in un cluster di Service Fabric.'
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
ms.openlocfilehash: 2863823205dbd70f63948ecd4af8898220fe1ff8
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="deploy-an-application-to-a-service-fabric-cluster"></a><span data-ttu-id="9fcf6-103">Distribuire un'applicazione in un cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9fcf6-103">Deploy an application to a Service Fabric cluster</span></span>

<span data-ttu-id="9fcf6-104">Questo script di esempio copia un pacchetto dell'applicazione in un archivio immagini del cluster, registra il tipo di applicazione nel cluster e crea un'istanza di applicazione dal tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="9fcf6-104">This sample script copies an application package to a cluster image store, registers the application type in the cluster, and creates an application instance from the application type.</span></span>  <span data-ttu-id="9fcf6-105">Se nel manifesto dell'applicazione del tipo di applicazione di destinazione sono specificati servizi predefiniti, questi verranno creati in questa fase.</span><span class="sxs-lookup"><span data-stu-id="9fcf6-105">If any default services were defined in the application manifest of the target application type, then those services are created at this time.</span></span> <span data-ttu-id="9fcf6-106">Personalizzare i parametri in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="9fcf6-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="9fcf6-107">Se necessario, installare il modulo PowerShell in Service Fabric con il [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9fcf6-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="9fcf6-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="9fcf6-108">Sample script</span></span>

<span data-ttu-id="9fcf6-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Distribuire un'applicazione in un cluster")]</span><span class="sxs-lookup"><span data-stu-id="9fcf6-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application to a cluster")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="9fcf6-110">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="9fcf6-110">Clean up deployment</span></span> 

<span data-ttu-id="9fcf6-111">Dopo l'esecuzione dell'esempio di script, lo script in [Rimuovere un'applicazione](service-fabric-powershell-remove-application.md) può essere usato per rimuovere l'istanza dell'applicazione, annullare la registrazione del tipo di applicazione ed eliminare il pacchetto dell'applicazione dall'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="9fcf6-111">After the script sample has been run, the script in [Remove an application](service-fabric-powershell-remove-application.md) can be used to remove the application instance, unregister the application type, and delete the application package from the image store.</span></span>

## <a name="script-explanation"></a><span data-ttu-id="9fcf6-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="9fcf6-112">Script explanation</span></span>

<span data-ttu-id="9fcf6-113">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="9fcf6-113">This script uses the following commands.</span></span> <span data-ttu-id="9fcf6-114">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="9fcf6-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9fcf6-115">Comando</span><span class="sxs-lookup"><span data-stu-id="9fcf6-115">Command</span></span> | <span data-ttu-id="9fcf6-116">Note</span><span class="sxs-lookup"><span data-stu-id="9fcf6-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9fcf6-117">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="9fcf6-117">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="9fcf6-118">Copiare un pacchetto dell'applicazione nell'archivio immagini del cluster.</span><span class="sxs-lookup"><span data-stu-id="9fcf6-118">Copy an application package to the cluster image store.</span></span>  |
|[<span data-ttu-id="9fcf6-119">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="9fcf6-119">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| <span data-ttu-id="9fcf6-120">Registra un tipo di applicazione e la versione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="9fcf6-120">Registers an application type and version on the cluster.</span></span> |
|[<span data-ttu-id="9fcf6-121">New-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="9fcf6-121">New-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| <span data-ttu-id="9fcf6-122">Crea un'applicazione da un tipo di applicazione registrata.</span><span class="sxs-lookup"><span data-stu-id="9fcf6-122">Creates an application from a registered application type.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9fcf6-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9fcf6-123">Next steps</span></span>

<span data-ttu-id="9fcf6-124">Per altre informazioni sul modulo PowerShell in Service Fabric, vedere la [documentazione di Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="9fcf6-124">For more information on the Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="9fcf6-125">Altri esempi di PowerShell per Azure Service Fabric sono disponibili in [Esempi di Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9fcf6-125">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
