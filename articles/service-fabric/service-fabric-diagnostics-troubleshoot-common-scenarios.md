---
title: Risoluzione dei problemi con la traccia di eventi | Documentazione Microsoft
description: "I problemi più comuni riscontrati durante la distribuzione dei servizi nell’infrastruttura di servizi di Microsoft Azure."
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
ms.openlocfilehash: e60bd4b9291cb2fc748921e42f11f54bb545984f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="69249-103">Risolvere i problemi comuni quando si distribuiscono servizi in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="69249-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="69249-104">Durante l'esecuzione di servizi nel computer di sviluppo è facile usare [Strumenti di debug di Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="69249-104">When you're running services on your developer computer, it is easy to use [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="69249-105">Per i cluster remoti, [i rapporti di integrità](service-fabric-view-entities-aggregated-health.md) sono sempre un buon punto di partenza.</span><span class="sxs-lookup"><span data-stu-id="69249-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place to start.</span></span> <span data-ttu-id="69249-106">I modi più semplici per accedere a questi report sono quelli che avvengono tramite PowerShell o [SFX](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="69249-106">The easiest ways to access these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="69249-107">In questo articolo si presuppone che si stia eseguendo il debug di un cluster remoto e una conoscenza di base dell'utilizzo di questi strumenti.</span><span class="sxs-lookup"><span data-stu-id="69249-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how to use either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="69249-108">Arresto anomalo dell’applicazione</span><span class="sxs-lookup"><span data-stu-id="69249-108">Application crash</span></span>
<span data-ttu-id="69249-109">Il report 'La partizione è inferiore rispetto al conteggio delle repliche di destinazione o dell’istanza ' è una valida indicazione del fatto che il servizio si sta arrestando in modo anomalo.</span><span class="sxs-lookup"><span data-stu-id="69249-109">The "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="69249-110">Per scoprire dove il servizio si arresta in modo anomalo è necessaria un’ulteriore indagine.</span><span class="sxs-lookup"><span data-stu-id="69249-110">To find out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="69249-111">Quando si esegue su vasta scala, sarà necessario un set di tracce ben studiate.</span><span class="sxs-lookup"><span data-stu-id="69249-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="69249-112">È consigliabile provare [Diagnostica di Azure](service-fabric-diagnostics-how-to-setup-wad.md) per raccogliere tali tracce e usare una soluzione come [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) per visualizzare ed eseguire ricerche nelle tracce.</span><span class="sxs-lookup"><span data-stu-id="69249-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching the traces.</span></span>

![Integrità della partizione SFX](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="69249-114">Durante l'inizializzazione dell’attore o del servizio</span><span class="sxs-lookup"><span data-stu-id="69249-114">During service or actor initialization</span></span>
<span data-ttu-id="69249-115">Tutte le eccezioni prima che il tipo di servizio venga inizializzato causeranno l'arresto anomalo del processo.</span><span class="sxs-lookup"><span data-stu-id="69249-115">Any exceptions before the service type is initialized will cause the process to crash.</span></span> <span data-ttu-id="69249-116">Per questi tipi di arresti anomali il log eventi dell’applicazione visualizzerà l'errore dal servizio.</span><span class="sxs-lookup"><span data-stu-id="69249-116">For these types of crashes, the application event log will show the error from your service.</span></span>
<span data-ttu-id="69249-117">Si tratta delle eccezioni più comuni che vengono visualizzate prima dell’inizializzazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="69249-117">These are the most common exceptions to see before the service is initialized.</span></span>

<span data-ttu-id="69249-118">***System.IO.FileNotFoundException***</span><span class="sxs-lookup"><span data-stu-id="69249-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="69249-119">Questo errore è spesso dovute a delle dipendenze mancanti dell’assembly.</span><span class="sxs-lookup"><span data-stu-id="69249-119">This error is often due to missing assembly dependencies.</span></span> <span data-ttu-id="69249-120">Controllare la proprietà CopyLocal in Visual Studio o la Global Assembly Cache per il nodo.</span><span class="sxs-lookup"><span data-stu-id="69249-120">Check the CopyLocal property in Visual Studio or the global assembly cache for the node.</span></span>

<span data-ttu-id="69249-121">***COMException*** *in System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*</span><span class="sxs-lookup"><span data-stu-id="69249-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="69249-122">Indica che il nome del tipo di servizio registrato non corrisponde con il manifesto del servizio.</span><span class="sxs-lookup"><span data-stu-id="69249-122">This indicates that the registered service type name does not match the service manifest.</span></span>

<span data-ttu-id="69249-123">[Diagnostica di Azure](service-fabric-diagnostics-how-to-setup-wad.md) può essere configurato per caricare automaticamente il log eventi dell'applicazione per tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="69249-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured to upload the application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="69249-124">RunAsync() or OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="69249-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="69249-125">Se si verifica l'arresto anomalo durante l'inizializzazione o l'esecuzione del tipo di servizio registrato o dell’attore, l'eccezione verrà rilevata da Service Fabric di Azure.</span><span class="sxs-lookup"><span data-stu-id="69249-125">If the crash happens during the initialization or running of your registered service type or actor, the exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="69249-126">È possibile visualizzarli dai provider EventSource descritti in modo dettagliato nella sezione “Passaggi successivi”.</span><span class="sxs-lookup"><span data-stu-id="69249-126">You can view these from the EventSource providers detailed in the "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69249-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="69249-127">Next steps</span></span>
<span data-ttu-id="69249-128">Altre informazioni sulla diagnostica esistente fornita dall'infrastruttura di servizi:</span><span class="sxs-lookup"><span data-stu-id="69249-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="69249-129">Diagnostica di Reliable actors</span><span class="sxs-lookup"><span data-stu-id="69249-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="69249-130">Diagnostica di Reliable Services</span><span class="sxs-lookup"><span data-stu-id="69249-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)

