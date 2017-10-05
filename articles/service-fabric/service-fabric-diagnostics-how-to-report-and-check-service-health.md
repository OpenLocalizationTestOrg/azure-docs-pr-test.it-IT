---
title: "Creare report e verificare l'integrità con Azure Service Fabric | Documentazione Microsoft"
description: "Informazioni su come inviare report di integrità dal codice del servizio e su come verificare l'integrità del servizio usando gli strumenti di monitoraggio dell'integrità forniti da Azure Service Fabric."
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
ms.openlocfilehash: 83981d5bec14c06c509f1a8a4153dc23298f5ce0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="report-and-check-service-health"></a><span data-ttu-id="20a2c-103">Creare report e verificare l'integrità dei servizi</span><span class="sxs-lookup"><span data-stu-id="20a2c-103">Report and check service health</span></span>
<span data-ttu-id="20a2c-104">Quando si verificano problemi nei servizi, la possibilità di rispondere e correggere interruzioni ed eventi imprevisti dipende dalla capacità di rilevare i problemi in tempi rapidi.</span><span class="sxs-lookup"><span data-stu-id="20a2c-104">When your services encounter problems, your ability to respond to and fix incidents and outages depends on your ability to detect the issues quickly.</span></span> <span data-ttu-id="20a2c-105">Se si segnalano problemi ed errori allo strumento di gestione dell'integrità di Azure Service Fabric dal codice del servizio, è possibile usare gli strumenti standard di monitoraggio dell'integrità forniti da Service Fabric per verificare lo stato di integrità.</span><span class="sxs-lookup"><span data-stu-id="20a2c-105">If you report problems and failures to the Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides to check the health status.</span></span>

<span data-ttu-id="20a2c-106">È possibile segnalare lo stato di integrità dal servizio in tre modi:</span><span class="sxs-lookup"><span data-stu-id="20a2c-106">There are three ways that you can report health from the service:</span></span>

* <span data-ttu-id="20a2c-107">Usare gli oggetti [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) o [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext).</span><span class="sxs-lookup"><span data-stu-id="20a2c-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="20a2c-108">È possibile usare gli oggetti `Partition` e `CodePackageActivationContext` per segnalare lo stato di integrità degli elementi appartenenti al contesto corrente.</span><span class="sxs-lookup"><span data-stu-id="20a2c-108">You can use the `Partition` and `CodePackageActivationContext` objects to report the health of elements that are part of the current context.</span></span> <span data-ttu-id="20a2c-109">Il codice in esecuzione come parte di una replica può ad esempio segnalare lo stato di integrità solo sulla replica, sulla partizione a cui appartiene e sull'applicazione di cui fa parte.</span><span class="sxs-lookup"><span data-stu-id="20a2c-109">For example, code that runs as part of a replica can report health only on that replica, the partition that it belongs to, and the application that it is a part of.</span></span>
* <span data-ttu-id="20a2c-110">Usare `FabricClient`.</span><span class="sxs-lookup"><span data-stu-id="20a2c-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="20a2c-111">È possibile usare `FabricClient` per segnalare lo stato di integrità dal codice del servizio se il cluster non è [sicuro](service-fabric-cluster-security.md) o se il servizio è in esecuzione con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="20a2c-111">You can use `FabricClient` to report health from the service code if the cluster is not [secure](service-fabric-cluster-security.md) or if the service is running with admin privileges.</span></span> <span data-ttu-id="20a2c-112">La maggior parte degli scenari reali non usa cluster non protetti oppure fornisce privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="20a2c-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="20a2c-113">Con `FabricClient`è possibile segnalare lo stato di integrità per qualsiasi entità appartenente al cluster.</span><span class="sxs-lookup"><span data-stu-id="20a2c-113">With `FabricClient`, you can report health on any entity that is a part of the cluster.</span></span> <span data-ttu-id="20a2c-114">Idealmente il codice del servizio dovrebbe tuttavia inviare solo report correlati alla propria integrità.</span><span class="sxs-lookup"><span data-stu-id="20a2c-114">Ideally, however, service code should only send reports that are related to its own health.</span></span>
* <span data-ttu-id="20a2c-115">Usare le API REST a livello di cluster, applicazione, applicazione distribuita, servizio, pacchetto di servizio, replica o nodo.</span><span class="sxs-lookup"><span data-stu-id="20a2c-115">Use the REST APIs at the cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="20a2c-116">In questo modo è possibile segnalare l'integrità direttamente da un contenitore.</span><span class="sxs-lookup"><span data-stu-id="20a2c-116">This can be used to report health from within a container.</span></span>

<span data-ttu-id="20a2c-117">Questo articolo illustra un esempio in cui viene segnalato lo stato di integrità dal codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="20a2c-117">This article walks you through an example that reports health from the service code.</span></span> <span data-ttu-id="20a2c-118">L'esempio mostra anche come usare gli strumenti forniti da Service Fabric per verificare lo stato di integrità.</span><span class="sxs-lookup"><span data-stu-id="20a2c-118">The example also shows how the tools provided by Service Fabric can be used to check the health status.</span></span> <span data-ttu-id="20a2c-119">Questo articolo può essere usato come breve introduzione alle funzionalità di monitoraggio dell'integrità di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="20a2c-119">This article is intended to be a quick introduction to the health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="20a2c-120">Per informazioni più dettagliate, è possibile leggere la serie di articoli di approfondimento sull'integrità accessibili dal collegamento presente alla fine di questo documento.</span><span class="sxs-lookup"><span data-stu-id="20a2c-120">For more detailed information, you can read the series of in-depth articles about health that start with the link at the end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20a2c-121">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="20a2c-121">Prerequisites</span></span>
<span data-ttu-id="20a2c-122">È necessario che siano installati i seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="20a2c-122">You must have the following installed:</span></span>

* <span data-ttu-id="20a2c-123">Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="20a2c-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="20a2c-124">Service Fabric SDK</span><span class="sxs-lookup"><span data-stu-id="20a2c-124">Service Fabric SDK</span></span>

## <a name="to-create-a-local-secure-dev-cluster"></a><span data-ttu-id="20a2c-125">Per creare un cluster di sviluppo sicuro locale</span><span class="sxs-lookup"><span data-stu-id="20a2c-125">To create a local secure dev cluster</span></span>
* <span data-ttu-id="20a2c-126">Aprire PowerShell con privilegi di amministratore ed eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="20a2c-126">Open PowerShell with admin privileges, and run the following commands:</span></span>

![Comandi che mostrano come creare un cluster di sviluppo sicuro locale](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="to-deploy-an-application-and-check-its-health"></a><span data-ttu-id="20a2c-128">Per distribuire un'applicazione e verificarne l'integrità</span><span class="sxs-lookup"><span data-stu-id="20a2c-128">To deploy an application and check its health</span></span>
1. <span data-ttu-id="20a2c-129">Aprire Visual Studio come amministratore.</span><span class="sxs-lookup"><span data-stu-id="20a2c-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="20a2c-130">Creare un progetto usando il modello **Servizio con stato** .</span><span class="sxs-lookup"><span data-stu-id="20a2c-130">Create a project by using the **Stateful Service** template.</span></span>
   
    ![Creare un'applicazione di Service Fabric con un servizio con stato](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="20a2c-132">Premere **F5** per eseguire l'applicazione in modalità di debug.</span><span class="sxs-lookup"><span data-stu-id="20a2c-132">Press **F5** to run the application in debug mode.</span></span> <span data-ttu-id="20a2c-133">L'applicazione verrà distribuita nel cluster locale.</span><span class="sxs-lookup"><span data-stu-id="20a2c-133">The application is deployed to the local cluster.</span></span>
4. <span data-ttu-id="20a2c-134">Dopo aver eseguito l'applicazione, fare clic con il tasto destro del mouse sull'icona di Local Cluster Manager nell'area di notifica e aprire Service Fabric Explorer selezionando **Gestisci cluster locale** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="20a2c-134">After the application is running, right-click the Local Cluster Manager icon in the notification area and select **Manage Local Cluster** from the shortcut menu to open Service Fabric Explorer.</span></span>
   
    ![Apertura di Service Fabric Explorer dall'area di notifica](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="20a2c-136">L'integrità dell'applicazione sarà simile a quella visualizzata in questa immagine.</span><span class="sxs-lookup"><span data-stu-id="20a2c-136">The application health should be displayed as in this image.</span></span> <span data-ttu-id="20a2c-137">A questo punto, l'applicazione dovrebbe essere integra e senza errori.</span><span class="sxs-lookup"><span data-stu-id="20a2c-137">At this time, the application should be healthy with no errors.</span></span>
   
    ![Applicazione integra in Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="20a2c-139">Per verificare l'integrità è possibile usare anche PowerShell.</span><span class="sxs-lookup"><span data-stu-id="20a2c-139">You can also check the health by using PowerShell.</span></span> <span data-ttu-id="20a2c-140">È possibile verificare l'integrità di un'applicazione usando ```Get-ServiceFabricApplicationHealth``` e l'integrità di un servizio usando ```Get-ServiceFabricServiceHealth```.</span><span class="sxs-lookup"><span data-stu-id="20a2c-140">You can use ```Get-ServiceFabricApplicationHealth``` to check an application's health, and you can use ```Get-ServiceFabricServiceHealth``` to check a service's health.</span></span> <span data-ttu-id="20a2c-141">Il report sullo stato di integrità per la stessa applicazione in PowerShell è visualizzato in questa immagine.</span><span class="sxs-lookup"><span data-stu-id="20a2c-141">The health report for the same application in PowerShell is in this image.</span></span>
   
    ![Applicazione integra in PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="to-add-custom-health-events-to-your-service-code"></a><span data-ttu-id="20a2c-143">Per aggiungere eventi di integrità personalizzati al codice del servizio</span><span class="sxs-lookup"><span data-stu-id="20a2c-143">To add custom health events to your service code</span></span>
<span data-ttu-id="20a2c-144">I modelli di progetto di Service Fabric in Visual Studio contengono codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="20a2c-144">The Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="20a2c-145">La procedura seguente illustra come segnalare eventi di integrità personalizzati dal codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="20a2c-145">The following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="20a2c-146">Questi report vengono automaticamente visualizzati negli strumenti standard per il monitoraggio dell'integrità forniti da Service Fabric, come Service Fabric Explorer, la vista del portale di Azure relativa all'integrità e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="20a2c-146">Such reports show up automatically in the standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="20a2c-147">Aprire nuovamente l'applicazione creata in precedenza in Visual Studio o crearne una nuova usando il modello di Visual Studio **Servizio con stato** .</span><span class="sxs-lookup"><span data-stu-id="20a2c-147">Reopen the application that you created previously in Visual Studio, or create a new application by using the **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="20a2c-148">Aprire il file Stateful1.cs e cercare la chiamata `myDictionary.TryGetValueAsync` nel metodo `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="20a2c-148">Open the Stateful1.cs file, and find the `myDictionary.TryGetValueAsync` call in the `RunAsync` method.</span></span> <span data-ttu-id="20a2c-149">Si noterà che questo metodo restituisce un `result` contenente il valore corrente del contatore, poiché la logica principale in questa applicazione è quella di mantenere un conteggio in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="20a2c-149">You can see that this method returns a `result` that holds the current value of the counter because the key logic in this application is to keep a count running.</span></span> <span data-ttu-id="20a2c-150">Nel caso di un'applicazione reale con un errore dovuto alla mancanza di risultati, può essere opportuno contrassegnare l'evento.</span><span class="sxs-lookup"><span data-stu-id="20a2c-150">If this were a real application, and if the lack of result represented a failure, you would want to flag that event.</span></span>
3. <span data-ttu-id="20a2c-151">Per segnalare un evento di integrità per un errore dovuto alla mancanza di risultati, aggiungere la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="20a2c-151">To report a health event when the lack of result represents a failure, add the following steps.</span></span>
   
    <span data-ttu-id="20a2c-152">a.</span><span class="sxs-lookup"><span data-stu-id="20a2c-152">a.</span></span> <span data-ttu-id="20a2c-153">Aggiungere lo spazio dei nomi `System.Fabric.Health` al file Stateful1.cs.</span><span class="sxs-lookup"><span data-stu-id="20a2c-153">Add the `System.Fabric.Health` namespace to the Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="20a2c-154">b.</span><span class="sxs-lookup"><span data-stu-id="20a2c-154">b.</span></span> <span data-ttu-id="20a2c-155">Aggiungere il codice seguente dopo la chiamata di `myDictionary.TryGetValueAsync`</span><span class="sxs-lookup"><span data-stu-id="20a2c-155">Add the following code after the `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="20a2c-156">Viene segnalata l'integrità di una replica, perché la segnalazione viene eseguita da un servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="20a2c-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="20a2c-157">Il parametro `HealthInformation` archivia informazioni relative al problema di integrità segnalato.</span><span class="sxs-lookup"><span data-stu-id="20a2c-157">The `HealthInformation` parameter stores information about the health issue that's being reported.</span></span>
   
    <span data-ttu-id="20a2c-158">Se è stato creato un servizio senza stato, utilizzare il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="20a2c-158">If you had created a stateless service, use the following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="20a2c-159">Se il servizio è in esecuzione con privilegi di amministratore o se il cluster non è [sicuro](service-fabric-cluster-security.md), è anche possibile usare `FabricClient` per segnalare lo stato di integrità, come illustrato nella procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="20a2c-159">If your service is running with admin privileges or if the cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` to report health as shown in the following steps.</span></span>  
   
    <span data-ttu-id="20a2c-160">a.</span><span class="sxs-lookup"><span data-stu-id="20a2c-160">a.</span></span> <span data-ttu-id="20a2c-161">Creare l'istanza di `FabricClient` dopo la dichiarazione `var myDictionary`.</span><span class="sxs-lookup"><span data-stu-id="20a2c-161">Create the `FabricClient` instance after the `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="20a2c-162">b.</span><span class="sxs-lookup"><span data-stu-id="20a2c-162">b.</span></span> <span data-ttu-id="20a2c-163">Aggiungere il codice seguente dopo la chiamata di `myDictionary.TryGetValueAsync` .</span><span class="sxs-lookup"><span data-stu-id="20a2c-163">Add the following code after the `myDictionary.TryGetValueAsync` call.</span></span>
   
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
5. <span data-ttu-id="20a2c-164">Simulare l'errore e osservare come venga visualizzato negli strumenti di monitoraggio dello stato.</span><span class="sxs-lookup"><span data-stu-id="20a2c-164">Let's simulate this failure and see it show up in the health monitoring tools.</span></span> <span data-ttu-id="20a2c-165">Per simulare l'errore, impostare la prima riga come commento nel codice del report di integrità aggiunto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="20a2c-165">To simulate the failure, comment out the first line in the health reporting code that you added earlier.</span></span> <span data-ttu-id="20a2c-166">Al termine di questa operazione, il codice sarà simile all'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="20a2c-166">After you comment out the first line, the code will look like the following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="20a2c-167">Questo codice genera il report di integrità ogni volta che si esegue `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="20a2c-167">This code fires the health report each time `RunAsync` executes.</span></span> <span data-ttu-id="20a2c-168">Dopo aver apportato la modifica, premere **F5** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="20a2c-168">After you make the change, press **F5** to run the application.</span></span>
6. <span data-ttu-id="20a2c-169">Dopo l'esecuzione dell'applicazione, aprire Service Fabric Explorer per verificare l'integrità dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="20a2c-169">After the application is running, open Service Fabric Explorer to check the health of the application.</span></span> <span data-ttu-id="20a2c-170">In questo caso, Service Fabric Explorer indica un problema di integrità dell'applicazione,</span><span class="sxs-lookup"><span data-stu-id="20a2c-170">This time, Service Fabric Explorer shows that the application is unhealthy.</span></span> <span data-ttu-id="20a2c-171">a causa dell'errore segnalato dal codice aggiunto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="20a2c-171">This is because of the error that was reported from the code that we added previously.</span></span>
   
    ![Applicazione non integra in Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="20a2c-173">Se si seleziona la replica primaria nella visualizzazione ad albero di Service Fabric Explorer, viene visualizzato anche in questo caso un errore dello **stato di integrità** .</span><span class="sxs-lookup"><span data-stu-id="20a2c-173">If you select the primary replica in the tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="20a2c-174">In Service Fabric Explorer vengono visualizzati anche i dettagli del report di integrità aggiunti al parametro `HealthInformation` nel codice.</span><span class="sxs-lookup"><span data-stu-id="20a2c-174">Service Fabric Explorer also displays the health report details that were added to the `HealthInformation` parameter in the code.</span></span> <span data-ttu-id="20a2c-175">È possibile visualizzare gli stessi report di integrità anche in PowerShell e nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="20a2c-175">You can see the same health reports in PowerShell and the Azure portal.</span></span>
   
    ![Integrità della replica in Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="20a2c-177">Questo report resta in Health Manager finché non viene sostituito da un altro o finché la replica non viene eliminata.</span><span class="sxs-lookup"><span data-stu-id="20a2c-177">This report remains in the health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="20a2c-178">Poiché per questo report di integrità non è stato impostato un valore `TimeToLive` nell'oggetto `HealthInformation`, il report non avrà scadenza.</span><span class="sxs-lookup"><span data-stu-id="20a2c-178">Because we did not set `TimeToLive` for this health report in the `HealthInformation` object, the report never expires.</span></span>

<span data-ttu-id="20a2c-179">È consigliabile creare report sull'integrità al livello più dettagliato possibile, che in questo caso corrisponde alla replica.</span><span class="sxs-lookup"><span data-stu-id="20a2c-179">We recommend that health should be reported on the most granular level, which in this case is the replica.</span></span> <span data-ttu-id="20a2c-180">È anche possibile segnalare lo stato di integrità relativo all'oggetto `Partition`.</span><span class="sxs-lookup"><span data-stu-id="20a2c-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="20a2c-181">Per segnalare lo stato di integrità relativo a `Application`, `DeployedApplication` e `DeployedServicePackage`, usare `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="20a2c-181">To report health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="20a2c-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="20a2c-182">Next steps</span></span>
* [<span data-ttu-id="20a2c-183">Introduzione al monitoraggio dell'integrità di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="20a2c-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* <span data-ttu-id="20a2c-184">[REST API for reporting service health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service) (API REST per segnalare l'integrità del servizio)</span><span class="sxs-lookup"><span data-stu-id="20a2c-184">[REST API for reporting service health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)</span></span>
* <span data-ttu-id="20a2c-185">[REST API for reporting application health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application) (API REST per segnalare l'integrità dell'applicazione)</span><span class="sxs-lookup"><span data-stu-id="20a2c-185">[REST API for reporting application health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)</span></span>

