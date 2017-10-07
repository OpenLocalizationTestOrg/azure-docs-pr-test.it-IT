---
title: gestione delle applicazioni Azure Service Fabric aaaAutomate | Documenti Microsoft
description: Distribuire, aggiornare, testare e rimuovere le applicazioni di Service Fabric tramite PowerShell.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: f03f4294-571d-4262-8a77-cc8b481b959d
ms.service: service-fabric
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/16/2017
ms.author: ryanwi
redirect_url: /azure/service-fabric/service-fabric-deploy-remove-applications
ms.openlocfilehash: a64a39dbee26be8ac15fee767a90fd06bfe4b896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-hello-application-lifecycle-using-powershell"></a>Automatizzare hello ciclo di vita delle applicazioni tramite PowerShell
Molti aspetti di hello [ciclo di vita dell'applicazione Service Fabric](service-fabric-application-lifecycle.md) possono essere automatizzate.  Questo articolo illustra come toouse PowerShell tooautomate comuni attività di distribuzione, l'aggiornamento, la rimozione e testing delle applicazioni Azure Service Fabric.  Sono disponibili anche API gestite e HTTP per la gestione delle app. Per altre informazioni, vedere la pagina sul [ciclo di vita delle app](service-fabric-application-lifecycle.md) .  

## <a name="prerequisites"></a>Prerequisiti
Prima di passare attività toohello nell'articolo hello, assicurarsi di:

* Acquisire familiarità con i concetti di Service Fabric hello descritti in [Panoramica tecnica di Service Fabric](service-fabric-technical-overview.md).
* [Installare il runtime di hello, SDK e strumenti](service-fabric-get-started.md), che viene installato anche hello **ServiceFabric** modulo di PowerShell.
* [Consentire l'esecuzione di script di PowerShell](service-fabric-get-started.md#enable-powershell-script-execution).
* Avviare un cluster locale.  Avviare una nuova finestra di PowerShell come amministratore, quindi eseguire lo script di installazione di cluster hello dalla cartella SDK hello:`& "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"`
* Prima di eseguire qualsiasi comando di PowerShell in questo articolo, prima di tutto connettersi toohello cluster di Service Fabric locale tramite [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps):`Connect-ServiceFabricCluster localhost:19000`
* Hello seguenti attività richiede una toodeploy pacchetto di applicazione v1 e v2 un pacchetto dell'applicazione per l'aggiornamento. Scaricare hello [ **WordCount** applicazione di esempio](http://aka.ms/servicefabricsamples) (all'interno di esempi di introduzione hello). Compilare e distribuire un'applicazione hello in Visual Studio (fare clic su **WordCount** in Esplora soluzioni e selezionare **pacchetto**). Pacchetto di v1 copia hello in `C:\ServiceFabricSamples\Services\WordCount\WordCount\pkg\Debug` troppo`C:\Temp\WordCount`. Copia `C:\Temp\WordCount` troppo`C:\Temp\WordCountV2`, creazione pacchetto di applicazione hello v2 per l'aggiornamento. Aprire `C:\Temp\WordCountV2\ApplicationManifest.xml` in un editor di testo. In hello **ApplicationManifest** elemento, modifica hello **ApplicationTypeVersion** troppo dell'attributo da "1.0.0" "2.0.0" numero di versione tooupdate hello app. Salvare file ApplicationManifest XML hello modificato.

## <a name="task-deploy-a-service-fabric-application"></a>Attività: Distribuire un'applicazione di Service Fabric
Dopo aver compilato e incluso nel pacchetto di applicazione hello (o scaricare il pacchetto di applicazione hello), è possibile distribuire un'applicazione hello in un cluster di Service Fabric locale. Distribuzione coinvolge il caricamento del pacchetto di applicazione hello, registrazione del tipo di applicazione hello e la creazione di istanza dell'applicazione hello. Utilizzare istruzioni hello in questa toodeploy sezione un nuovo cluster tooa dell'applicazione.

### <a name="step-1-upload-hello-application-package"></a>Passaggio 1: Caricare il pacchetto dell'applicazione hello
Caricamento toohello pacchetto di applicazione hello archivio immagini inserisce nei componenti di Service Fabric toointernal accessibile percorso.  pacchetto di applicazione Hello contiene hello manifesto dell'applicazione, i manifesti del servizio e il codice di configurazione necessarie e l'applicazione hello toocreate i pacchetti di dati e le istanze del servizio. Se si desidera localmente pacchetto dell'applicazione hello tooverify, utilizzare hello [Test ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet.  Hello [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) comando caricamenti hello pacchetto. ad esempio:

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCount\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

### <a name="step-2-register-hello-application-type"></a>Passaggio 2: Registrare il tipo di applicazione hello
Pacchetto di applicazione hello registrazione rende il tipo di applicazione hello e versione dichiarato nel manifesto dell'applicazione hello disponibile per l'uso. sistema Hello legge pacchetto hello caricato nel passaggio hello 1, verificare il pacchetto di hello (equivalente toorunning [Test ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) in locale), l'elaborazione di contenuto del pacchetto hello e copiare tooan pacchetto hello elaborato percorso di sistema interno.  Eseguire hello [registro ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCount
```
tutti i tipi di applicazione hello registrati nel cluster di hello, eseguire hello toosee [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Get-ServiceFabricApplicationType
```

### <a name="step-3-create-hello-application-instance"></a>Passaggio 3: Creare l'istanza dell'applicazione hello
È possibile creare istanze di un'applicazione utilizzando la versione di qualsiasi tipo di applicazione che è stato registrato correttamente tramite hello [New ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) comando. nome Hello di ogni applicazione è dichiarata in fase di distribuzione e deve iniziare con hello **fabric:** dello schema e di essere univoco per ogni istanza dell'applicazione. Hello nome tipo e la versione di tipo di applicazione vengono dichiarati in hello **ApplicationManifest.xml** file del pacchetto di applicazione hello. Se servizi predefiniti sono stati definiti nel manifesto dell'applicazione hello del tipo di applicazione di destinazione hello, quelli vengono creati in questo momento.

```powershell
New-ServiceFabricApplication fabric:/WordCount WordCount 1.0.0
```

Hello [Get ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) comando Elenca tutte le istanze di applicazione che sono state create, insieme al relativo stato generale. Hello [Get ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) comando Elenca tutte le istanze del servizio hello che sono state create all'interno di un'istanza dell'applicazione specificato. Vengono elencati anche gli eventuali servizi predefiniti.

```powershell
Get-ServiceFabricApplication

Get-ServiceFabricApplication | Get-ServiceFabricService
```

## <a name="task-upgrade-a-service-fabric-application"></a>Attività: Aggiornare un'applicazione di Service Fabric
È possibile aggiornare un'applicazione di Service Fabric distribuita in precedenza con un pacchetto dell'applicazione aggiornato. Questa attività consente di aggiornare un'applicazione WordCount hello che è stata distribuita in "attività: distribuire un'applicazione di Service Fabric." Per altre informazioni, vedere [Aggiornamento di un'applicazione di Service Fabric](service-fabric-application-upgrade.md) .

tookeep le cose semplici per questo esempio, un solo numero di versione dell'applicazione hello è stata aggiornata nel pacchetto di applicazione hello WordCountV2 creato nei prerequisiti hello. Uno scenario più realistico implica l'aggiornamento del file di codice, configurazione o dati del servizio e la ricompilazione e assemblaggio applicazione hello con numeri di versione aggiornati.  

### <a name="step-1-upload-hello-updated-application-package"></a>Passaggio 1: Caricare il pacchetto di applicazione aggiornata hello
Hello WordCount v1 applicazione è pronta toobe aggiornato. Se si apre una finestra di PowerShell come amministratore e digitare [ **Get ServiceFabricApplication**](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), vedrai che la versione 1.0.0 del tipo di applicazione WordCount hello viene distribuita.  

Ora hello copia aggiornata archivio applicazioni pacchetto toohello Service Fabric immagine (in cui i pacchetti di applicazione hello sono archiviati dall'infrastruttura di servizio). parametro Hello **ApplicationPackagePathInImageStore** informa Service Fabric in cui è possibile trovare il pacchetto di applicazione hello. Hello comando copie hello pacchetto di applicazione troppo seguente**WordCountV2** nell'archivio immagini hello:  

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCountV2\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCountV2

```
### <a name="step-2-register-hello-updated-application-type"></a>Passaggio 2: Registrare hello aggiornato il tipo di applicazione
passaggio successivo Hello è tooregister hello nuova versione dell'applicazione hello con Service Fabric, che può essere eseguita tramite hello [registro ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCountV2
```

### <a name="step-3-start-hello-upgrade"></a>Passaggio 3: Avviare l'aggiornamento di hello
Vari parametri di aggiornamento, timeout e criteri di integrità possono essere applicati tooapplication aggiornamenti. Leggere hello [parametri di aggiornamento dell'applicazione](service-fabric-application-upgrade-parameters.md) e [processo di aggiornamento](service-fabric-application-upgrade.md) toolearn più documenti. Tutti i servizi e le istanze devono essere *integro* dopo l'aggiornamento di hello.  Set hello **HealthCheckStableDuration** too60 secondi (in modo che i servizi di hello siano integri per dominio di aggiornamento successivo almeno 20 secondi prima di avviare l'aggiornamento di hello toohello).  Anche set hello **UpgradeDomainTimeout** too1200 secondi e hello **UpgradeTimeout** too3000 secondi. Infine, impostare hello **UpgradeFailureAction** troppo**rollback**, che le richieste di cui eseguire il rollback di Service Fabric hello toohello versione precedente dell'applicazione se si verificano errori durante l'aggiornamento.

È ora possibile avviare l'aggiornamento dell'applicazione hello utilizzando hello [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet:

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/WordCount -ApplicationTypeVersion 2.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000  -FailureAction Rollback -Monitored
```

Si noti che il nome dell'applicazione hello è hello stesso come hello distribuito in precedenza nome applicazione versione 1.0.0 (fabric: / WordCount). Service Fabric utilizza tooidentify questo nome è aggiornamento l'applicazione. Se si imposta hello toobe di timeout troppo breve, un messaggio di errore di timeout che stati hello problema potrebbero verificarsi. Fare riferimento troppo[risolvere gli aggiornamenti dell'applicazione](service-fabric-application-upgrade-troubleshooting.md), o aumentare il timeout di hello.

### <a name="step-4-check-upgrade-progress"></a>Passaggio 4: Verificare lo stato dell'aggiornamento
È possibile monitorare lo stato dell'aggiornamento dell'applicazione utilizzando [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md), oppure utilizzando hello [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet:

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/WordCount
```

In pochi minuti, hello [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) indica che sono stati aggiornati tutti i domini di aggiornamento (completato).

## <a name="task-test-a-service-fabric-application"></a>Attività: Testare un'applicazione di Service Fabric
servizi di alta qualità toowrite, gli sviluppatori devono toobe tooinduce in grado di infrastruttura inaffidabili errori tootest hello la stabilità dei servizi. Service Fabric offre agli sviluppatori di azioni di errore tooinduce possibilità hello e testare i servizi in presenza di hello di errori tramite hello chaos e failover scenari di test.  Leggere [toohello introduzione errore Analysis Service](service-fabric-testability-overview.md) per ulteriori informazioni.

### <a name="step-1-run-hello-chaos-test-scenario"></a>Passaggio 1: Eseguire uno scenario di test chaos hello
scenario di test chaos Hello genera errori nel cluster di Service Fabric intera hello. scenario di Hello comprime gli errori rilevati in genere in mesi o anni tooa alcune ore. combinazione di Hello di interfoliazione errori con una frequenza elevata di errori consente di trovare casi estremi che potrebbero altrimenti non essere rilevati. Hello seguente esempio viene eseguito uno scenario di test chaos hello per 60 minuti.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```

### <a name="step-2-run-hello-failover-test-scenario"></a>Passaggio 2: Eseguire uno scenario di test di failover hello
failover Hello una partizione di servizio specifico anziché l'intero cluster hello destinazioni di uno scenario di test e altri servizi lascia interessato. scenario Hello iterazione di una sequenza di errori simulati in convalida del servizio durante l'esecuzione della regola business. Un errore nella convalida del servizio indica un problema necessita di ulteriore analisi. test failover Hello provoca l'errore solo una alla volta, come toohello anziché chaos uno scenario di test, che può provocare errori più. Hello esempio seguente viene eseguito il test failover hello per 60 minuti rispetto dell'infrastruttura di hello: WordCount/servizio WordCountService.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/WordCount/WordCountService"

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindUniformInt64 -PartitionKey 1
```

## <a name="task-remove-a-service-fabric-application"></a>Attività: Rimuovere un'applicazione di Service Fabric
È possibile eliminare un'istanza di un'applicazione distribuita, rimuovere il tipo di applicazione hello provisioning dal cluster hello e rimuovere il pacchetto di applicazione hello da hello ImageStore.

### <a name="step-1-remove-an-application-instance"></a>Passaggio 1: Rimuovere un'istanza dell'applicazione
Quando un'istanza di applicazione non è più necessario, è possibile rimuoverlo in modo permanente tramite hello [Remove ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet. Questa operazione rimuove automaticamente anche tutti i servizi appartenenti toohello applicazione, in modo permanente la rimozione di tutti gli stati di servizio. Tale operazione non può essere annullata e lo stato dell'applicazione non può essere recuperato.

```powershell
Remove-ServiceFabricApplication fabric:/WordCount
```

### <a name="step-2-unregister-hello-application-type"></a>Passaggio 2: Annullare la registrazione del tipo di applicazione hello
Quando non è più necessario una particolare versione di un tipo di applicazione, annullare la registrazione tramite hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet. Annullamento della registrazione tipi inutilizzati versioni spazio di archiviazione utilizzato dal pacchetto di applicazione hello in archivio immagini hello. È possibile annullare la registrazione di un tipo di applicazione solo se non sono state create istanze di applicazioni basate su di esso o non vi sono aggiornamenti di applicazioni in sospeso che vi fanno riferimento.

```powershell
Unregister-ServiceFabricApplicationType WordCount 1.0.0
```

### <a name="step-3-remove-hello-application-package"></a>Passaggio 3: Rimuovere il pacchetto di applicazione hello
Una volta annullata la registrazione, il tipo di applicazione hello pacchetto dell'applicazione hello può essere rimosse dall'archivio immagini hello con hello [Remove ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.

```powershell
Remove-ServiceFabricApplicationPackage -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

## <a name="next-steps"></a>Passaggi successivi
[Ciclo di vita dell'applicazione Service Fabric](service-fabric-application-lifecycle.md)

[Distribuire un'applicazione](service-fabric-deploy-remove-applications.md)

[Aggiornamento dell'applicazione](service-fabric-application-upgrade.md)

[Cmdlet di Service Fabric di Azure](/powershell/azure/overview?view=azureservicefabricps)

