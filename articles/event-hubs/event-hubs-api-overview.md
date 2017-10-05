---
title: Panoramica delle API di Hub eventi di Azure | Microsoft Docs
description: Panoramica delle API di Hub eventi di Azure disponibili
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3f221a0c-182d-4e39-9f3d-3a3c16c5c6ed
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 40cd76e1aacb68d6051cae4a3c90a8970f5449f0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="available-event-hubs-apis"></a><span data-ttu-id="72912-103">API di Hub eventi disponibili</span><span class="sxs-lookup"><span data-stu-id="72912-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="72912-104">API di runtime</span><span class="sxs-lookup"><span data-stu-id="72912-104">Runtime APIs</span></span>

<span data-ttu-id="72912-105">Di seguito vengono descritti tutti i client di runtime di Hub eventi di Azure attualmente disponibili.</span><span class="sxs-lookup"><span data-stu-id="72912-105">The following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="72912-106">Sebbene alcune di queste librerie includano anche la funzionalità di gestione limitata, esistono [librerie specifiche](#management-apis) dedicate alle operazioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="72912-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated to management operations.</span></span> <span data-ttu-id="72912-107">L'obiettivo principale di queste librerie è di inviare e ricevere messaggi da un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="72912-107">The core focus of these libraries is to send and receive messages from an event hub.</span></span>

<span data-ttu-id="72912-108">Sono disponibili [altre informazioni](#additional-information) per trovare più dettagli sullo stato corrente di tutte le librerie di runtime.</span><span class="sxs-lookup"><span data-stu-id="72912-108">See [additional information](#additional-information) for more details on the current status of each runtime library.</span></span>

| <span data-ttu-id="72912-109">Linguaggio/Piattaforma</span><span class="sxs-lookup"><span data-stu-id="72912-109">Language/Platform</span></span> | <span data-ttu-id="72912-110">Pacchetto client</span><span class="sxs-lookup"><span data-stu-id="72912-110">Client package</span></span> | <span data-ttu-id="72912-111">Pacchetto EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="72912-111">EventProcessorHost package</span></span> | <span data-ttu-id="72912-112">Repository</span><span class="sxs-lookup"><span data-stu-id="72912-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="72912-113">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="72912-113">.NET Standard</span></span> | [<span data-ttu-id="72912-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="72912-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="72912-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="72912-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="72912-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="72912-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="72912-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="72912-117">.NET Framework</span></span> | [<span data-ttu-id="72912-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="72912-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="72912-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="72912-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="72912-120">N/D</span><span class="sxs-lookup"><span data-stu-id="72912-120">N/A</span></span> |
| <span data-ttu-id="72912-121">Java</span><span class="sxs-lookup"><span data-stu-id="72912-121">Java</span></span> | [<span data-ttu-id="72912-122">Maven</span><span class="sxs-lookup"><span data-stu-id="72912-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="72912-123">Maven</span><span class="sxs-lookup"><span data-stu-id="72912-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="72912-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="72912-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="72912-125">Nodo</span><span class="sxs-lookup"><span data-stu-id="72912-125">Node</span></span> | [<span data-ttu-id="72912-126">NPM</span><span class="sxs-lookup"><span data-stu-id="72912-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="72912-127">N/D</span><span class="sxs-lookup"><span data-stu-id="72912-127">N/A</span></span> | [<span data-ttu-id="72912-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="72912-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="72912-129">C</span><span class="sxs-lookup"><span data-stu-id="72912-129">C</span></span> | <span data-ttu-id="72912-130">N/D</span><span class="sxs-lookup"><span data-stu-id="72912-130">N/A</span></span> | <span data-ttu-id="72912-131">N/D</span><span class="sxs-lookup"><span data-stu-id="72912-131">N/A</span></span> | [<span data-ttu-id="72912-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="72912-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="72912-133">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="72912-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="72912-134">.NET</span><span class="sxs-lookup"><span data-stu-id="72912-134">.NET</span></span>
<span data-ttu-id="72912-135">I runtime in un ecosistema .NET sono vari, pertanto sono presenti più librerie .NET per gli Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="72912-135">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="72912-136">La libreria .NET Standard può essere eseguita usando .NET Core o .NET Framework, mentre la libreria .NET Framework può essere eseguita solo in un ambiente .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="72912-136">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="72912-137">Per altre informazioni su .NET Framework, vedere le [versioni del framework](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="72912-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="72912-138">Nodo</span><span class="sxs-lookup"><span data-stu-id="72912-138">Node</span></span>

<span data-ttu-id="72912-139">La libreria Node.js è attualmente in anteprima e viene gestita come progetto a parte da dipendenti Microsoft e collaboratori esterni.</span><span class="sxs-lookup"><span data-stu-id="72912-139">The Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="72912-140">Tutti i contributi compreso il codice sorgente sono graditi e verranno presi in esame.</span><span class="sxs-lookup"><span data-stu-id="72912-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="72912-141">API di gestione</span><span class="sxs-lookup"><span data-stu-id="72912-141">Management APIs</span></span>

<span data-ttu-id="72912-142">Di seguito è riportato un elenco di tutte le librerie di gestione specifiche attualmente disponibili.</span><span class="sxs-lookup"><span data-stu-id="72912-142">The following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="72912-143">Nessuna di loro include operazioni di runtime e le librerie hanno il solo scopo di gestire le entità di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="72912-143">None of these libraries contain runtime operations, and are for the sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="72912-144">Linguaggio/Piattaforma</span><span class="sxs-lookup"><span data-stu-id="72912-144">Language/Platform</span></span> | <span data-ttu-id="72912-145">Pacchetto di gestione</span><span class="sxs-lookup"><span data-stu-id="72912-145">Management package</span></span> | <span data-ttu-id="72912-146">Repository</span><span class="sxs-lookup"><span data-stu-id="72912-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="72912-147">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="72912-147">.NET Standard</span></span> | [<span data-ttu-id="72912-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="72912-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="72912-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="72912-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="72912-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="72912-150">Next steps</span></span>
<span data-ttu-id="72912-151">Per ulteriori informazioni su Hub eventi visitare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="72912-151">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="72912-152">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="72912-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="72912-153">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="72912-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="72912-154">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="72912-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)