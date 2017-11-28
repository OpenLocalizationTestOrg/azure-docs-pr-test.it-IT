---
title: aaaTroubleshooting con event Tracing for | Documenti Microsoft
description: problemi di Hello comuni riscontrati durante la distribuzione di servizi in Microsoft Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="e31c4-103">Risolvere i problemi comuni quando si distribuiscono servizi in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e31c4-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="e31c4-104">Quando si esegue i servizi nel computer di sviluppo, è facile toouse [strumenti di debug di Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="e31c4-104">When you're running services on your developer computer, it is easy toouse [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="e31c4-105">Per i cluster remoti, [rapporti di stato](service-fabric-view-entities-aggregated-health.md) sono sempre toostart un buon punto.</span><span class="sxs-lookup"><span data-stu-id="e31c4-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place toostart.</span></span> <span data-ttu-id="e31c4-106">Hello più semplice tooaccess modi questi report sono tramite PowerShell o [SFX](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="e31c4-106">hello easiest ways tooaccess these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="e31c4-107">Questo articolo si presuppone che si sta eseguendo il debug di un cluster remoto e avere una conoscenza di base di toouse uno di questi strumenti.</span><span class="sxs-lookup"><span data-stu-id="e31c4-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how toouse either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="e31c4-108">Arresto anomalo dell’applicazione</span><span class="sxs-lookup"><span data-stu-id="e31c4-108">Application crash</span></span>
<span data-ttu-id="e31c4-109">Hello "partizione è inferiore al numero di istanze o di replica di destinazione" report è molto probabile che il servizio è arrestato in modo anomalo.</span><span class="sxs-lookup"><span data-stu-id="e31c4-109">hello "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="e31c4-110">toofind out in un arresto anomalo del servizio richiede qualche ulteriore analisi.</span><span class="sxs-lookup"><span data-stu-id="e31c4-110">toofind out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="e31c4-111">Quando si esegue su vasta scala, sarà necessario un set di tracce ben studiate.</span><span class="sxs-lookup"><span data-stu-id="e31c4-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="e31c4-112">È consigliabile provare [diagnostica Azure](service-fabric-diagnostics-how-to-setup-wad.md) per raccogliere le tracce e l'utilizzo di una soluzione, ad esempio [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) per la visualizzazione e la ricerca delle tracce hello.</span><span class="sxs-lookup"><span data-stu-id="e31c4-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching hello traces.</span></span>

![Integrità della partizione SFX](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="e31c4-114">Durante l'inizializzazione dell’attore o del servizio</span><span class="sxs-lookup"><span data-stu-id="e31c4-114">During service or actor initialization</span></span>
<span data-ttu-id="e31c4-115">Tutte le eccezioni prima dell'inizializzazione tipo di servizio hello causerà toocrash processo hello.</span><span class="sxs-lookup"><span data-stu-id="e31c4-115">Any exceptions before hello service type is initialized will cause hello process toocrash.</span></span> <span data-ttu-id="e31c4-116">Per questi tipi di arresti anomali del sistema, log eventi dell'applicazione hello visualizzerà l'errore hello dal servizio.</span><span class="sxs-lookup"><span data-stu-id="e31c4-116">For these types of crashes, hello application event log will show hello error from your service.</span></span>
<span data-ttu-id="e31c4-117">Si tratta di toosee eccezioni più comuni di hello prima hello servizio viene inizializzato.</span><span class="sxs-lookup"><span data-stu-id="e31c4-117">These are hello most common exceptions toosee before hello service is initialized.</span></span>

<span data-ttu-id="e31c4-118">***System.IO.FileNotFoundException***</span><span class="sxs-lookup"><span data-stu-id="e31c4-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="e31c4-119">Questo errore è spesso dovuto toomissing le dipendenze dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="e31c4-119">This error is often due toomissing assembly dependencies.</span></span> <span data-ttu-id="e31c4-120">Controllare la proprietà CopyLocal hello in Visual Studio o hello global assembly cache per il nodo hello.</span><span class="sxs-lookup"><span data-stu-id="e31c4-120">Check hello CopyLocal property in Visual Studio or hello global assembly cache for hello node.</span></span>

<span data-ttu-id="e31c4-121">***COMException*** *in System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*</span><span class="sxs-lookup"><span data-stu-id="e31c4-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="e31c4-122">Questo indica che il nome del tipo servizio registrato hello non corrisponde a manifesto del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="e31c4-122">This indicates that hello registered service type name does not match hello service manifest.</span></span>

<span data-ttu-id="e31c4-123">[Diagnostica di Azure](service-fabric-diagnostics-how-to-setup-wad.md) possono il registro eventi dell'applicazione hello tooupload configurato per tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="e31c4-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured tooupload hello application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="e31c4-124">RunAsync() or OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="e31c4-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="e31c4-125">In caso di arresto anomalo di hello durante l'inizializzazione di hello o l'esecuzione del tipo di servizio registrato o attore, hello eccezione verrà rilevata da Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e31c4-125">If hello crash happens during hello initialization or running of your registered service type or actor, hello exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="e31c4-126">È possibile visualizzare questi dai provider di EventSource hello descritta in dettaglio nella sezione "Passaggi successivi" hello.</span><span class="sxs-lookup"><span data-stu-id="e31c4-126">You can view these from hello EventSource providers detailed in hello "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e31c4-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e31c4-127">Next steps</span></span>
<span data-ttu-id="e31c4-128">Altre informazioni sulla diagnostica esistente fornita dall'infrastruttura di servizi:</span><span class="sxs-lookup"><span data-stu-id="e31c4-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="e31c4-129">Diagnostica di Reliable actors</span><span class="sxs-lookup"><span data-stu-id="e31c4-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="e31c4-130">Diagnostica di Reliable Services</span><span class="sxs-lookup"><span data-stu-id="e31c4-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)

