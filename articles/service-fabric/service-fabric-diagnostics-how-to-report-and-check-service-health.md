---
title: "aaaReport e controllo di integrità con Azure Service Fabric | Documenti Microsoft"
description: "Informazioni su come rapporti di integrità toosend dal codice del servizio e modo fornisce l'integrità hello toocheck del servizio tramite gli strumenti di monitoraggio dell'integrità hello che Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: mfussell
editor: 
ms.assetid: 7c712c22-d333-44bc-b837-d0b3603d9da8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: bcb838fefe3f2054447e1731d709e455560260e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="report-and-check-service-health"></a><span data-ttu-id="f10a9-103">Creare report e verificare l'integrità dei servizi</span><span class="sxs-lookup"><span data-stu-id="f10a9-103">Report and check service health</span></span>
<span data-ttu-id="f10a9-104">Quando i servizi verificano problemi le interruzioni interventi di correzione tooand toorespond possibilità dipende dai possibilità toodetect hello problemi rapidamente.</span><span class="sxs-lookup"><span data-stu-id="f10a9-104">When your services encounter problems, your ability toorespond tooand fix incidents and outages depends on your ability toodetect hello issues quickly.</span></span> <span data-ttu-id="f10a9-105">Se si segnala errori e problemi di gestione di integrità di Azure Service Fabric toohello dal codice del servizio, è possibile utilizzare gli strumenti di Service Fabric fornisce lo stato di integrità hello toocheck di monitoraggio dello stato standard.</span><span class="sxs-lookup"><span data-stu-id="f10a9-105">If you report problems and failures toohello Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides toocheck hello health status.</span></span>

<span data-ttu-id="f10a9-106">Esistono tre modi che è possibile segnalare l'integrità dal servizio hello:</span><span class="sxs-lookup"><span data-stu-id="f10a9-106">There are three ways that you can report health from hello service:</span></span>

* <span data-ttu-id="f10a9-107">Usare gli oggetti [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) o [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext).</span><span class="sxs-lookup"><span data-stu-id="f10a9-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="f10a9-108">È possibile utilizzare hello `Partition` e `CodePackageActivationContext` oggetti integrità hello tooreport di elementi che fanno parte del contesto corrente hello.</span><span class="sxs-lookup"><span data-stu-id="f10a9-108">You can use hello `Partition` and `CodePackageActivationContext` objects tooreport hello health of elements that are part of hello current context.</span></span> <span data-ttu-id="f10a9-109">Ad esempio, il codice che viene eseguito come parte di una replica può segnalare l'integrità solo su tale replica, hello partizione a cui appartiene e che fa parte di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f10a9-109">For example, code that runs as part of a replica can report health only on that replica, hello partition that it belongs to, and hello application that it is a part of.</span></span>
* <span data-ttu-id="f10a9-110">Usare `FabricClient`.</span><span class="sxs-lookup"><span data-stu-id="f10a9-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="f10a9-111">È possibile utilizzare `FabricClient` integrità tooreport dal codice del servizio hello se non è cluster hello [sicura](service-fabric-cluster-security.md) o se il servizio di hello è in esecuzione con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="f10a9-111">You can use `FabricClient` tooreport health from hello service code if hello cluster is not [secure](service-fabric-cluster-security.md) or if hello service is running with admin privileges.</span></span> <span data-ttu-id="f10a9-112">La maggior parte degli scenari reali non usa cluster non protetti oppure fornisce privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="f10a9-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="f10a9-113">Con `FabricClient`, è possibile segnalare l'integrità per qualsiasi entità che fa parte del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="f10a9-113">With `FabricClient`, you can report health on any entity that is a part of hello cluster.</span></span> <span data-ttu-id="f10a9-114">In teoria, tuttavia, codice del servizio deve solo inviare i report correlati tooits sanitari.</span><span class="sxs-lookup"><span data-stu-id="f10a9-114">Ideally, however, service code should only send reports that are related tooits own health.</span></span>
* <span data-ttu-id="f10a9-115">Utilizzare API REST di hello cluster hello, applicazione, applicazione distribuita, servizio, pacchetto del servizio, una partizione, replica o livelli dei nodi.</span><span class="sxs-lookup"><span data-stu-id="f10a9-115">Use hello REST APIs at hello cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="f10a9-116">Può trattarsi di integrità tooreport utilizzati all'interno di un contenitore.</span><span class="sxs-lookup"><span data-stu-id="f10a9-116">This can be used tooreport health from within a container.</span></span>

<span data-ttu-id="f10a9-117">Questo articolo viene illustrato un esempio che segnala l'integrità dal codice del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="f10a9-117">This article walks you through an example that reports health from hello service code.</span></span> <span data-ttu-id="f10a9-118">esempio Hello Mostra anche come strumenti hello forniti dall'infrastruttura di servizio possono essere utilizzato toocheck hello lo stato di integrità.</span><span class="sxs-lookup"><span data-stu-id="f10a9-118">hello example also shows how hello tools provided by Service Fabric can be used toocheck hello health status.</span></span> <span data-ttu-id="f10a9-119">In questo articolo è previsto toobe integrità toohello di introduzione funzionalità di monitoraggio di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f10a9-119">This article is intended toobe a quick introduction toohello health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="f10a9-120">Per informazioni più dettagliate, è possibile leggere una serie di hello di articoli approfonditi su integrità che iniziano con collegamento hello alla fine di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="f10a9-120">For more detailed information, you can read hello series of in-depth articles about health that start with hello link at hello end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f10a9-121">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f10a9-121">Prerequisites</span></span>
<span data-ttu-id="f10a9-122">È necessario avere installato quanto segue hello:</span><span class="sxs-lookup"><span data-stu-id="f10a9-122">You must have hello following installed:</span></span>

* <span data-ttu-id="f10a9-123">Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="f10a9-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="f10a9-124">Service Fabric SDK</span><span class="sxs-lookup"><span data-stu-id="f10a9-124">Service Fabric SDK</span></span>

## <a name="toocreate-a-local-secure-dev-cluster"></a><span data-ttu-id="f10a9-125">toocreate un cluster locale sviluppo sicuro</span><span class="sxs-lookup"><span data-stu-id="f10a9-125">toocreate a local secure dev cluster</span></span>
* <span data-ttu-id="f10a9-126">Aprire PowerShell con privilegi di amministratore ed eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="f10a9-126">Open PowerShell with admin privileges, and run hello following commands:</span></span>

![I comandi che mostrano come toocreate un cluster di sviluppo sicuro](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a><span data-ttu-id="f10a9-128">toodeploy un'applicazione e controllare l'integrità</span><span class="sxs-lookup"><span data-stu-id="f10a9-128">toodeploy an application and check its health</span></span>
1. <span data-ttu-id="f10a9-129">Aprire Visual Studio come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f10a9-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="f10a9-130">Creare un progetto utilizzando hello **servizio con stato** modello.</span><span class="sxs-lookup"><span data-stu-id="f10a9-130">Create a project by using hello **Stateful Service** template.</span></span>
   
    ![Creare un'applicazione di Service Fabric con un servizio con stato](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="f10a9-132">Premere **F5** toorun un'applicazione hello in modalità di debug.</span><span class="sxs-lookup"><span data-stu-id="f10a9-132">Press **F5** toorun hello application in debug mode.</span></span> <span data-ttu-id="f10a9-133">un'applicazione Hello è cluster locale toohello distribuito.</span><span class="sxs-lookup"><span data-stu-id="f10a9-133">hello application is deployed toohello local cluster.</span></span>
4. <span data-ttu-id="f10a9-134">Dopo l'applicazione hello è in esecuzione, fare clic sull'icona di gestione di Cluster locale hello nell'area di notifica hello e selezionare **gestire Cluster locale** da tooopen dal menu di scelta rapida hello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="f10a9-134">After hello application is running, right-click hello Local Cluster Manager icon in hello notification area and select **Manage Local Cluster** from hello shortcut menu tooopen Service Fabric Explorer.</span></span>
   
    ![Apertura di Service Fabric Explorer dall'area di notifica](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="f10a9-136">integrità applicazione Hello dovrebbero essere visualizzati come questa immagine.</span><span class="sxs-lookup"><span data-stu-id="f10a9-136">hello application health should be displayed as in this image.</span></span> <span data-ttu-id="f10a9-137">In questo momento, un'applicazione hello deve essere integra senza errori.</span><span class="sxs-lookup"><span data-stu-id="f10a9-137">At this time, hello application should be healthy with no errors.</span></span>
   
    ![Applicazione integra in Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="f10a9-139">È inoltre possibile verificare l'integrità di hello tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f10a9-139">You can also check hello health by using PowerShell.</span></span> <span data-ttu-id="f10a9-140">È possibile utilizzare ```Get-ServiceFabricApplicationHealth``` toocheck integrità di un'applicazione, si può usare ```Get-ServiceFabricServiceHealth``` toocheck integrità di un servizio.</span><span class="sxs-lookup"><span data-stu-id="f10a9-140">You can use ```Get-ServiceFabricApplicationHealth``` toocheck an application's health, and you can use ```Get-ServiceFabricServiceHealth``` toocheck a service's health.</span></span> <span data-ttu-id="f10a9-141">Hello rapporto di stato per hello stessa applicazione in PowerShell è in questa immagine.</span><span class="sxs-lookup"><span data-stu-id="f10a9-141">hello health report for hello same application in PowerShell is in this image.</span></span>
   
    ![Applicazione integra in PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a><span data-ttu-id="f10a9-143">codice del servizio tooyour eventi tooadd integrità personalizzato</span><span class="sxs-lookup"><span data-stu-id="f10a9-143">tooadd custom health events tooyour service code</span></span>
<span data-ttu-id="f10a9-144">modelli di progetto di Service Fabric Hello in Visual Studio contengono codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="f10a9-144">hello Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="f10a9-145">Hello passaggi seguenti viene illustrato come è possibile segnalare gli eventi di stato personalizzato dal codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="f10a9-145">hello following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="f10a9-146">Tali report vengono visualizzate automaticamente in strumenti standard di hello per l'integrità del monitoraggio che fornisce Service Fabric, ad esempio Service Fabric Explorer e visualizzazione dell'integrità del portale di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f10a9-146">Such reports show up automatically in hello standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="f10a9-147">Riaprire l'applicazione hello creata in precedenza in Visual Studio o creare una nuova applicazione con hello **servizio con stato** modello di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f10a9-147">Reopen hello application that you created previously in Visual Studio, or create a new application by using hello **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="f10a9-148">Aprire il file Stateful1.cs hello e trovare hello `myDictionary.TryGetValueAsync` chiamare hello `RunAsync` metodo.</span><span class="sxs-lookup"><span data-stu-id="f10a9-148">Open hello Stateful1.cs file, and find hello `myDictionary.TryGetValueAsync` call in hello `RunAsync` method.</span></span> <span data-ttu-id="f10a9-149">È possibile vedere che questo metodo restituisce un `result` che contiene hello valore corrente del contatore hello perché la chiave logica hello in questa applicazione è tookeep in esecuzione di un numero.</span><span class="sxs-lookup"><span data-stu-id="f10a9-149">You can see that this method returns a `result` that holds hello current value of hello counter because hello key logic in this application is tookeep a count running.</span></span> <span data-ttu-id="f10a9-150">Se si trattasse di un'applicazione reale e mancanza di hello del risultato rappresentato un errore, è opportuno tooflag quell'evento.</span><span class="sxs-lookup"><span data-stu-id="f10a9-150">If this were a real application, and if hello lack of result represented a failure, you would want tooflag that event.</span></span>
3. <span data-ttu-id="f10a9-151">tooreport un evento di integrità quando assenza hello del risultato rappresenta un errore, aggiungere hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="f10a9-151">tooreport a health event when hello lack of result represents a failure, add hello following steps.</span></span>
   
    <span data-ttu-id="f10a9-152">a.</span><span class="sxs-lookup"><span data-stu-id="f10a9-152">a.</span></span> <span data-ttu-id="f10a9-153">Aggiungere hello `System.Fabric.Health` Stateful1.cs toohello di spazio dei nomi file.</span><span class="sxs-lookup"><span data-stu-id="f10a9-153">Add hello `System.Fabric.Health` namespace toohello Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="f10a9-154">b.</span><span class="sxs-lookup"><span data-stu-id="f10a9-154">b.</span></span> <span data-ttu-id="f10a9-155">Aggiungere hello seguente codice dopo hello `myDictionary.TryGetValueAsync` chiamare</span><span class="sxs-lookup"><span data-stu-id="f10a9-155">Add hello following code after hello `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="f10a9-156">Viene segnalata l'integrità di una replica, perché la segnalazione viene eseguita da un servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="f10a9-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="f10a9-157">Hello `HealthInformation` parametro archivia le informazioni hello integrità problema da segnalare.</span><span class="sxs-lookup"><span data-stu-id="f10a9-157">hello `HealthInformation` parameter stores information about hello health issue that's being reported.</span></span>
   
    <span data-ttu-id="f10a9-158">Se è stato creato un servizio senza stato, utilizzare hello seguente di codice</span><span class="sxs-lookup"><span data-stu-id="f10a9-158">If you had created a stateless service, use hello following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="f10a9-159">Se il servizio è in esecuzione con privilegi di amministratore o se hello cluster non è [sicura](service-fabric-cluster-security.md), è inoltre possibile utilizzare `FabricClient` integrità tooreport come illustrato nell'hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="f10a9-159">If your service is running with admin privileges or if hello cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` tooreport health as shown in hello following steps.</span></span>  
   
    <span data-ttu-id="f10a9-160">a.</span><span class="sxs-lookup"><span data-stu-id="f10a9-160">a.</span></span> <span data-ttu-id="f10a9-161">Creare hello `FabricClient` istanza dopo hello `var myDictionary` dichiarazione.</span><span class="sxs-lookup"><span data-stu-id="f10a9-161">Create hello `FabricClient` instance after hello `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="f10a9-162">b.</span><span class="sxs-lookup"><span data-stu-id="f10a9-162">b.</span></span> <span data-ttu-id="f10a9-163">Aggiungere hello seguente codice dopo hello `myDictionary.TryGetValueAsync` chiamare.</span><span class="sxs-lookup"><span data-stu-id="f10a9-163">Add hello following code after hello `myDictionary.TryGetValueAsync` call.</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
       var replicaHealthReport = new StatefulServiceReplicaHealthReport(
            this.Context.PartitionId,
            this.Context.ReplicaId,
            new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error));
        fabricClient.HealthManager.ReportHealth(replicaHealthReport);
    }
    ```
5. <span data-ttu-id="f10a9-164">Di seguito simulare l'errore e per visualizzare in strumenti di monitoraggio integrità hello.</span><span class="sxs-lookup"><span data-stu-id="f10a9-164">Let's simulate this failure and see it show up in hello health monitoring tools.</span></span> <span data-ttu-id="f10a9-165">Errore di hello toosimulate, commento hello nella prima riga integrità hello reporting codice aggiunto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f10a9-165">toosimulate hello failure, comment out hello first line in hello health reporting code that you added earlier.</span></span> <span data-ttu-id="f10a9-166">Dopo la prima riga hello è come commento, codice hello avrà un aspetto simile hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="f10a9-166">After you comment out hello first line, hello code will look like hello following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="f10a9-167">Questo codice viene generato ogni volta che il rapporto di stato hello `RunAsync` esegue.</span><span class="sxs-lookup"><span data-stu-id="f10a9-167">This code fires hello health report each time `RunAsync` executes.</span></span> <span data-ttu-id="f10a9-168">Dopo aver modificato hello, premere **F5** toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f10a9-168">After you make hello change, press **F5** toorun hello application.</span></span>
6. <span data-ttu-id="f10a9-169">Dopo l'applicazione hello è in esecuzione, aprire Service Fabric Explorer toocheck hello integrità hello applicazione.</span><span class="sxs-lookup"><span data-stu-id="f10a9-169">After hello application is running, open Service Fabric Explorer toocheck hello health of hello application.</span></span> <span data-ttu-id="f10a9-170">Questa volta, Service Fabric Explorer mostra che l'applicazione hello è integra.</span><span class="sxs-lookup"><span data-stu-id="f10a9-170">This time, Service Fabric Explorer shows that hello application is unhealthy.</span></span> <span data-ttu-id="f10a9-171">Ciò è dovuto errore hello che è stato segnalato dal codice hello che è stato aggiunto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f10a9-171">This is because of hello error that was reported from hello code that we added previously.</span></span>
   
    ![Applicazione non integra in Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="f10a9-173">Se si seleziona la replica primaria hello nella visualizzazione ad albero di hello di Service Fabric Explorer, si noterà che **lo stato di integrità** indica un errore troppo.</span><span class="sxs-lookup"><span data-stu-id="f10a9-173">If you select hello primary replica in hello tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="f10a9-174">Service Fabric Explorer consente inoltre di visualizzare i report di integrità hello dettagli che sono stati aggiunti toohello `HealthInformation` parametro hello codice.</span><span class="sxs-lookup"><span data-stu-id="f10a9-174">Service Fabric Explorer also displays hello health report details that were added toohello `HealthInformation` parameter in hello code.</span></span> <span data-ttu-id="f10a9-175">È possibile visualizzare hello stesso report sull'integrità in PowerShell e hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f10a9-175">You can see hello same health reports in PowerShell and hello Azure portal.</span></span>
   
    ![Integrità della replica in Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="f10a9-177">Questo report rimane nel gestore integrità hello fino a quando non viene sostituita da un altro report o fino a quando la replica viene eliminata.</span><span class="sxs-lookup"><span data-stu-id="f10a9-177">This report remains in hello health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="f10a9-178">Poiché non è stato impostato `TimeToLive` per questo rapporto di stato di hello `HealthInformation` oggetto report hello non scade mai.</span><span class="sxs-lookup"><span data-stu-id="f10a9-178">Because we did not set `TimeToLive` for this health report in hello `HealthInformation` object, hello report never expires.</span></span>

<span data-ttu-id="f10a9-179">È consigliabile che l'integrità deve essere segnalato al livello più granulare hello, ovvero in questo caso è hello replica.</span><span class="sxs-lookup"><span data-stu-id="f10a9-179">We recommend that health should be reported on hello most granular level, which in this case is hello replica.</span></span> <span data-ttu-id="f10a9-180">È anche possibile segnalare lo stato di integrità relativo all'oggetto `Partition`.</span><span class="sxs-lookup"><span data-stu-id="f10a9-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="f10a9-181">lo stato su tooreport `Application`, `DeployedApplication`, e `DeployedServicePackage`, utilizzare `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="f10a9-181">tooreport health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="f10a9-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f10a9-182">Next steps</span></span>
* [<span data-ttu-id="f10a9-183">Introduzione al monitoraggio dell'integrità di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f10a9-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* <span data-ttu-id="f10a9-184">[REST API for reporting service health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service) (API REST per segnalare l'integrità del servizio)</span><span class="sxs-lookup"><span data-stu-id="f10a9-184">[REST API for reporting service health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)</span></span>
* <span data-ttu-id="f10a9-185">[REST API for reporting application health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application) (API REST per segnalare l'integrità dell'applicazione)</span><span class="sxs-lookup"><span data-stu-id="f10a9-185">[REST API for reporting application health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)</span></span>

