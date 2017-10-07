---
title: Panoramica dell'API di inoltro aaaAzure | Documenti Microsoft
description: Panoramica delle API di Inoltro di Azure disponibili
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fdaa1d2b-bd80-4e75-abb9-0c3d0773af2d
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 3c4d737d5fee9a8babce094fa6dfddb28910834b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="available-relay-apis"></a><span data-ttu-id="cb35b-103">API di Inoltro disponibili</span><span class="sxs-lookup"><span data-stu-id="cb35b-103">Available Relay APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="cb35b-104">API di runtime</span><span class="sxs-lookup"><span data-stu-id="cb35b-104">Runtime APIs</span></span>

<span data-ttu-id="cb35b-105">Hello nella tabella seguente sono elencati tutti i client di runtime inoltro attualmente disponibili.</span><span class="sxs-lookup"><span data-stu-id="cb35b-105">hello following table lists all currently available Relay runtime clients.</span></span>

<span data-ttu-id="cb35b-106">Hello [informazioni aggiuntive](#additional-information) sezione contiene ulteriori informazioni sullo stato di hello ogni della libreria di runtime.</span><span class="sxs-lookup"><span data-stu-id="cb35b-106">hello [additional information](#additional-information) section contains more information about hello status of each runtime library.</span></span>

| <span data-ttu-id="cb35b-107">Linguaggio/Piattaforma</span><span class="sxs-lookup"><span data-stu-id="cb35b-107">Language/Platform</span></span> | <span data-ttu-id="cb35b-108">Funzionalità disponibile</span><span class="sxs-lookup"><span data-stu-id="cb35b-108">Available feature</span></span> | <span data-ttu-id="cb35b-109">Pacchetto client</span><span class="sxs-lookup"><span data-stu-id="cb35b-109">Client package</span></span> | <span data-ttu-id="cb35b-110">Repository</span><span class="sxs-lookup"><span data-stu-id="cb35b-110">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cb35b-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="cb35b-111">.NET Standard</span></span> | <span data-ttu-id="cb35b-112">Connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="cb35b-112">Hybrid Connections</span></span> | [<span data-ttu-id="cb35b-113">Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="cb35b-113">Microsoft.Azure.Relay</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [<span data-ttu-id="cb35b-114">GitHub</span><span class="sxs-lookup"><span data-stu-id="cb35b-114">GitHub</span></span>](https://github.com/azure/azure-relay-dotnet) |
| <span data-ttu-id="cb35b-115">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="cb35b-115">.NET Framework</span></span> | <span data-ttu-id="cb35b-116">Inoltro WCF</span><span class="sxs-lookup"><span data-stu-id="cb35b-116">WCF Relay</span></span> | [<span data-ttu-id="cb35b-117">WindowsAzure.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="cb35b-117">WindowsAzure.ServiceBus</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | <span data-ttu-id="cb35b-118">N/D</span><span class="sxs-lookup"><span data-stu-id="cb35b-118">N/A</span></span> |
| <span data-ttu-id="cb35b-119">Nodo</span><span class="sxs-lookup"><span data-stu-id="cb35b-119">Node</span></span> | <span data-ttu-id="cb35b-120">Connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="cb35b-120">Hybrid Connections</span></span> | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [<span data-ttu-id="cb35b-121">GitHub</span><span class="sxs-lookup"><span data-stu-id="cb35b-121">GitHub</span></span>](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a><span data-ttu-id="cb35b-122">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="cb35b-122">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="cb35b-123">.NET</span><span class="sxs-lookup"><span data-stu-id="cb35b-123">.NET</span></span>
<span data-ttu-id="cb35b-124">ecosistema .NET Hello ha più runtime, pertanto sono presenti più librerie .NET per gli hub eventi.</span><span class="sxs-lookup"><span data-stu-id="cb35b-124">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="cb35b-125">libreria Standard di .NET Hello può essere eseguita tramite .NET Core o hello .NET Framework, mentre la libreria di .NET Framework hello può essere eseguita solo in un ambiente .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="cb35b-125">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="cb35b-126">Per altre informazioni su .NET Framework, vedere le [versioni del framework](/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="cb35b-126">For more information on .NET Frameworks, see [framework versions](/dotnet/articles/standard/frameworks#framework-versions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb35b-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cb35b-127">Next steps</span></span>
<span data-ttu-id="cb35b-128">toolearn ulteriori informazioni sull'inoltro di Azure, visitare i collegamenti:</span><span class="sxs-lookup"><span data-stu-id="cb35b-128">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="cb35b-129">Che cos'è il servizio di inoltro di Azure?</span><span class="sxs-lookup"><span data-stu-id="cb35b-129">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="cb35b-130">Domande frequenti sul servizio di inoltro</span><span class="sxs-lookup"><span data-stu-id="cb35b-130">Relay FAQ</span></span>](relay-faq.md)