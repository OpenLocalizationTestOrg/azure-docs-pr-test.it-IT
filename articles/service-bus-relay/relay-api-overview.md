---
title: Panoramica delle API di Inoltro di Azure | Documentazione Microsoft
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
ms.openlocfilehash: 8d93a0344adc3b0b7617f3a7d85124142d7a7555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="available-relay-apis"></a><span data-ttu-id="f23fc-103">API di Inoltro disponibili</span><span class="sxs-lookup"><span data-stu-id="f23fc-103">Available Relay APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="f23fc-104">API di runtime</span><span class="sxs-lookup"><span data-stu-id="f23fc-104">Runtime APIs</span></span>

<span data-ttu-id="f23fc-105">La tabella seguente elenca tutti i client di runtime di Inoltro attualmente disponibili.</span><span class="sxs-lookup"><span data-stu-id="f23fc-105">The following table lists all currently available Relay runtime clients.</span></span>

<span data-ttu-id="f23fc-106">La sezione [Informazioni aggiuntive](#additional-information) contiene altre informazioni sullo stato di ogni libreria di runtime.</span><span class="sxs-lookup"><span data-stu-id="f23fc-106">The [additional information](#additional-information) section contains more information about the status of each runtime library.</span></span>

| <span data-ttu-id="f23fc-107">Linguaggio/Piattaforma</span><span class="sxs-lookup"><span data-stu-id="f23fc-107">Language/Platform</span></span> | <span data-ttu-id="f23fc-108">Funzionalità disponibile</span><span class="sxs-lookup"><span data-stu-id="f23fc-108">Available feature</span></span> | <span data-ttu-id="f23fc-109">Pacchetto client</span><span class="sxs-lookup"><span data-stu-id="f23fc-109">Client package</span></span> | <span data-ttu-id="f23fc-110">Repository</span><span class="sxs-lookup"><span data-stu-id="f23fc-110">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f23fc-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="f23fc-111">.NET Standard</span></span> | <span data-ttu-id="f23fc-112">Connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="f23fc-112">Hybrid Connections</span></span> | [<span data-ttu-id="f23fc-113">Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="f23fc-113">Microsoft.Azure.Relay</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [<span data-ttu-id="f23fc-114">GitHub</span><span class="sxs-lookup"><span data-stu-id="f23fc-114">GitHub</span></span>](https://github.com/azure/azure-relay-dotnet) |
| <span data-ttu-id="f23fc-115">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f23fc-115">.NET Framework</span></span> | <span data-ttu-id="f23fc-116">Inoltro WCF</span><span class="sxs-lookup"><span data-stu-id="f23fc-116">WCF Relay</span></span> | [<span data-ttu-id="f23fc-117">WindowsAzure.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="f23fc-117">WindowsAzure.ServiceBus</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | <span data-ttu-id="f23fc-118">N/D</span><span class="sxs-lookup"><span data-stu-id="f23fc-118">N/A</span></span> |
| <span data-ttu-id="f23fc-119">Nodo</span><span class="sxs-lookup"><span data-stu-id="f23fc-119">Node</span></span> | <span data-ttu-id="f23fc-120">Connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="f23fc-120">Hybrid Connections</span></span> | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [<span data-ttu-id="f23fc-121">GitHub</span><span class="sxs-lookup"><span data-stu-id="f23fc-121">GitHub</span></span>](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a><span data-ttu-id="f23fc-122">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f23fc-122">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="f23fc-123">.NET</span><span class="sxs-lookup"><span data-stu-id="f23fc-123">.NET</span></span>
<span data-ttu-id="f23fc-124">I runtime in un ecosistema .NET sono vari, pertanto sono presenti più librerie .NET per gli Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="f23fc-124">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="f23fc-125">La libreria .NET Standard può essere eseguita usando .NET Core o .NET Framework, mentre la libreria .NET Framework può essere eseguita solo in un ambiente .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="f23fc-125">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="f23fc-126">Per altre informazioni su .NET Framework, vedere le [versioni del framework](/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="f23fc-126">For more information on .NET Frameworks, see [framework versions](/dotnet/articles/standard/frameworks#framework-versions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f23fc-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f23fc-127">Next steps</span></span>
<span data-ttu-id="f23fc-128">Per altre informazioni sul servizio di inoltro di Azure, vedere i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f23fc-128">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="f23fc-129">Che cos'è il servizio di inoltro di Azure?</span><span class="sxs-lookup"><span data-stu-id="f23fc-129">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="f23fc-130">Domande frequenti sul servizio di inoltro</span><span class="sxs-lookup"><span data-stu-id="f23fc-130">Relay FAQ</span></span>](relay-faq.md)