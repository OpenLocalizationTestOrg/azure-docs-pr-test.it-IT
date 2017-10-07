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
# <a name="how-tooinvoke-data-loss-on-services"></a>Come tooInvoke perdite di dati nei servizi
> [!WARNING]
> Questo documento viene descritto come perdita di dati toocause nei servizi e deve essere utilizzata con cautela.
> 
> 

## <a name="introduction"></a>Introduzione
È possibile richiamare la perdita di dati in una partizione del servizio Service Fabric chiamando StartPartitionDataLossAsync().  Questa api utilizza hello attacco intrusivo nel codice di errore e il servizio di analisi tooperform hello lavoro toocause dati perdita condizioni.

## <a name="using-hello-fault-injection-and-analysis-service"></a>Utilizzo di hello attacco intrusivo nel codice di errore e Analysis Services
Hello attacco intrusivo nel codice di errore e Analysis Services supporta attualmente hello seguenti API nel seguente grafico hello.  Hello nella parte destra del grafico hello sono hello cmdlet di PowerShell corrispondente.  Consultare la documentazione msdn toohello ogni API per ulteriori informazioni su ciascuna di esse.

| API C# | Cmdlet di PowerShell |
| --- | ---:|
| [StartPartitionDataLossAsync][dl] |[Start-ServiceFabricPartitionDataLoss][psdl] |
| [StartPartitionQuorumLossAsync][ql] |[Start-ServiceFabricPartitionQuorumLoss][psql] |
| [StartPartitionRestartAsync][rp] |[Start-ServiceFabricPartitionRestart][psrp] |

## <a name="conceptual-overview-of-running-a-command"></a>Panoramica concettuale dell'esecuzione di un comando
attacco intrusivo nel codice di errore e il servizio di analisi utilizzato un modello asincrono in cui viene avviata hello comando con un'API, cui tooas hello "Start" API in questo documento, quindi verifica hello lo stato di avanzamento di questo comando utilizza un'API "GetProgress" fino a quando non è stato raggiunto un terminale Hello stato, oppure finché non si annullarla.
toostart un comando, chiamata API "Start" hello per le API corrispondenti hello.  Questa API restituisce quando hello attacco intrusivo nel codice di errore e il servizio di analisi ha accettato la richiesta hello.  Tuttavia non indica a che punto si trova l'esecuzione del comando e neppure se è già stato avviato.  In ordine toocheck lo stato di avanzamento di un comando, chiamare l'API corrispondente toohello "Start" API in precedenza denominata "GetProgress" hello.  Hello "GetProgress" API restituirà un oggetto che indica lo stato corrente di hello del comando hello all'interno delle proprietà di stato.  Un comando viene eseguito all'infinito finché:

1. Viene completato correttamente.  Se si chiama "GetProgress" su di essa in questo caso, lo stato dell'oggetto di stato di avanzamento hello verrà completato.
2. Si verifica un errore irreversibile.  Se si chiama "GetProgress" su di essa in questo caso, lo stato dell'oggetto di stato di avanzamento hello verrà essere con errori
3. Annullarlo tramite hello [CancelTestCommandAsync] [ cancel] API, o [Stop ServiceFabricTestCommand] [ cancelps] cmdlet di PowerShell.  Se si chiama "GetProgress" su di essa in questo caso, hello stato di avanzamento dell'oggetto sarà annullato o ForceCancelled, a seconda di un toothat argomento API.  Vedere la documentazione di hello per [CancelTestCommandAsync] [ cancel] per altri dettagli.

## <a name="details-of-running-a-command"></a>Dettagli dell'esecuzione di un comando
In ordine toostart un comando, chiamare hello avviare API con argomenti hello previsto.  Tutte le API Start dispongono di un argomento Guid denominato operationId.  È necessario tenere traccia delle argomento operationId hello, poiché è utilizzato tootrack lo stato di avanzamento di questo comando.  Questo metodo deve essere passato in hello "GetProgress" API in corso tootrack ordine del comando hello.  ID operazione Hello deve essere univoci.

Dopo l'esito positivo della chiamata hello avviare API, hello GetProgress API deve essere chiamato in un ciclo fino a quando hello restituito lo stato di avanzamento proprietà State dell'oggetto viene completato.  È necessario provare di nuovo tutti i [FabricTransientException][fte] e OperationCanceledException.
Quando il comando hello ha raggiunto uno stato finale (Completed, Faulted o annullato), hello restituito proprietà Result dell'oggetto di stato di avanzamento saranno disponibili informazioni aggiuntive.  Se lo stato di hello viene completato, Result.SelectedPartition.PartitionId conterrà l'id di partizione hello che è stato selezionato.  Result.Exception sarà null.  Se lo stato di hello è Faulted, sarà necessario Result.Exception hello motivo hello attacco intrusivo nel codice di errore e il comando di hello Analysis Services con errori.  Result.SelectedPartition.PartitionId avrà id di partizione hello che è stato selezionato.  In alcuni casi, il comando hello potrebbe non proseguita fino toochoose una partizione.  In tal caso, hello PartitionId sarà pari a 0.  Se lo stato di hello viene annullato, Result.Exception sarà null.  Ad esempio hello case Faulted, Result.SelectedPartition.PartitionId avrà un id di partizione hello che è stato scelto, ma se il comando hello ha non viene eseguita fino toodo così, sarà 0.  Consultare inoltre toohello esempio riportato di seguito.

codice di esempio Hello riportato di seguito viene illustrato come toostart quindi controllare lo stato di avanzamento in una perdita di dati toocause comando su una partizione specifica.

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

esempio Hello riportato di seguito viene illustrato come toouse hello PartitionSelector toochoose una partizione casuale di un servizio specificato:

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

## <a name="history-and-truncation"></a>Cronologia e troncamento
Dopo che un comando ha raggiunto uno stato terminale, relativi metadati rimarranno in hello attacco intrusivo nel codice di errore e Analysis Services per un certo periodo di tempo, prima che questa venga rimosso lo spazio toosave.  Se viene chiamato "GetProgress" utilizzando operationId hello di un comando, dopo che è stato rimosso, verrà restituito un FabricException con un codice di errore di KeyNotFound.

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
