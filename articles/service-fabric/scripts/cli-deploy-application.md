---
title: aaaAzure esempio distribuire uno Script del servizio dell'infrastruttura CLI
description: Distribuire un cluster di Azure Service Fabric tooan applicazione utilizzando hello CLI di Azure Service Fabric
services: service-fabric
documentationcenter: 
author: Thraka
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
ms.openlocfilehash: aaec7042a4fd7ed32ad706cde70361f23d18fb48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="a07be-103">Distribuire un cluster di Service Fabric tooa applicazione</span><span class="sxs-lookup"><span data-stu-id="a07be-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="a07be-104">Questo script di esempio copia di un archivio di immagini dell'applicazione pacchetto tooa cluster, registra il tipo di applicazione hello cluster hello e crea un'istanza di applicazione dal tipo di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a07be-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span> <span data-ttu-id="a07be-105">Anche i servizi predefiniti vengono creati in questa fase.</span><span class="sxs-lookup"><span data-stu-id="a07be-105">Any default services are also created at this time.</span></span>

<span data-ttu-id="a07be-106">Se necessario, installare hello [servizio infrastruttura CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a07be-106">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="a07be-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="a07be-107">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a07be-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="a07be-108">Clean up deployment</span></span>

<span data-ttu-id="a07be-109">Al termine, hello [rimuovere](cli-remove-application.md) script può essere un'applicazione hello tooremove utilizzato.</span><span class="sxs-lookup"><span data-stu-id="a07be-109">When done, hello [remove](cli-remove-application.md) script can be used tooremove hello application.</span></span> <span data-ttu-id="a07be-110">script di rimozione Hello Elimina istanza dell'applicazione hello, Annulla la registrazione di tipo di applicazione hello e pacchetto dell'applicazione hello dall'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="a07be-110">hello remove script deletes hello application instance, unregisters hello application type, and deletes hello application package from the image store.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a07be-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a07be-111">Next steps</span></span>

<span data-ttu-id="a07be-112">Per ulteriori informazioni, vedere hello [documentazione servizio infrastruttura CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a07be-112">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="a07be-113">Esempi aggiuntivi di servizio dell'infrastruttura CLI per Azure Service Fabric sono reperibile in hello [esempi del servizio dell'infrastruttura CLI](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a07be-113">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
