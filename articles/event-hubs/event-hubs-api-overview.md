---
title: Panoramica dell'API di hub eventi aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: 46dfcc544ff92642cfd7a967f9ec38a0d8e2bd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="available-event-hubs-apis"></a><span data-ttu-id="4f4a9-103">API di Hub eventi disponibili</span><span class="sxs-lookup"><span data-stu-id="4f4a9-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="4f4a9-104">API di runtime</span><span class="sxs-lookup"><span data-stu-id="4f4a9-104">Runtime APIs</span></span>

<span data-ttu-id="4f4a9-105">di seguito Hello è una descrizione di tutti i client di runtime hub eventi di Azure attualmente disponibili.</span><span class="sxs-lookup"><span data-stu-id="4f4a9-105">hello following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="4f4a9-106">Benché alcune di queste librerie include anche funzionalità di gestione limitata, ci sono anche [librerie specifiche](#management-apis) dedicato toomanagement operazioni.</span><span class="sxs-lookup"><span data-stu-id="4f4a9-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated toomanagement operations.</span></span> <span data-ttu-id="4f4a9-107">lo stato attivo principale Hello di queste librerie è toosend e ricevere messaggi da un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="4f4a9-107">hello core focus of these libraries is toosend and receive messages from an event hub.</span></span>

<span data-ttu-id="4f4a9-108">Vedere [informazioni aggiuntive](#additional-information) per ulteriori informazioni sullo stato corrente di hello ogni della libreria di runtime.</span><span class="sxs-lookup"><span data-stu-id="4f4a9-108">See [additional information](#additional-information) for more details on hello current status of each runtime library.</span></span>

| <span data-ttu-id="4f4a9-109">Linguaggio/Piattaforma</span><span class="sxs-lookup"><span data-stu-id="4f4a9-109">Language/Platform</span></span> | <span data-ttu-id="4f4a9-110">Pacchetto client</span><span class="sxs-lookup"><span data-stu-id="4f4a9-110">Client package</span></span> | <span data-ttu-id="4f4a9-111">Pacchetto EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="4f4a9-111">EventProcessorHost package</span></span> | <span data-ttu-id="4f4a9-112">Repository</span><span class="sxs-lookup"><span data-stu-id="4f4a9-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f4a9-113">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="4f4a9-113">.NET Standard</span></span> | [<span data-ttu-id="4f4a9-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="4f4a9-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="4f4a9-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="4f4a9-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="4f4a9-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="4f4a9-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="4f4a9-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="4f4a9-117">.NET Framework</span></span> | [<span data-ttu-id="4f4a9-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="4f4a9-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="4f4a9-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="4f4a9-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="4f4a9-120">N/D</span><span class="sxs-lookup"><span data-stu-id="4f4a9-120">N/A</span></span> |
| <span data-ttu-id="4f4a9-121">Java</span><span class="sxs-lookup"><span data-stu-id="4f4a9-121">Java</span></span> | [<span data-ttu-id="4f4a9-122">Maven</span><span class="sxs-lookup"><span data-stu-id="4f4a9-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="4f4a9-123">Maven</span><span class="sxs-lookup"><span data-stu-id="4f4a9-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="4f4a9-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="4f4a9-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="4f4a9-125">Nodo</span><span class="sxs-lookup"><span data-stu-id="4f4a9-125">Node</span></span> | [<span data-ttu-id="4f4a9-126">NPM</span><span class="sxs-lookup"><span data-stu-id="4f4a9-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="4f4a9-127">N/D</span><span class="sxs-lookup"><span data-stu-id="4f4a9-127">N/A</span></span> | [<span data-ttu-id="4f4a9-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="4f4a9-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="4f4a9-129">C</span><span class="sxs-lookup"><span data-stu-id="4f4a9-129">C</span></span> | <span data-ttu-id="4f4a9-130">N/D</span><span class="sxs-lookup"><span data-stu-id="4f4a9-130">N/A</span></span> | <span data-ttu-id="4f4a9-131">N/D</span><span class="sxs-lookup"><span data-stu-id="4f4a9-131">N/A</span></span> | [<span data-ttu-id="4f4a9-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="4f4a9-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="4f4a9-133">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4f4a9-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="4f4a9-134">.NET</span><span class="sxs-lookup"><span data-stu-id="4f4a9-134">.NET</span></span>
<span data-ttu-id="4f4a9-135">ecosistema .NET Hello ha più runtime, pertanto sono presenti più librerie .NET per gli hub eventi.</span><span class="sxs-lookup"><span data-stu-id="4f4a9-135">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="4f4a9-136">libreria Standard di .NET Hello può essere eseguita tramite .NET Core o hello .NET Framework, mentre la libreria di .NET Framework hello può essere eseguita solo in un ambiente .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="4f4a9-136">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="4f4a9-137">Per altre informazioni su .NET Framework, vedere le [versioni del framework](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="4f4a9-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="4f4a9-138">Nodo</span><span class="sxs-lookup"><span data-stu-id="4f4a9-138">Node</span></span>

<span data-ttu-id="4f4a9-139">libreria di Node.js Hello è attualmente in anteprima e viene mantenuta come progetto lato dai dipendenti Microsoft e dai collaboratori esterni.</span><span class="sxs-lookup"><span data-stu-id="4f4a9-139">hello Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="4f4a9-140">Tutti i contributi compreso il codice sorgente sono graditi e verranno presi in esame.</span><span class="sxs-lookup"><span data-stu-id="4f4a9-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="4f4a9-141">API di gestione</span><span class="sxs-lookup"><span data-stu-id="4f4a9-141">Management APIs</span></span>

<span data-ttu-id="4f4a9-142">di seguito Hello è un elenco di tutte le librerie specifiche di gestione attualmente disponibili.</span><span class="sxs-lookup"><span data-stu-id="4f4a9-142">hello following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="4f4a9-143">Nessuna di queste librerie contengono le operazioni di runtime e hello solo scopo di gestire le entità di hub eventi.</span><span class="sxs-lookup"><span data-stu-id="4f4a9-143">None of these libraries contain runtime operations, and are for hello sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="4f4a9-144">Linguaggio/Piattaforma</span><span class="sxs-lookup"><span data-stu-id="4f4a9-144">Language/Platform</span></span> | <span data-ttu-id="4f4a9-145">Pacchetto di gestione</span><span class="sxs-lookup"><span data-stu-id="4f4a9-145">Management package</span></span> | <span data-ttu-id="4f4a9-146">Repository</span><span class="sxs-lookup"><span data-stu-id="4f4a9-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4f4a9-147">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="4f4a9-147">.NET Standard</span></span> | [<span data-ttu-id="4f4a9-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="4f4a9-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="4f4a9-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="4f4a9-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="4f4a9-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4f4a9-150">Next steps</span></span>
<span data-ttu-id="4f4a9-151">Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="4f4a9-151">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="4f4a9-152">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="4f4a9-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="4f4a9-153">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="4f4a9-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="4f4a9-154">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="4f4a9-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)