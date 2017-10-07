---
title: aaaDeploy ed eseguire l'aggiornamento di Azure microservizi localmente | Documenti Microsoft
description: Informazioni su come distribuire un esempio di applicazione esistente tooit tooset di un cluster di Service Fabric locale e quindi aggiornare l'applicazione.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 60a1f6a5-5478-46c0-80a8-18fe62da17a8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi;mikhegn
ms.openlocfilehash: e5f5adc9edb71433b2a7635e9d661ff92a4b18ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a>Introduzione alla distribuzione e all'aggiornamento di applicazioni nel cluster locale
Hello Azure Service Fabric SDK include un ambiente di sviluppo locale completo che è possibile utilizzare tooquickly iniziare con la distribuzione e la gestione delle applicazioni in un cluster locale. In questo articolo, creare un cluster locale, distribuire un tooit applicazione esistente e quindi aggiornare tale applicazione tooa nuova versione, tutte da Windows PowerShell.

> [!NOTE]
> Questo articolo presuppone che l' [ambiente di sviluppo sia già stato configurato](service-fabric-get-started.md).
> 
> 

## <a name="create-a-local-cluster"></a>Creare un cluster locale
Un cluster di Service Fabric rappresenta un set di risorse hardware in cui è possibile distribuire le applicazioni. In genere, un cluster è costituito da un punto qualsiasi da cinque toomany migliaia di computer. Tuttavia, hello Service Fabric SDK include una configurazione del cluster che è possibile eseguire su un singolo computer.

È importante toounderstand che hello cluster locale di Service Fabric non è un emulatore o simulatore. Viene eseguito hello stesso codice di piattaforma che si trova su un cluster con più computer. Hello unica differenza è che l'esecuzione di processi di piattaforma hello che sono in genere suddivisi in cinque macchine in un unico computer.

Hello SDK fornisce due modi tooset di un cluster locale: un Windows PowerShell script e hello gestione Cluster locale sistema cassetto app. In questa esercitazione, si usa uno script di PowerShell hello.

> [!NOTE]
> Se è già stato creato un cluster locale con la distribuzione di un'applicazione da Visual Studio, è possibile ignorare questa sezione.
> 
> 

1. Avviare una nuova finestra di PowerShell come amministratore.
2. Eseguire lo script di installazione di cluster hello dalla cartella SDK hello:
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    La configurazione del cluster richiede alcuni istanti. Al termine, l'output visualizzato sarà simile al seguente:
   
    ![Output installazione del cluster][cluster-setup-success]
   
    Si è ora pronto tootry distribuzione di un cluster di tooyour dell'applicazione.

## <a name="deploy-an-application"></a>Distribuire un'applicazione
Hello Service Fabric SDK include una vasta gamma di strumenti per la creazione di applicazioni per sviluppatori e ai Framework. Se è interessati a ottenere applicazioni toocreate in Visual Studio, vedere [creare la prima applicazione di Service Fabric in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).

In questa esercitazione, si utilizza un'applicazione di esempio esistente (denominata WordCount) in modo che sia possibile concentrarsi sugli aspetti di hello gestione della piattaforma hello: la distribuzione, monitoraggio e aggiornamento.

1. Avviare una nuova finestra di PowerShell come amministratore.
2. Importare il modulo di PowerShell di Service Fabric SDK hello.
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. Creare un'applicazione hello toostore di directory disponibili per download e distribuzione, ad esempio C:\ServiceFabric.
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. [Scaricare l'applicazione WordCount hello](http://aka.ms/servicefabric-wordcountapp) toohello percorso è stato creato.  Nota: browser Microsoft Edge hello Salva file hello con un *zip* estensione.  Modificare anche l'estensione del file hello*.sfpkg*.
5. Connettersi cluster locale toohello:
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. Creare una nuova applicazione utilizzando il comando di distribuzione del SDK di hello con un nome e un pacchetto di applicazione toohello percorso.
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    Se tutto va bene, dovrebbe essere hello seguente output:
   
    ![Distribuire un cluster locale toohello di applicazione][deploy-app-to-local-cluster]
7. un'applicazione hello toosee in azione, avviare il browser hello e passare troppo[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html). Dovrebbe essere visualizzato:
   
    ![Interfaccia utente dell'applicazione distribuita][deployed-app-ui]
   
    applicazione WordCount Hello è semplice. Include sul lato client JavaScript toogenerate casuale cinque caratteri "parole chiave", che vengono quindi inoltrate toohello applicazione tramite l'API Web ASP.NET. Un servizio con stato registra il numero di hello di parole conteggiati. Devono essere partizionati in base hello primo carattere della parola hello. È possibile trovare il codice sorgente hello per applicazione WordCount hello in hello [classico introduzione esempi](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).
   
    l'applicazione Hello che sono stati distribuiti contiene quattro partizioni. In modo da parole che iniziano con una lettera e G vengono archiviate nella partizione prima di hello, le parole che iniziano con H a N vengono archiviate nella seconda partizione hello e così via.

## <a name="view-application-details-and-status"></a>Visualizzare i dettagli e lo stato dell'applicazione
Ora che è stata distribuita un'applicazione hello, ecco alcuni dei dettagli dell'app hello in PowerShell.

1. Eseguire una query tutte le applicazioni distribuite in cluster hello:
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    Supponendo che è stato distribuito solo app WordCount hello, viene visualizzato qualcosa di simile a:
   
    ![Query per individuare tutte le applicazioni distribuite in PowerShell][ps-getsfapp]
2. Passare livello successivo toohello eseguendo una query su set hello dei servizi inclusi in un'applicazione WordCount hello.
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Elencare i servizi per un'applicazione hello in PowerShell][ps-getsfsvc]
   
    un'applicazione Hello è costituita da due servizi front-end web hello e servizio con stato hello che gestisce le parole hello.
3. Infine, esaminare l'elenco di hello delle partizioni per WordCountService:
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![Visualizzare le partizioni servizio hello in PowerShell][ps-getsfpartitions]
   
    set di comandi che è stata utilizzata, come tutti i comandi di PowerShell di Service Fabric Hello, sono disponibili per qualsiasi cluster che è possibile connettersi a, locale o remoto.
   
    Per più visual toointeract un modo con cluster hello, è possibile utilizzare lo strumento hello di Service Fabric Explorer basata sul web passando troppo[http://localhost:19080/Esplora](http://localhost:19080/Explorer) nel browser hello.
   
    ![Visualizzazione dei dettagli dell'applicazione in Service Fabric Explorer][sfx-service-overview]
   
   > [!NOTE]
   > toolearn informazioni su Service Fabric Explorer, vedere [visualizzazione cluster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
   > 
   > 

## <a name="upgrade-an-application"></a>Aggiornare un'applicazione
Service Fabric fornisce gli aggiornamenti senza tempo di inattività dal monitoraggio dell'integrità di hello di un'applicazione hello come viene eseguito il rollback cluster hello. Eseguire un aggiornamento dell'applicazione WordCount hello.

nuova versione di Hello di un'applicazione hello ora conta solo le parole che iniziano con una vocale. Come l'aggiornamento di hello implementa, vediamo due modifiche del comportamento dell'applicazione hello. In primo luogo, deve rallentare frequenza hello in corrispondenza del quale il conteggio di hello cresce, poiché viene contate minor numero di parole. In secondo luogo, poiché la prima partizione hello ha due vocali (ed E) e tutte le altre partizioni contengano solo uno, il conteggio deve infine avviare toooutpace hello altri.

1. [Download del pacchetto versione 2 WordCount hello](http://aka.ms/servicefabric-wordcountappv2) toohello stessa posizione in cui è stato scaricato il pacchetto di versione 1 hello.
2. Restituire tooyour finestra di PowerShell e utilizzare il comando di aggiornamento del SDK di hello tooregister hello nuova versione nel cluster hello. Quindi iniziare l'aggiornamento dell'infrastruttura di hello: / applicazione WordCount.
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    Dovrebbe essere hello output seguente nel PowerShell come hello aggiornamento inizia.
   
    ![Stato dell'aggiornamento in PowerShell][ps-appupgradeprogress]
3. Durante l'aggiornamento di hello procedere, può risultare più semplice toomonitor lo stato da Service Fabric Explorer. Avviare una finestra del browser e passare troppo[http://localhost:19080/Esplora](http://localhost:19080/Explorer). Espandere **applicazioni** albero hello hello sinistra, quindi scegliere **WordCount**e infine **fabric: / WordCount**. Nella scheda essentials hello, vedere lo stato di hello dell'aggiornamento hello durante il trasferimento tramite domini di aggiornamento del cluster hello.
   
    ![Stato dell'aggiornamento in Service Fabric Explorer][sfx-upgradeprogress]
   
    Come avviare l'aggiornamento di hello tramite ogni dominio, controlli di integrità sono eseguite tooensure che un'applicazione hello è funziona correttamente.
4. Se si esegue nuovamente hello in precedenza eseguire una query per il set di hello di servizi nell'infrastruttura hello: / applicazione WordCount, si noti che hello versione WordCountService modificato ma hello WordCountWebService versione non è stato eseguito:
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Query per individuare i servizi dell'applicazione dopo l'aggiornamento][ps-getsfsvc-postupgrade]
   
    Questo esempio illustra il modo in cui Service Fabric gestisce gli aggiornamenti dell'applicazione. Tocca solo hello set di servizi (o pacchetti di configurazione o codice all'interno di tali servizi) che sono stati modificati, che consente al processo di aggiornamento più veloce e affidabile hello.
5. Infine, restituire toohello il comportamento della nuova versione dell'applicazione hello di browser tooobserve hello. Come previsto, hello conteggio avanza più lenta e hello prima partizione termina con leggermente più del volume hello.
   
    ![Nuova versione hello visualizzazione di un'applicazione hello nel browser hello][deployed-app-ui-v2]

## <a name="cleaning-up"></a>+ Cleaning up
Prima di concludere, è importante tooremember che hello cluster locale è di tipo real. Le applicazioni continuano toorun in background hello fino alla rimozione.  A seconda della natura hello delle App, un'app in esecuzione può richiedere notevoli risorse del computer. Si dispone di vari opzioni toomanage e applicazioni cluster hello:

1. tooremove una singola applicazione e tutte di dati, eseguire hello comando seguente:
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    In alternativa, eliminare un'applicazione hello hello Service Fabric Explorer **azioni** menu o i menu di scelta rapida hello nella visualizzazione elenco a sinistra dell'applicazione di hello.
   
    ![Eliminare un'applicazione in Service Fabric Explorer][sfe-delete-application]
2. Dopo l'eliminazione di un'applicazione hello dal cluster hello, annullare la registrazione di versioni 1.0.0 e 2.0.0 del tipo di applicazione WordCount hello. L'eliminazione rimuove i pacchetti di applicazione hello, inclusi codice hello e la configurazione, dall'archivio di immagini del cluster hello.
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    In alternativa, in Service Fabric Explorer, scegliere **tipo annullamento del provisioning** per un'applicazione hello.
3. tooshut cluster hello ma Mantieni dati dell'applicazione hello e tracce, fare clic su **arrestare Cluster locale** nell'app di area di notifica di sistema hello.
4. cluster hello toodelete interamente, fare clic su **rimuovere Cluster locale** nell'app di area di notifica di sistema hello. Questa opzione comporterà un altro hello lenta distribuzione quando che si preme F5 in Visual Studio. Rimuovi cluster locale hello solo se non si prevede di toouse per un certo tempo oppure se è necessario tooreclaim risorse.

## <a name="one-node-and-five-node-cluster-mode"></a>Modalità cluster a un nodo e a cinque nodi
Quando si sviluppano applicazioni, ci si ritroverà spesso a eseguire rapide iterazioni di scrittura di codice, debug, modifica del codice e debug. toohelp ottimizzare questo processo, cluster locale di hello può essere eseguito in due modalità: uno o cinque nodi. Entrambe le modalità cluster presentano vantaggi. Modalità di cinque nodi cluster consente toowork con un cluster reale. È possibile testare gli scenari di failover e usare più istanze e repliche dei servizi. Modalità di cluster a un nodo è la distribuzione rapida toodo ottimizzato e la registrazione dei servizi, toohelp è convalidare rapidamente il codice mediante il runtime di Service Fabric hello.

Né la modalità cluster a un nodo, né quella a cinque è un emulatore o un simulatore. cluster di sviluppo locale Hello esecuzioni hello stesso codice di piattaforma che si trova su un cluster con più computer.

> [!WARNING]
> Quando si modifica la modalità di hello cluster, il cluster corrente hello viene rimosso dal sistema e viene creato un nuovo cluster. dati Hello archiviati in hello cluster viene eliminati quando si modifica la modalità del cluster.
> 
> 

toochange hello modalità tooone nodo cluster, selezionare **cambia modalità Cluster** in Gestione Cluster di Service Fabric locale hello.

![Cambiare la modalità cluster][switch-cluster-mode]

In alternativa, modificare la modalità di cluster hello con PowerShell:

1. Avviare una nuova finestra di PowerShell come amministratore.
2. Eseguire lo script di installazione di cluster hello dalla cartella SDK hello:
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    La configurazione del cluster richiede alcuni istanti. Al termine, l'output visualizzato sarà simile al seguente:
   
    ![Output installazione del cluster][cluster-setup-success-1-node]

## <a name="next-steps"></a>Passaggi successivi
* Dopo aver distribuito e aggiornato alcune applicazioni precompilate, è possibile [provare a creare un'applicazione personalizzata in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).
* Tutte le azioni eseguite nel cluster locale di hello in questo articolo hello possono essere eseguite su un [cluster Azure](service-fabric-cluster-creation-via-portal.md) anche.
* aggiornamento di Hello effettuate in questo articolo è stato base. Vedere hello [documentazione relativa all'aggiornamento](service-fabric-application-upgrade.md) toolearn ulteriori informazioni sulla hello potenza e flessibilità di aggiornamento di Service Fabric.

<!-- Images -->

[cluster-setup-success]: ./media/service-fabric-get-started-with-a-local-cluster/LocalClusterSetup.png
[extracted-app-package]: ./media/service-fabric-get-started-with-a-local-cluster/ExtractedAppPackage.png
[deploy-app-to-local-cluster]: ./media/service-fabric-get-started-with-a-local-cluster/DeployAppToLocalCluster.png
[deployed-app-ui]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-v1.png
[deployed-app-ui-v2]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-PostUpgrade.png
[sfx-app-instance]: ./media/service-fabric-get-started-with-a-local-cluster/SfxAppInstance.png
[sfx-two-app-instances-different-partitions]: ./media/service-fabric-get-started-with-a-local-cluster/SfxTwoAppInstances-DifferentPartitionCount.png
[ps-getsfapp]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFApp.png
[ps-getsfsvc]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc.png
[ps-getsfpartitions]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFPartitions.png
[ps-appupgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/PS-AppUpgradeProgress.png
[ps-getsfsvc-postupgrade]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc-PostUpgrade.png
[sfx-upgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/SfxUpgradeOverview.png
[sfx-service-overview]: ./media/service-fabric-get-started-with-a-local-cluster/sfx-service-overview.png
[sfe-delete-application]: ./media/service-fabric-get-started-with-a-local-cluster/sfe-delete-application.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[switch-cluster-mode]: ./media/service-fabric-get-started-with-a-local-cluster/switch-cluster-mode.png
