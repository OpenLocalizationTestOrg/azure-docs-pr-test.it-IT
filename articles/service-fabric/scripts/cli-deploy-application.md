---
title: Esempio di distribuzione di script dell'interfaccia della riga di comando di Azure Service Fabric
description: Distribuire un'applicazione in un cluster di Azure Service Fabric usando l'interfaccia della riga di comando di Azure Service Fabric
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
ms.openlocfilehash: c77ecfccdf7d3e34b0b3133e9c63810a04fb1132
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-application-to-a-service-fabric-cluster"></a><span data-ttu-id="7deb9-103">Distribuire un'applicazione in un cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7deb9-103">Deploy an application to a Service Fabric cluster</span></span>

<span data-ttu-id="7deb9-104">Questo script di esempio copia un pacchetto dell'applicazione in un archivio immagini del cluster, registra il tipo di applicazione nel cluster e crea un'istanza di applicazione dal tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="7deb9-104">This sample script copies an application package to a cluster image store, registers the application type in the cluster, and creates an application instance from the application type.</span></span> <span data-ttu-id="7deb9-105">Anche i servizi predefiniti vengono creati in questa fase.</span><span class="sxs-lookup"><span data-stu-id="7deb9-105">Any default services are also created at this time.</span></span>

<span data-ttu-id="7deb9-106">Se necessario, installare l'[interfaccia della riga di comando di Service Fabric](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7deb9-106">If needed, install the [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="7deb9-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="7deb9-107">Sample script</span></span>

<span data-ttu-id="7deb9-108">[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Distribuire un'applicazione in un cluster")]</span><span class="sxs-lookup"><span data-stu-id="7deb9-108">[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application to a cluster")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="7deb9-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="7deb9-109">Clean up deployment</span></span>

<span data-ttu-id="7deb9-110">Al termine, è possibile usare lo script [remove](cli-remove-application.md) per rimuovere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7deb9-110">When done, the [remove](cli-remove-application.md) script can be used to remove the application.</span></span> <span data-ttu-id="7deb9-111">Lo script remove elimina l'istanza dell'applicazione, annulla la registrazione del tipo di applicazione ed elimina il pacchetto dell'applicazione dall'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="7deb9-111">The remove script deletes the application instance, unregisters the application type, and deletes the application package from the image store.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7deb9-112">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7deb9-112">Next steps</span></span>

<span data-ttu-id="7deb9-113">Per altre informazioni, vedere la [documentazione sull'interfaccia della riga di comando di Service Fabric](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7deb9-113">For more information, see the [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="7deb9-114">Altri esempi dell'interfaccia della riga di comando di Service Fabric per Azure Service Fabric sono disponibili negli [esempi dell'interfaccia della riga di comando di Service Fabric](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7deb9-114">Additional Service Fabric CLI samples for Azure Service Fabric can be found in the [Service Fabric CLI samples](../samples-cli.md).</span></span>
