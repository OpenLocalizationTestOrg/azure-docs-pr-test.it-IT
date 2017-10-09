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
# <a name="report-and-check-service-health"></a>Creare report e verificare l'integrità dei servizi
Quando i servizi verificano problemi le interruzioni interventi di correzione tooand toorespond possibilità dipende dai possibilità toodetect hello problemi rapidamente. Se si segnala errori e problemi di gestione di integrità di Azure Service Fabric toohello dal codice del servizio, è possibile utilizzare gli strumenti di Service Fabric fornisce lo stato di integrità hello toocheck di monitoraggio dello stato standard.

Esistono tre modi che è possibile segnalare l'integrità dal servizio hello:

* Usare gli oggetti [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) o [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext).  
  È possibile utilizzare hello `Partition` e `CodePackageActivationContext` oggetti integrità hello tooreport di elementi che fanno parte del contesto corrente hello. Ad esempio, il codice che viene eseguito come parte di una replica può segnalare l'integrità solo su tale replica, hello partizione a cui appartiene e che fa parte di un'applicazione hello.
* Usare `FabricClient`.   
  È possibile utilizzare `FabricClient` integrità tooreport dal codice del servizio hello se non è cluster hello [sicura](service-fabric-cluster-security.md) o se il servizio di hello è in esecuzione con privilegi di amministratore. La maggior parte degli scenari reali non usa cluster non protetti oppure fornisce privilegi di amministratore. Con `FabricClient`, è possibile segnalare l'integrità per qualsiasi entità che fa parte del cluster di hello. In teoria, tuttavia, codice del servizio deve solo inviare i report correlati tooits sanitari.
* Utilizzare API REST di hello cluster hello, applicazione, applicazione distribuita, servizio, pacchetto del servizio, una partizione, replica o livelli dei nodi. Può trattarsi di integrità tooreport utilizzati all'interno di un contenitore.

Questo articolo viene illustrato un esempio che segnala l'integrità dal codice del servizio hello. esempio Hello Mostra anche come strumenti hello forniti dall'infrastruttura di servizio possono essere utilizzato toocheck hello lo stato di integrità. In questo articolo è previsto toobe integrità toohello di introduzione funzionalità di monitoraggio di Service Fabric. Per informazioni più dettagliate, è possibile leggere una serie di hello di articoli approfonditi su integrità che iniziano con collegamento hello alla fine di hello di questo articolo.

## <a name="prerequisites"></a>Prerequisiti
È necessario avere installato quanto segue hello:

* Visual Studio 2015 o Visual Studio 2017
* Service Fabric SDK

## <a name="toocreate-a-local-secure-dev-cluster"></a>toocreate un cluster locale sviluppo sicuro
* Aprire PowerShell con privilegi di amministratore ed eseguire hello seguenti comandi:

![I comandi che mostrano come toocreate un cluster di sviluppo sicuro](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a>toodeploy un'applicazione e controllare l'integrità
1. Aprire Visual Studio come amministratore.
2. Creare un progetto utilizzando hello **servizio con stato** modello.
   
    ![Creare un'applicazione di Service Fabric con un servizio con stato](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. Premere **F5** toorun un'applicazione hello in modalità di debug. un'applicazione Hello è cluster locale toohello distribuito.
4. Dopo l'applicazione hello è in esecuzione, fare clic sull'icona di gestione di Cluster locale hello nell'area di notifica hello e selezionare **gestire Cluster locale** da tooopen dal menu di scelta rapida hello Service Fabric Explorer.
   
    ![Apertura di Service Fabric Explorer dall'area di notifica](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. integrità applicazione Hello dovrebbero essere visualizzati come questa immagine. In questo momento, un'applicazione hello deve essere integra senza errori.
   
    ![Applicazione integra in Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. È inoltre possibile verificare l'integrità di hello tramite PowerShell. È possibile utilizzare ```Get-ServiceFabricApplicationHealth``` toocheck integrità di un'applicazione, si può usare ```Get-ServiceFabricServiceHealth``` toocheck integrità di un servizio. Hello rapporto di stato per hello stessa applicazione in PowerShell è in questa immagine.
   
    ![Applicazione integra in PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a>codice del servizio tooyour eventi tooadd integrità personalizzato
modelli di progetto di Service Fabric Hello in Visual Studio contengono codice di esempio. Hello passaggi seguenti viene illustrato come è possibile segnalare gli eventi di stato personalizzato dal codice del servizio. Tali report vengono visualizzate automaticamente in strumenti standard di hello per l'integrità del monitoraggio che fornisce Service Fabric, ad esempio Service Fabric Explorer e visualizzazione dell'integrità del portale di Azure PowerShell.

1. Riaprire l'applicazione hello creata in precedenza in Visual Studio o creare una nuova applicazione con hello **servizio con stato** modello di Visual Studio.
2. Aprire il file Stateful1.cs hello e trovare hello `myDictionary.TryGetValueAsync` chiamare hello `RunAsync` metodo. È possibile vedere che questo metodo restituisce un `result` che contiene hello valore corrente del contatore hello perché la chiave logica hello in questa applicazione è tookeep in esecuzione di un numero. Se si trattasse di un'applicazione reale e mancanza di hello del risultato rappresentato un errore, è opportuno tooflag quell'evento.
3. tooreport un evento di integrità quando assenza hello del risultato rappresenta un errore, aggiungere hello alla procedura seguente.
   
    a. Aggiungere hello `System.Fabric.Health` Stateful1.cs toohello di spazio dei nomi file.
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    b. Aggiungere hello seguente codice dopo hello `myDictionary.TryGetValueAsync` chiamare
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    Viene segnalata l'integrità di una replica, perché la segnalazione viene eseguita da un servizio con stato. Hello `HealthInformation` parametro archivia le informazioni hello integrità problema da segnalare.
   
    Se è stato creato un servizio senza stato, utilizzare hello seguente di codice
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. Se il servizio è in esecuzione con privilegi di amministratore o se hello cluster non è [sicura](service-fabric-cluster-security.md), è inoltre possibile utilizzare `FabricClient` integrità tooreport come illustrato nell'hello alla procedura seguente.  
   
    a. Creare hello `FabricClient` istanza dopo hello `var myDictionary` dichiarazione.
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    b. Aggiungere hello seguente codice dopo hello `myDictionary.TryGetValueAsync` chiamare.
   
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
5. Di seguito simulare l'errore e per visualizzare in strumenti di monitoraggio integrità hello. Errore di hello toosimulate, commento hello nella prima riga integrità hello reporting codice aggiunto in precedenza. Dopo la prima riga hello è come commento, codice hello avrà un aspetto simile hello di esempio seguente.
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   Questo codice viene generato ogni volta che il rapporto di stato hello `RunAsync` esegue. Dopo aver modificato hello, premere **F5** toorun un'applicazione hello.
6. Dopo l'applicazione hello è in esecuzione, aprire Service Fabric Explorer toocheck hello integrità hello applicazione. Questa volta, Service Fabric Explorer mostra che l'applicazione hello è integra. Ciò è dovuto errore hello che è stato segnalato dal codice hello che è stato aggiunto in precedenza.
   
    ![Applicazione non integra in Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. Se si seleziona la replica primaria hello nella visualizzazione ad albero di hello di Service Fabric Explorer, si noterà che **lo stato di integrità** indica un errore troppo. Service Fabric Explorer consente inoltre di visualizzare i report di integrità hello dettagli che sono stati aggiunti toohello `HealthInformation` parametro hello codice. È possibile visualizzare hello stesso report sull'integrità in PowerShell e hello portale di Azure.
   
    ![Integrità della replica in Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

Questo report rimane nel gestore integrità hello fino a quando non viene sostituita da un altro report o fino a quando la replica viene eliminata. Poiché non è stato impostato `TimeToLive` per questo rapporto di stato di hello `HealthInformation` oggetto report hello non scade mai.

È consigliabile che l'integrità deve essere segnalato al livello più granulare hello, ovvero in questo caso è hello replica. È anche possibile segnalare lo stato di integrità relativo all'oggetto `Partition`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

lo stato su tooreport `Application`, `DeployedApplication`, e `DeployedServicePackage`, utilizzare `CodePackageActivationContext`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione al monitoraggio dell'integrità di Service Fabric](service-fabric-health-introduction.md)
* [REST API for reporting service health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service) (API REST per segnalare l'integrità del servizio)
* [REST API for reporting application health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application) (API REST per segnalare l'integrità dell'applicazione)

