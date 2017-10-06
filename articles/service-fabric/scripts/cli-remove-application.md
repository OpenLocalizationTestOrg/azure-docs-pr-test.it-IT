---
title: aaaAzure esempio rimuovere Script del servizio dell'infrastruttura CLI
description: Rimuovere un'applicazione da un cluster di Azure Service Fabric utilizzando hello CLI di Azure Service Fabric
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
ms.openlocfilehash: 3ccefd4a04c5b7af71a2f959e11da6e402f25881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="5951d-103">Rimuovere un'applicazione da un cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5951d-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="5951d-104">Questo script di esempio elimina un'istanza di applicazione di Service Fabric in esecuzione, Annulla la registrazione di un tipo di applicazione e la versione dal cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5951d-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster.</span></span>  <span data-ttu-id="5951d-105">Istanza dell'applicazione hello eliminazione elimina inoltre hello tutte le istanze del servizio associata all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5951d-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="5951d-106">Successivamente, i file dell'applicazione hello vengono eliminati dall'archivio immagini hello.</span><span class="sxs-lookup"><span data-stu-id="5951d-106">Next, hello application files are deleted from hello image store.</span></span> 

<span data-ttu-id="5951d-107">Se necessario, installare hello [servizio infrastruttura CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5951d-107">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="5951d-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="5951d-108">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]

## <a name="next-steps"></a><span data-ttu-id="5951d-109">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5951d-109">Next steps</span></span>

<span data-ttu-id="5951d-110">Per ulteriori informazioni, vedere hello [documentazione servizio infrastruttura CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5951d-110">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="5951d-111">Esempi aggiuntivi di servizio dell'infrastruttura CLI per Azure Service Fabric sono reperibile in hello [esempi del servizio dell'infrastruttura CLI](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5951d-111">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
