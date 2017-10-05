---
title: Esempio di rimozione di script dell'interfaccia della riga di comando di Azure Service Fabric
description: Rimuovere un'applicazione da un cluster di Azure Service Fabric usando l'interfaccia della riga di comando di Azure Service Fabric
services: service-fabric
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: d86f195d2c37a71e476c5ba4eec040dd46931d23
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="d4f24-103">Rimuovere un'applicazione da un cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d4f24-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="d4f24-104">Questo script di esempio elimina un'istanza di applicazione di Service Fabric in esecuzione, annulla la registrazione di un tipo di applicazione e della versione dal cluster.</span><span class="sxs-lookup"><span data-stu-id="d4f24-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from the cluster.</span></span>  <span data-ttu-id="d4f24-105">L'eliminazione dell'istanza dell'applicazione elimina anche tutte le istanze del servizio associate a questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="d4f24-105">Deleting the application instance also deletes all the running service instances associated with that application.</span></span> <span data-ttu-id="d4f24-106">I file dell'applicazione vengono quindi eliminati dall'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="d4f24-106">Next, the application files are deleted from the image store.</span></span> 

<span data-ttu-id="d4f24-107">Se necessario, installare l'[interfaccia della riga di comando di Service Fabric](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d4f24-107">If needed, install the [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="d4f24-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="d4f24-108">Sample script</span></span>

<span data-ttu-id="d4f24-109">[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Rimuovere un'applicazione da un cluster")]</span><span class="sxs-lookup"><span data-stu-id="d4f24-109">[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4f24-110">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d4f24-110">Next steps</span></span>

<span data-ttu-id="d4f24-111">Per altre informazioni, vedere la [documentazione sull'interfaccia della riga di comando di Service Fabric](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d4f24-111">For more information, see the [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="d4f24-112">Altri esempi dell'interfaccia della riga di comando di Service Fabric per Azure Service Fabric sono disponibili negli [esempi dell'interfaccia della riga di comando di Service Fabric](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d4f24-112">Additional Service Fabric CLI samples for Azure Service Fabric can be found in the [Service Fabric CLI samples](../samples-cli.md).</span></span>
