---
title: aaaDebug dell'applicazione in Visual Studio | Documenti Microsoft
description: "Migliorare hello affidabilità e prestazioni dei servizi, sviluppo e il debug in Visual Studio in un cluster di sviluppo locale."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: 8d08689e82195d09f57b462631ad04fd237bc4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a>Debug dell'applicazione di Service Fabric mediante Visual Studio
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a>Eseguire il debug di un'applicazione di Service Fabric
Per risparmiare tempo e denaro, è possibile distribuire l'applicazione di Service Fabric ed eseguirne il debug in un cluster di sviluppo locale. Visual Studio 2017 o Visual Studio 2015 è possibile distribuire cluster locale di hello applicazione toohello e si connettono automaticamente le istanze di hello debugger tooall dell'applicazione.

1. Avviare un cluster di sviluppo locale seguendo i passaggi di hello in [impostazione dell'ambiente di sviluppo di Service Fabric](service-fabric-get-started.md).
2. Premere **F5** oppure fare clic su **Debug** > **Avvia debug**.
   
    ![Avviare il debug di un'applicazione][startdebugging]
3. Impostare i punti di interruzione nel codice ed esaminare l'applicazione hello tramite i comandi in hello **Debug** menu.
   
   > [!NOTE]
   > Visual Studio collega tooall istanze dell'applicazione. Mentre il codice viene eseguito un'istruzione alla volta, i punti di interruzione possono essere raggiunti da più processi, dando luogo a sessioni simultanee. Provare a disabilitare i punti di interruzione hello dopo che è raggiunto apportando ogni punto di interruzione condizionale sull'ID di thread hello o usando gli eventi di diagnostica.
   > 
   > 
4. Hello **gli eventi di diagnostica** finestra verrà aperta automaticamente in modo da visualizzare gli eventi di diagnostica in tempo reale.
   
    ![Visualizzare gli eventi diagnostici in tempo reale][diagnosticevents]
5. È inoltre possibile aprire hello **gli eventi di diagnostica** finestra in Cloud Explorer.  In **Service Fabric** fare clic con il pulsante destro del mouse e scegliere **Visualizza tracce streaming**.
   
    ![Finestra di eventi di diagnostica hello aperto][viewdiagnosticevents]
   
    Se si desidera toofilter il servizio specifico di tracce tooa o l'applicazione, semplicemente abilitando le tracce di streaming su tale applicazione o un servizio specifico.
6. eventi di diagnostica Hello possono essere visualizzati in hello generato automaticamente **ServiceEventSource.cs** file e vengono chiamati dal codice dell'applicazione.
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. Hello **gli eventi di diagnostica** finestra supporta il filtro, la sospensione e controllando gli eventi in tempo reale.  filtro di Hello è una ricerca semplice stringa di messaggio di evento hello, incluso il relativo contenuto.
   
    ![Filtrare, sospendere e riprendere o esaminare eventi in tempo reale][diagnosticeventsactions]
8. Il debug dei servizi è come il debug di qualsiasi altra applicazione. In genere i punti di interruzione vengono impostati tramite Visual Studio per semplificare il debug. Anche se le raccolte Reliable Collections vengono replicate in più nodi, implementano comunque IEnumerable. Ciò significa che è possibile utilizzare hello visualizzazione dei risultati in Visual Studio durante il debug toosee è memorizzato all'interno. È sufficiente impostare un punto di interruzione in qualsiasi posizione all'interno del codice.
   
    ![Avviare il debug di un'applicazione][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a>Eseguire il debug di un'applicazione remota di Service Fabric
Se le applicazioni di Service Fabric sono in esecuzione in un cluster di Service Fabric in Azure, si è in grado di eseguire il debug tooremotely questi, direttamente da Visual Studio.

> [!NOTE]
> funzionalità di Hello richiede [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) e [Azure SDK per .NET 2.9](https://azure.microsoft.com/downloads/).    
> 
> 

<!-- -->
> [!WARNING]
> Debug remoto è destinato agli scenari di sviluppo e test e non toobe utilizzato negli ambienti di produzione a causa dell'impatto hello in hello applicazioni in esecuzione.
> 
> 

1. Passare il cluster tooyour in **Cloud Explorer**destro del mouse e scegliere **attivare il debug**
   
    ![Abilitare il debug remoto][enableremotedebugging]
   
    Ciò consente di avviare il processo di hello di abilitazione hello estensione nei nodi del cluster del debug remoto, nonché le configurazioni di rete necessarie.
2. Nodo del cluster rapida hello in **Cloud Explorer**e scegliere **collega Debugger**
   
    ![Collega debugger][attachdebugger]
3. In hello **allegare tooprocess** finestra di dialogo, scegliere il processo di hello toodebug desiderato e fare clic su **Connetti**
   
    ![Scegliere il processo][chooseprocess]
   
    nome Hello del processo di hello desiderate tooattach a, uguale a hello nome del nome di assembly del progetto di servizio.
   
    debugger Hello collegherà tooall nodi in esecuzione il processo di hello.
   
   * In caso di hello in cui si esegue il debug di un servizio senza stato, tutte le istanze del servizio hello in tutti i nodi fanno parte della sessione di debug hello.
   * Se si esegue il debug di un servizio con stato, solo hello replica primaria di ogni partizione sarà attiva e pertanto rilevata dal debugger hello. Se la replica primaria hello viene spostata durante una sessione di debug di hello, l'elaborazione di hello di tale replica sarà ancora parte della sessione di debug hello.
   * Le partizioni rilevanti ordine tooonly catch o istanze di un determinato servizio, è possibile utilizzare i punti di interruzione condizionali tooonly interruzione una partizione specifica o istanza.
     
     ![Punto di interruzione condizionale][conditionalbreakpoint]
     
     > [!NOTE]
     > Attualmente non è supportato il debug di un cluster di Service Fabric con più istanze di hello nome eseguibile del servizio stesso.
     > 
     > 
4. Dopo aver completato il debug dell'applicazione, è possibile disabilitare l'estensione di debug remoto hello facendo clic con il cluster hello in **Cloud Explorer** e scegliere **disabilitare il debug**
   
    ![Disabilitare il debug remoto][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a>Streaming delle tracce da un nodo del cluster remoto
Inoltre in grado di toostream tracce sono direttamente da un tooVisual nodo cluster remoto Studio. Questa funzionalità permette di eventi di traccia ETW toostream, generati in un nodo di cluster di Service Fabric.

> [!NOTE]
> La funzionalità richiede [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) e [Azure SDK per .NET 2.9](https://azure.microsoft.com/downloads/).
> Questa funzionalità supporta solo i cluster in esecuzione in Azure.
> 
> 

<!-- -->
> [!WARNING]
> Il flusso di tracce è progettato per scenari di sviluppo e test e non toobe utilizzato negli ambienti di produzione a causa dell'impatto hello in hello applicazioni in esecuzione.
> In uno scenario di produzione è consigliabile basarsi sugli eventi di inoltro usando Diagnostica di Azure.
> 
> 

1. Passare il cluster tooyour in **Cloud Explorer**destro del mouse e scegliere **abilitare lo Streaming di tracce**
   
    ![Abilitare le tracce di streaming remote][enablestreamingtraces]
   
    Ciò consente di avviare il processo di hello di abilitazione hello streaming estensione tracce nei nodi del cluster, nonché le configurazioni di rete necessarie.
2. Espandere hello **nodi** elemento **Cloud Explorer**, il nodo hello rapida toostream tracce da desiderato e scegliere **visualizzazione tracce di Streaming**
   
    ![Visualizzare le tracce di streaming remote][viewremotestreamingtraces]
   
    Ripetere il passaggio 2 per qualsiasi numero di nodi che si desidera toosee tracce da. Il flusso di ogni nodo verrà visualizzato in una finestra dedicata.
   
    Ora in grado di toosee hello tracce sono generate dall'infrastruttura di servizio e i servizi. Se si desidera toofilter hello eventi tooonly Mostra un'applicazione specifica, è sufficiente digitare hello nome dell'applicazione hello nel filtro hello.
   
    ![Visualizzazione delle tracce di streaming][viewingstreamingtraces]
3. Dopo aver eseguito le tracce di streaming dal cluster, è possibile disabilitare le tracce di flusso remote, facendo clic con il cluster hello in **Cloud Explorer** e scegliere **disabilitare tracce di Streaming**
   
    ![Disabilitare le tracce di streaming remote][disablestreamingtraces]

## <a name="next-steps"></a>Passaggi successivi
* [Testare un servizio di Service Fabric](service-fabric-testability-overview.md)
* [Gestione delle applicazioni di Service Fabric in Visual Studio](service-fabric-manage-application-in-visual-studio.md).

<!--Image references-->
[startdebugging]: ./media/service-fabric-debugging-your-application/startdebugging.png
[diagnosticevents]: ./media/service-fabric-debugging-your-application/diagnosticevents.png
[viewdiagnosticevents]: ./media/service-fabric-debugging-your-application/viewdiagnosticevents.png
[diagnosticeventsactions]: ./media/service-fabric-debugging-your-application/diagnosticeventsactions.png
[breakpoint]: ./media/service-fabric-debugging-your-application/breakpoint.png
[enableremotedebugging]: ./media/service-fabric-debugging-your-application/enableremotedebugging.png
[attachdebugger]: ./media/service-fabric-debugging-your-application/attachdebugger.png
[chooseprocess]: ./media/service-fabric-debugging-your-application/chooseprocess.png
[conditionalbreakpoint]: ./media/service-fabric-debugging-your-application/conditionalbreakpoint.png
[disableremotedebugging]: ./media/service-fabric-debugging-your-application/disableremotedebugging.png
[enablestreamingtraces]: ./media/service-fabric-debugging-your-application/enablestreamingtraces.png
[viewingstreamingtraces]: ./media/service-fabric-debugging-your-application/viewingstreamingtraces.png
[viewremotestreamingtraces]: ./media/service-fabric-debugging-your-application/viewremotestreamingtraces.png
[disablestreamingtraces]: ./media/service-fabric-debugging-your-application/disablestreamingtraces.png
