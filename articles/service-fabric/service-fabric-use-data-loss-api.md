---
title: aaaHow tooInvoke perdite di dati nei servizi di infrastruttura | Documenti Microsoft
description: Viene descritto come toouse hello perdita di dati api
services: service-fabric
documentationcenter: .net
author: LMWF
manager: rsinha
editor: 
ms.assetid: f4e70f6f-cad9-4a3e-9655-009b4db09c6d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/19/2016
ms.author: lemai
redirect_url: /azure/service-fabric/service-fabric-testability-overview
ms.openlocfilehash: 014c7ebfd2c42d79a5fe1802ecc3fa0c1f26f9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinvoke-data-loss-on-services"></a><span data-ttu-id="8382e-103">Come tooInvoke perdite di dati nei servizi</span><span class="sxs-lookup"><span data-stu-id="8382e-103">How tooInvoke Data Loss on Services</span></span>
> [!WARNING]
> <span data-ttu-id="8382e-104">Questo documento viene descritto come perdita di dati toocause nei servizi e deve essere utilizzata con cautela.</span><span class="sxs-lookup"><span data-stu-id="8382e-104">This document describe how toocause data loss in your services, and should be used with care.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="8382e-105">Introduzione</span><span class="sxs-lookup"><span data-stu-id="8382e-105">Introduction</span></span>
<span data-ttu-id="8382e-106">È possibile richiamare la perdita di dati in una partizione del servizio Service Fabric chiamando StartPartitionDataLossAsync().</span><span class="sxs-lookup"><span data-stu-id="8382e-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span></span>  <span data-ttu-id="8382e-107">Questa api utilizza hello attacco intrusivo nel codice di errore e il servizio di analisi tooperform hello lavoro toocause dati perdita condizioni.</span><span class="sxs-lookup"><span data-stu-id="8382e-107">This api uses hello Fault Injection and Analysis Service tooperform hello work toocause data loss conditions.</span></span>

## <a name="using-hello-fault-injection-and-analysis-service"></a><span data-ttu-id="8382e-108">Utilizzo di hello attacco intrusivo nel codice di errore e Analysis Services</span><span class="sxs-lookup"><span data-stu-id="8382e-108">Using hello Fault Injection and Analysis Service</span></span>
<span data-ttu-id="8382e-109">Hello attacco intrusivo nel codice di errore e Analysis Services supporta attualmente hello seguenti API nel seguente grafico hello.</span><span class="sxs-lookup"><span data-stu-id="8382e-109">hello Fault Injection and Analysis Service currently supports hello following APIs in hello chart below.</span></span>  <span data-ttu-id="8382e-110">Hello nella parte destra del grafico hello sono hello cmdlet di PowerShell corrispondente.</span><span class="sxs-lookup"><span data-stu-id="8382e-110">hello right side of hello chart shows hello corresponding PowerShell cmdlet.</span></span>  <span data-ttu-id="8382e-111">Consultare la documentazione msdn toohello ogni API per ulteriori informazioni su ciascuna di esse.</span><span class="sxs-lookup"><span data-stu-id="8382e-111">Please refer toohello msdn documentation on each API for more information on each one.</span></span>

| <span data-ttu-id="8382e-112">API C#</span><span class="sxs-lookup"><span data-stu-id="8382e-112">C# API</span></span> | <span data-ttu-id="8382e-113">Cmdlet di PowerShell</span><span class="sxs-lookup"><span data-stu-id="8382e-113">PowerShell Cmdlet</span></span> |
| --- | ---:|
| <span data-ttu-id="8382e-114">[StartPartitionDataLossAsync][dl]</span><span class="sxs-lookup"><span data-stu-id="8382e-114">[StartPartitionDataLossAsync][dl]</span></span> |<span data-ttu-id="8382e-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span><span class="sxs-lookup"><span data-stu-id="8382e-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span></span> |
| <span data-ttu-id="8382e-116">[StartPartitionQuorumLossAsync][ql]</span><span class="sxs-lookup"><span data-stu-id="8382e-116">[StartPartitionQuorumLossAsync][ql]</span></span> |<span data-ttu-id="8382e-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span><span class="sxs-lookup"><span data-stu-id="8382e-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span></span> |
| <span data-ttu-id="8382e-118">[StartPartitionRestartAsync][rp]</span><span class="sxs-lookup"><span data-stu-id="8382e-118">[StartPartitionRestartAsync][rp]</span></span> |<span data-ttu-id="8382e-119">[Start-ServiceFabricPartitionRestart][psrp]</span><span class="sxs-lookup"><span data-stu-id="8382e-119">[Start-ServiceFabricPartitionRestart][psrp]</span></span> |

## <a name="conceptual-overview-of-running-a-command"></a><span data-ttu-id="8382e-120">Panoramica concettuale dell'esecuzione di un comando</span><span class="sxs-lookup"><span data-stu-id="8382e-120">Conceptual Overview of Running a Command</span></span>
<span data-ttu-id="8382e-121">attacco intrusivo nel codice di errore e il servizio di analisi utilizzato un modello asincrono in cui viene avviata hello comando con un'API, cui tooas hello "Start" API in questo documento, quindi verifica hello lo stato di avanzamento di questo comando utilizza un'API "GetProgress" fino a quando non è stato raggiunto un terminale Hello stato, oppure finché non si annullarla.</span><span class="sxs-lookup"><span data-stu-id="8382e-121">hello Fault Injection and Analysis Service uses an asynchronous model where you start hello command with one API, referred tooas hello “Start” API in this document, then checks hello progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span></span>
<span data-ttu-id="8382e-122">toostart un comando, chiamata API "Start" hello per le API corrispondenti hello.</span><span class="sxs-lookup"><span data-stu-id="8382e-122">toostart a command, call hello “Start” API for hello corresponding API.</span></span>  <span data-ttu-id="8382e-123">Questa API restituisce quando hello attacco intrusivo nel codice di errore e il servizio di analisi ha accettato la richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="8382e-123">This API returns when hello Fault Injection and Analysis Service has accepted hello request.</span></span>  <span data-ttu-id="8382e-124">Tuttavia non indica a che punto si trova l'esecuzione del comando e neppure se è già stato avviato.</span><span class="sxs-lookup"><span data-stu-id="8382e-124">However, it does not indicate how far a command has run, or even if it has started yet.</span></span>  <span data-ttu-id="8382e-125">In ordine toocheck lo stato di avanzamento di un comando, chiamare l'API corrispondente toohello "Start" API in precedenza denominata "GetProgress" hello.</span><span class="sxs-lookup"><span data-stu-id="8382e-125">In order toocheck progress of a command, call hello “GetProgress” API that corresponds toohello “Start” API previously called.</span></span>  <span data-ttu-id="8382e-126">Hello "GetProgress" API restituirà un oggetto che indica lo stato corrente di hello del comando hello all'interno delle proprietà di stato.</span><span class="sxs-lookup"><span data-stu-id="8382e-126">hello “GetProgress” API will return an object indicating hello current status of hello command inside its State property.</span></span>  <span data-ttu-id="8382e-127">Un comando viene eseguito all'infinito finché:</span><span class="sxs-lookup"><span data-stu-id="8382e-127">A command runs indefinitely until:</span></span>

1. <span data-ttu-id="8382e-128">Viene completato correttamente.</span><span class="sxs-lookup"><span data-stu-id="8382e-128">It completes successfully.</span></span>  <span data-ttu-id="8382e-129">Se si chiama "GetProgress" su di essa in questo caso, lo stato dell'oggetto di stato di avanzamento hello verrà completato.</span><span class="sxs-lookup"><span data-stu-id="8382e-129">If you call “GetProgress” on it in this case, hello progress object’s State will be Completed.</span></span>
2. <span data-ttu-id="8382e-130">Si verifica un errore irreversibile.</span><span class="sxs-lookup"><span data-stu-id="8382e-130">It encounters a fatal error.</span></span>  <span data-ttu-id="8382e-131">Se si chiama "GetProgress" su di essa in questo caso, lo stato dell'oggetto di stato di avanzamento hello verrà essere con errori</span><span class="sxs-lookup"><span data-stu-id="8382e-131">If you call “GetProgress” on it in this case, hello progress object’s State will be Faulted</span></span>
3. <span data-ttu-id="8382e-132">Annullarlo tramite hello [CancelTestCommandAsync] [ cancel] API, o [Stop ServiceFabricTestCommand] [ cancelps] cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8382e-132">You cancel it through hello [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span></span>  <span data-ttu-id="8382e-133">Se si chiama "GetProgress" su di essa in questo caso, hello stato di avanzamento dell'oggetto sarà annullato o ForceCancelled, a seconda di un toothat argomento API.</span><span class="sxs-lookup"><span data-stu-id="8382e-133">If you call “GetProgress” on it in this case, hello progress object’s State will be either Cancelled or ForceCancelled, depending on an argument toothat API.</span></span>  <span data-ttu-id="8382e-134">Vedere la documentazione di hello per [CancelTestCommandAsync] [ cancel] per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="8382e-134">See hello documentation for [CancelTestCommandAsync][cancel] for more details.</span></span>

## <a name="details-of-running-a-command"></a><span data-ttu-id="8382e-135">Dettagli dell'esecuzione di un comando</span><span class="sxs-lookup"><span data-stu-id="8382e-135">Details of Running a Command</span></span>
<span data-ttu-id="8382e-136">In ordine toostart un comando, chiamare hello avviare API con argomenti hello previsto.</span><span class="sxs-lookup"><span data-stu-id="8382e-136">In order toostart a command, call hello Start API with hello expected arguments.</span></span>  <span data-ttu-id="8382e-137">Tutte le API Start dispongono di un argomento Guid denominato operationId.</span><span class="sxs-lookup"><span data-stu-id="8382e-137">All Start APIs have a Guid argument named operationId.</span></span>  <span data-ttu-id="8382e-138">È necessario tenere traccia delle argomento operationId hello, poiché è utilizzato tootrack lo stato di avanzamento di questo comando.</span><span class="sxs-lookup"><span data-stu-id="8382e-138">You should keep track of hello operationId argument, since it is used tootrack progress of this command.</span></span>  <span data-ttu-id="8382e-139">Questo metodo deve essere passato in hello "GetProgress" API in corso tootrack ordine del comando hello.</span><span class="sxs-lookup"><span data-stu-id="8382e-139">This must be passed into hello “GetProgress” API in order tootrack progress of hello command.</span></span>  <span data-ttu-id="8382e-140">ID operazione Hello deve essere univoci.</span><span class="sxs-lookup"><span data-stu-id="8382e-140">hello operationId must be unique.</span></span>

<span data-ttu-id="8382e-141">Dopo l'esito positivo della chiamata hello avviare API, hello GetProgress API deve essere chiamato in un ciclo fino a quando hello restituito lo stato di avanzamento proprietà State dell'oggetto viene completato.</span><span class="sxs-lookup"><span data-stu-id="8382e-141">After successfully calling hello Start API, hello GetProgress API should be called in a loop until hello returned progress object’s State property is Completed.</span></span>  <span data-ttu-id="8382e-142">È necessario provare di nuovo tutti i [FabricTransientException][fte] e OperationCanceledException.</span><span class="sxs-lookup"><span data-stu-id="8382e-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span></span>
<span data-ttu-id="8382e-143">Quando il comando hello ha raggiunto uno stato finale (Completed, Faulted o annullato), hello restituito proprietà Result dell'oggetto di stato di avanzamento saranno disponibili informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="8382e-143">When hello command has reached a terminal state (Completed, Faulted, or Cancelled), hello returned progress object’s Result property will have additional information.</span></span>  <span data-ttu-id="8382e-144">Se lo stato di hello viene completato, Result.SelectedPartition.PartitionId conterrà l'id di partizione hello che è stato selezionato.</span><span class="sxs-lookup"><span data-stu-id="8382e-144">If hello state is Completed, Result.SelectedPartition.PartitionId will contain hello partition id that was selected.</span></span>  <span data-ttu-id="8382e-145">Result.Exception sarà null.</span><span class="sxs-lookup"><span data-stu-id="8382e-145">Result.Exception will be null.</span></span>  <span data-ttu-id="8382e-146">Se lo stato di hello è Faulted, sarà necessario Result.Exception hello motivo hello attacco intrusivo nel codice di errore e il comando di hello Analysis Services con errori.</span><span class="sxs-lookup"><span data-stu-id="8382e-146">If hello state is Faulted, Result.Exception will have hello reason hello Fault Injection and Analysis Service faulted hello command.</span></span>  <span data-ttu-id="8382e-147">Result.SelectedPartition.PartitionId avrà id di partizione hello che è stato selezionato.</span><span class="sxs-lookup"><span data-stu-id="8382e-147">Result.SelectedPartition.PartitionId will have hello partition id that was selected.</span></span>  <span data-ttu-id="8382e-148">In alcuni casi, il comando hello potrebbe non proseguita fino toochoose una partizione.</span><span class="sxs-lookup"><span data-stu-id="8382e-148">In some situations, hello command may not have proceeded far enough toochoose a partition.</span></span>  <span data-ttu-id="8382e-149">In tal caso, hello PartitionId sarà pari a 0.</span><span class="sxs-lookup"><span data-stu-id="8382e-149">In that case, hello PartitionId will be 0.</span></span>  <span data-ttu-id="8382e-150">Se lo stato di hello viene annullato, Result.Exception sarà null.</span><span class="sxs-lookup"><span data-stu-id="8382e-150">If hello state is Cancelled, Result.Exception will be null.</span></span>  <span data-ttu-id="8382e-151">Ad esempio hello case Faulted, Result.SelectedPartition.PartitionId avrà un id di partizione hello che è stato scelto, ma se il comando hello ha non viene eseguita fino toodo così, sarà 0.</span><span class="sxs-lookup"><span data-stu-id="8382e-151">Like hello Faulted case, Result.SelectedPartition.PartitionId will have hello partition id that was chosen, but if hello command has not proceeded far enough toodo so, it will be 0.</span></span>  <span data-ttu-id="8382e-152">Consultare inoltre toohello esempio riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8382e-152">Please also refer toohello sample below.</span></span>

<span data-ttu-id="8382e-153">codice di esempio Hello riportato di seguito viene illustrato come toostart quindi controllare lo stato di avanzamento in una perdita di dati toocause comando su una partizione specifica.</span><span class="sxs-lookup"><span data-stu-id="8382e-153">hello sample code below shows how toostart then check progress on a command toocause data loss on a specific partition.</span></span>

```csharp
    static async Task PerformDataLossSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/MyService");

        // hello id of hello target partition inside hello target service
        Guid targetPartitionId = new Guid("00000000-0000-0000-0000-000002233445");

        PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(targetServiceName, targetPartitionId);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.        

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                // In a terminal state .Result.SelectedPartition.PartitionId will have hello chosen partition
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);
                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}'", operationId, progress.Result.Exception);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(5.0d)).ConfigureAwait(false);
        }
    }
```

<span data-ttu-id="8382e-154">esempio Hello riportato di seguito viene illustrato come toouse hello PartitionSelector toochoose una partizione casuale di un servizio specificato:</span><span class="sxs-lookup"><span data-stu-id="8382e-154">hello sample below shows how toouse hello PartitionSelector toochoose a random partition of a specified service:</span></span>

```csharp
    static async Task PerformDataLossUseSelectorSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/SampleService ");

        // Use a PartitionSelector that will have hello Fault Injection and Analysis Service choose a random partition of “targetServiceName”
        PartitionSelector partitionSelector = PartitionSelector.RandomOf(targetServiceName);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }
            catch (Exception e)
            {
                Console.WriteLine("Unexpected exception '{0}'", e);
                throw;
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                Console.WriteLine("Printing progress.Result:");
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);

                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}', SelectedPartition {2}", operationId, progress.Result.Exception, progress.Result.SelectedPartition);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }
    }
```

## <a name="history-and-truncation"></a><span data-ttu-id="8382e-155">Cronologia e troncamento</span><span class="sxs-lookup"><span data-stu-id="8382e-155">History and Truncation</span></span>
<span data-ttu-id="8382e-156">Dopo che un comando ha raggiunto uno stato terminale, relativi metadati rimarranno in hello attacco intrusivo nel codice di errore e Analysis Services per un certo periodo di tempo, prima che questa venga rimosso lo spazio toosave.</span><span class="sxs-lookup"><span data-stu-id="8382e-156">After a command has reached a terminal state, its metadata will remain in hello Fault Injection and Analysis Service for a certain time, before it will be removed toosave space.</span></span>  <span data-ttu-id="8382e-157">Se viene chiamato "GetProgress" utilizzando operationId hello di un comando, dopo che è stato rimosso, verrà restituito un FabricException con un codice di errore di KeyNotFound.</span><span class="sxs-lookup"><span data-stu-id="8382e-157">If “GetProgress” is called using hello operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span></span>

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
