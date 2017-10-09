---
title: aggiornamento di App Fabric aaaService mediante PowerShell | Documenti Microsoft
description: In questo articolo vengono esaminati esperienza hello di distribuzione di un'applicazione di Service Fabric, modificare il codice hello e implementazione di un aggiornamento tramite PowerShell.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 9bc75748-96b0-49ca-8d8a-41fe08398f25
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: f31212264de45c3b257a0efafb75c10c279b989f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-using-powershell"></a>Aggiornamento di un'applicazione di Service Fabric mediante PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
> * [Visual Studio](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

Hello utilizzati più di frequente e approccio di aggiornamento consigliato è l'aggiornamento in sequenza hello monitorato.  Azure Service Fabric esegue monitoraggio hello di un'applicazione hello viene aggiornata in base a un set di criteri di integrità. Dopo aver aggiornato un dominio di aggiornamento (UD), Service Fabric valuta l'integrità dell'applicazione hello e procede toohello successivo dominio di aggiornamento o si verifica un errore di aggiornamento hello in base a criteri di integrità hello.

Un aggiornamento dell'applicazione monitorata può essere eseguito mediante hello gestito o le API native, PowerShell o REST. Per istruzioni su come eseguire un aggiornamento usando Visual Studio, vedere [Esercitazione sull'aggiornamento di un'applicazione di Service Fabric tramite Visual Studio](service-fabric-application-upgrade-tutorial.md).

Con Service Fabric monitorati aggiornamenti in sequenza, amministratore dell'applicazione hello possibile configurare i criteri di valutazione salute hello utilizzato Service Fabric toodetermine se un'applicazione hello è integra. Inoltre, messaggio per l'amministratore può configurare hello toobe di azione eseguita quando si verifica un errore di valutazione dell'integrità hello (ad esempio, eseguire il rollback automatico). In questa sezione vengono illustrati un aggiornamento per uno degli esempi SDK hello che utilizza PowerShell monitorato. Hello video Microsoft Virtual Academy seguente illustra anche un aggiornamento di app:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=OrHJH66yC_6406218965">
<img src="./media/service-fabric-application-upgrade-tutorial-powershell/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="step-1-build-and-deploy-hello-visual-objects-sample"></a>Passaggio 1: Creare e distribuire: esempio hello oggetti visivi
Compilare e pubblicare un'applicazione hello facendo clic sul progetto di applicazione hello **VisualObjectsApplication,** e selezionando hello **pubblica** comando.  Per altre informazioni, vedere [Esercitazione sull'aggiornamento di un'applicazione di Service Fabric tramite Visual Studio](service-fabric-application-upgrade-tutorial.md).  In alternativa, è possibile utilizzare PowerShell toodeploy l'applicazione.

> [!NOTE]
> Prima di tutti i comandi di Service Fabric hello possono essere usati in PowerShell, è necessario innanzitutto tooconnect toohello cluster utilizzando hello `Connect-ServiceFabricCluster` cmdlet. Analogamente, si presuppone che hello che cluster è già stato configurato nel computer locale. Vedere l'articolo hello in [impostazione dell'ambiente di sviluppo di Service Fabric](service-fabric-get-started.md).
> 
> 

Dopo aver compilato il progetto hello in Visual Studio, è possibile utilizzare il comando di PowerShell hello [copia ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) toohello pacchetto di applicazione hello toocopy ImageStore. Se si desidera localmente pacchetto dell'applicazione hello tooverify, utilizzare hello [Test ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet. passaggio successivo Hello è tooregister hello toohello Service Fabric runtime dell'applicazione utilizzando hello [registro ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) cmdlet. Hello passaggio finale è un'istanza di un'applicazione hello toostart utilizzando hello [New ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.  Questi tre passaggi sono analoghi toousing hello **Distribuisci** voce di menu in Visual Studio.

A questo punto, è possibile utilizzare [Service Fabric Explorer tooview cluster e hello applicazione hello](service-fabric-visualizing-your-cluster.md). applicazione Hello è un servizio web che è possibile spostarsi tooin Internet Explorer digitare [http://localhost:8081/visualobjects](http://localhost:8081/visualobjects) nella barra degli indirizzi hello.  Si noterà che alcuni oggetti visivi Mobile gli spostamenti nella schermata di hello.  Inoltre, è possibile utilizzare [Get ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) toocheck stato dell'applicazione hello.

## <a name="step-2-update-hello-visual-objects-sample"></a>Passaggio 2: Aggiornare: esempio hello oggetti visivi
È possibile notare che con la versione di hello che è stato distribuito nel passaggio 1, gli oggetti visivi hello non ruotare. Eseguire l'aggiornamento si tooone questa applicazione in cui gli oggetti visivi hello inoltre ruotare.

Selezionare il progetto VisualObjects.ActorService hello all'interno di hello VisualObjects soluzione e aprire il file StatefulVisualObjectActor.cs hello. All'interno del file, passare il metodo toohello `MoveObject`, impostare come commento `this.State.Move()`e rimuovere il commento `this.State.Move(true)`. Questa modifica consente di ruotare oggetti hello dopo l'aggiornamento di servizio hello.

È anche necessario hello tooupdate *ServiceManifest.xml* file (in PackageRoot) del progetto hello **VisualObjects.ActorService**. Hello aggiornamento *CodePackage* hello servizio versione too2.0 e hello righe corrispondenti hello *ServiceManifest.xml* file.
È possibile utilizzare Visual Studio hello *modifica file manifesto* opzione dopo fare clic su modifiche al file manifesto di hello soluzione toomake hello.

Dopo aver apportato modifiche di hello, manifesto hello dovrebbe essere simile hello seguente (parti evidenziate mostrano modifiche hello):

```xml
<ServiceManifestName="VisualObjects.ActorService" Version="2.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

<CodePackageName="Code" Version="2.0">
```

Ora hello *ApplicationManifest.xml* file (in hello **VisualObjects** progetto sottoposto a hello **VisualObjects** soluzione) viene aggiornato tooversion 2.0 di hello  **VisualObjects.ActorService** progetto. Inoltre, versione dell'applicazione hello è too2.0.0.0 aggiornata dalla 1.0.0.0. Hello *ApplicationManifest.xml* deve hello l'aspetto seguente frammento di codice:

```xml
<ApplicationManifestxmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="VisualObjects" ApplicationTypeVersion="2.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

 <ServiceManifestRefServiceManifestName="VisualObjects.ActorService" ServiceManifestVersion="2.0" />
```


A questo punto, compilare il progetto di hello selezionando solo hello **ActorService** progetto, quindi facendo clic e selezionare hello **compilare** opzione in Visual Studio. Se si seleziona **Ricompila tutto**, è necessario aggiornare le versioni di hello per tutti i progetti, poiché potrebbe aver modificato il codice hello. Successivamente, si hello pacchetto applicazione aggiornata facendo clic su ***VisualObjectsApplication***, selezionando hello Menu dell'infrastruttura del servizio e scegliere **pacchetto**. In questo modo viene creato un pacchetto dell'applicazione che può essere distribuito.  L'applicazione aggiornata è pronto toobe distribuito.

## <a name="step-3--decide-on-health-policies-and-upgrade-parameters"></a>Passaggio 3: Scegliere i criteri di integrità e i parametri di aggiornamento
Acquisire familiarità con hello [parametri di aggiornamento dell'applicazione](service-fabric-application-upgrade-parameters.md) hello e [processo di aggiornamento](service-fabric-application-upgrade.md) tooget una buona conoscenza di hello vari parametri, valori di timeout e il criterio di integrità applicato l'aggiornamento . Questa procedura dettagliata, criteri di valutazione di integrità servizio hello sono impostare il valore predefinito di toohello (e consigliabile) valori, il che significa che tutti i servizi e le istanze devono essere *integro* dopo l'aggiornamento di hello.  

Tuttavia, si aumenta hello *HealthCheckStableDuration* too60 secondi (in modo che i servizi di hello siano integri per almeno 20 secondi prima di avviare l'aggiornamento di hello toohello successivamente aggiornare il dominio).  Impostiamo anche hello *UpgradeDomainTimeout* toobe 1200 secondi e hello *UpgradeTimeout* toobe 3.000 secondi.

Infine, anche impostiamo hello *UpgradeFailureAction* toorollback. Questa opzione richiede la versione precedente di Service Fabric tooroll hello indietro applicazione toohello se vengono rilevati problemi durante l'aggiornamento di hello. Pertanto, quando si avvia l'aggiornamento di hello (nel passaggio 4), hello seguenti parametri vengono specificati:

FailureAction = Rollback

HealthCheckStableDurationSec = 60

UpgradeDomainTimeoutSec = 1200

UpgradeTimeout = 3000

## <a name="step-4-prepare-application-for-upgrade"></a>Passaggio 4: preparare l'applicazione per l'aggiornamento
Ora di compilazione dell'applicazione hello e pronto toobe aggiornato. Se si apre una finestra di PowerShell come amministratore e si digita [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), verrà indicato che è stato distribuito il tipo di applicazione 1.0.0.0 di **VisualObject**.  

Hello pacchetto dell'applicazione viene archiviato in seguito hello percorso relativo in cui non compressi hello Service Fabric SDK - *Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug*. In questa directory in cui è archiviato il pacchetto di applicazione hello, è necessario trovare una cartella "Package". Controllare tooensure timestamp hello è costituito da build più recente di hello (potrebbe essere necessario in modo appropriato anche i percorsi hello toomodify).

Ora si hello copia aggiornata toohello pacchetto di applicazione nell'archivio immagini dell'infrastruttura di servizio (in cui i pacchetti di applicazione hello sono archiviati dall'infrastruttura di servizio). parametro Hello *ApplicationPackagePathInImageStore* informa Service Fabric in cui è possibile trovare il pacchetto di applicazione hello. È stato creato l'applicazione hello aggiornato "VisualObjects\_V2" con hello (potrebbe essere necessario toomodify percorsi nuovamente in modo appropriato) di comando seguente.

```powershell
Copy-ServiceFabricApplicationPackage  -ApplicationPackagePath .\Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug\Package
-ImageStoreConnectionString fabric:ImageStore   -ApplicationPackagePathInImageStore "VisualObjects\_V2"
```

passaggio successivo Hello è tooregister dell'applicazione con Service Fabric, che può essere eseguita mediante hello [registro ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) comando:

```powershell
Register-ServiceFabricApplicationType -ApplicationPathInImageStore "VisualObjects\_V2"
```

Se hello comando precedente non riesce, è probabile che sia necessario ricompilare tutti i servizi. Come indicato nel passaggio 2, è possibile tooupdate anche la versione del servizio Web.

## <a name="step-5-start-hello-application-upgrade"></a>Passaggio 5: Avviare l'aggiornamento dell'applicazione hello
A questo punto, siamo tutti i set di un'applicazione hello toostart aggiornamento utilizzando hello [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) comando:

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/VisualObjects -ApplicationTypeVersion 2.0.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000   -FailureAction Rollback -Monitored
```


Hello nome dell'applicazione è hello stesso descritta in hello *ApplicationManifest.xml* file. Service Fabric utilizza tooidentify questo nome è aggiornamento l'applicazione. Se si imposta hello toobe di timeout troppo breve, è possibile riscontrare un messaggio di errore che stati hello problema. Riferimento toohello risoluzione dei problemi di sezione o aumentare il timeout di hello.

A questo punto, come hello viene eseguito l'aggiornamento dell'applicazione, è possibile monitorare l'utilizzo di Service Fabric Explorer, oppure utilizzando hello [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) comando di PowerShell: 

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/VisualObjects
```

In pochi minuti, lo stato di hello ottenuti utilizzando hello precedente comando di PowerShell, devono indicare che sono stati aggiornati tutti i domini di aggiornamento (completato). E si rileverà che gli oggetti visivi hello nella finestra del browser siano stati avviati rotazione!

È possibile provare a effettuare l'aggiornamento dalla versione 2 tooversion 3 o dalla versione 2 tooversion 1 come esercizio. Lo spostamento da versione 2 tooversion 1 viene considerato anche un aggiornamento. Provare a usare toomake di criteri di integrità e timeout manualmente familiarità con esse. Quando si distribuiscono cluster Azure tooan, hello set di parametri necessario toobe in modo appropriato. È buona tooset i timeout di hello conservativamente.

## <a name="next-steps"></a>Passaggi successivi
[Esercitazione sull'aggiornamento di un'applicazione di Service Fabric tramite Visual Studio](service-fabric-application-upgrade-tutorial.md) descrive la procedura di aggiornamento di un'applicazione con Visual Studio.

Controllare l'aggiornamento dell'applicazione tramite [Parametri di aggiornamento](service-fabric-application-upgrade-parameters.md).

Apportare aggiornamenti applicazione compatibile da learning come toouse [la serializzazione dei dati](service-fabric-application-upgrade-data-serialization.md).

Informazioni su come toouse funzionalità avanzate durante l'aggiornamento dell'applicazione riferendosi troppo[argomenti avanzati](service-fabric-application-upgrade-advanced.md).

Risolvere i problemi comuni negli aggiornamenti dell'applicazione riferendosi passaggi toohello [gli aggiornamenti dell'applicazione di risoluzione dei problemi](service-fabric-application-upgrade-troubleshooting.md).

