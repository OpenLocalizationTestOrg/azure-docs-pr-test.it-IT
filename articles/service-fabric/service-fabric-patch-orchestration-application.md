---
title: applicazione di Service Fabric patch orchestrazione aaaAzure | Documenti Microsoft
description: Applicazione tooautomate operativo l'applicazione di sistema in un cluster di Service Fabric patch.
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a>Sistema operativo di Windows hello del cluster di Service Fabric patch

un'applicazione Hello patch orchestrazione è un'applicazione Azure Service Fabric che consente di automatizzare l'applicazione di patch in un cluster di Service Fabric in Azure senza tempi di inattività del sistema operativo.

app di Hello patch orchestrazione fornisce seguente hello:

- **Installazione automatica dell'aggiornamento del sistema operativo**. Gli aggiornamenti del sistema operativo vengono scaricati e installati automaticamente. I nodi del cluster vengono riavviati in base alle esigenze senza tempi di inattività del cluster.

- **Integrazione dell'integrità e l'applicazione di patch compatibile con il cluster**. Durante l'applicazione degli aggiornamenti, hello patch orchestrazione app esegue il monitoraggio di integrità hello hello dei nodi del cluster. I nodi del cluster sono aggiornati un nodo alla volta o un dominio di aggiornamento alla volta. Se integrità hello del cluster di hello smette di funzionare a causa di processo di gestione delle patch toohello, l'applicazione di patch è arrestato tooprevent aggravare il problema di hello.

## <a name="internal-details-of-hello-app"></a>Dettagli interni dell'applicazione hello

app di orchestrazione patch Hello è costituito da hello sottocomponenti seguenti:

- **Coordinator Service**: il servizio con stato è responsabile per:
    - Coordinare il processo di aggiornamento di Windows hello su intero cluster hello.
    - Archiviazione del risultato hello delle operazioni completate di Windows Update.
- **Node Agent Service**: è un servizio senza stato che viene eseguito in tutti i nodi di cluster di Service Fabric. servizio Hello è responsabile per:
    - Avvio automatico hello NTService agente nodo.
    - Monitoraggio hello NTService agente nodo.
- **Node agent NTService**: questo servizio di Windows NT viene eseguito con un privilegio di livello superiore (SYSTEM). Al contrario, hello servizio agente del nodo e il servizio coordinatore hello eseguire in un privilegio di livello inferiore (servizio di rete). servizio di Hello è responsabile dell'esecuzione hello seguendo i processi di Windows Update in tutti i nodi del cluster di hello:
    - La disabilitazione di aggiornamento automatico di Windows nel nodo hello.
    - Download e installazione di Windows Update in base a utente hello di criteri toohello ha fornito.
    - Il riavvio post macchina hello installazione Windows Update.
    - Il caricamento dei risultati di hello di toohello gli aggiornamenti di Windows il servizio coordinatore.
    - Generazione di report sull'integrità in caso di un'operazione non riuscita dopo l'esaurimento di tutti i tentativi.

> [!NOTE]
> Hello patch orchestrazione app utilizza hello Service Fabric ripristinare toodisable servizio di gestione del sistema o abilitare nodo hello ed eseguire controlli di integrità. attività di correzione Hello creata da hello patch orchestrazione app tracce hello lo stato di avanzamento di Windows Update per ogni nodo.

## <a name="prerequisites"></a>Prerequisiti

### <a name="minimum-supported-service-fabric-runtime-version"></a>Versione minima di runtime di Service Fabric supportata

#### <a name="azure-clusters"></a>Cluster di Azure
Hello patch orchestrazione app deve essere eseguito nel cluster di Azure con versione 5.5 versione runtime di Service Fabric o versione successiva.

#### <a name="standalone-on-premises-clusters"></a>Cluster locali autonomi
Hello patch orchestrazione app deve essere eseguito nel cluster autonomo con versione 5.6 versione runtime di Service Fabric o versione successiva.

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a>Abilitare il servizio di gestione ripristino hello (se non è in esecuzione già)

app di orchestrazione patch Hello richiede hello repair manager system service toobe abilitata sul cluster hello.

#### <a name="azure-clusters"></a>Cluster di Azure

I cluster di Azure nel livello di durabilità argento hello dispongono hello di ripristinare il servizio di gestione abilitato per impostazione predefinita. Cluster di Azure nel livello di durabilità gold hello potrebbe oppure potrebbe non disporre di servizio di gestione ripristino hello abilitato, a seconda della creazione di tali cluster. Cluster di Azure nel livello di durabilità "Bronze" hello, per impostazione predefinita, non è necessario hello ripristinare il servizio di gestione abilitato. Se il servizio di hello è già abilitato, è possibile visualizzarlo in esecuzione nella sezione Servizi di sistema hello in hello Service Fabric Explorer.

##### <a name="azure-portal"></a>Portale di Azure
È possibile abilitare Gestione ripristino dal portale di Azure in fase di hello di configurazione del cluster. Selezionare `Include Repair Manager` opzione `Add on features` in fase di hello della configurazione del Cluster.
![Immagine dell'attivazione del servizio di gestione della riparazione dal portale di Azure](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)

##### <a name="azure-resource-manager-template"></a>Modello di Azure Resource Manager
In alternativa è possibile utilizzare hello [modello di Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello manager di riparazione sui cluster di Service Fabric nuove ed esistenti. Ottiene il modello di hello per cluster hello che si desidera toodeploy. È possibile utilizzare i modelli di esempio hello o creare un modello di gestione risorse personalizzato. 

tooenable hello riparazione gestore servizio tramite [modello di Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):

1. Verificare innanzitutto che hello `apiversion` è troppo`2017-07-01-preview` per hello `Microsoft.ServiceFabric/clusters` risorsa, come illustrato nel seguente frammento di codice hello. Se è diverso, quindi è necessario hello tooupdate `apiVersion` toohello valore `2017-07-01-preview`:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. Ora abilitare il servizio di gestione ripristino hello aggiungendo segue hello `addonFeatures` sezione dopo hello `fabricSettings` sezione:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. Dopo aver aggiornato il modello di cluster con queste modifiche, applicarli e consentire l'aggiornamento di hello di fine. È ora possibile visualizzare hello manager sistema riparazione in esecuzione nel cluster. Viene chiamato `fabric:/System/RepairManagerService` nella sezione Servizi di sistema hello in hello Service Fabric Explorer. 

### <a name="standalone-on-premises-clusters"></a>Cluster locali autonomi

È possibile utilizzare hello [le impostazioni di configurazione per il cluster di Windows autonoma](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello manager di riparazione nel cluster di Service Fabric nuove ed esistenti.

servizio di gestione ripristino hello tooenable:

1. Verificare innanzitutto che hello `apiversion` in [configurazioni cluster generale](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) è troppo`04-2017` o versione successiva:

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. Ora abilitare il servizio di gestione ripristino aggiungendo segue hello `addonFeaturres` sezione dopo hello `fabricSettings` sezione come illustrato di seguito:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. Aggiornare il manifesto del cluster con le modifiche, utilizzando manifesto del cluster aggiornato hello [creare un nuovo cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) o [configurazione del cluster aggiornamento hello](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration). Una volta cluster hello è in esecuzione con manifesto del cluster aggiornato, è ora possibile visualizzare hello manager sistema riparazione in esecuzione nel cluster, che viene chiamato `fabric:/System/RepairManagerService`, in Esplora Service Fabric hello sezione servizi del sistema.

### <a name="disable-automatic-windows-update-on-all-nodes"></a>Disabilitare la connessione automatica a Windows Update su tutti i nodi

Aggiornamenti automatici di Windows potrebbero causare perdita tooavailability perché è possono riavviare più nodi del cluster in hello stesso tempo. app di orchestrazione patch Hello, per impostazione predefinita, i tentativi toodisable hello automatica di Windows Update in ogni nodo del cluster. Tuttavia, se le impostazioni di hello sono gestite da un amministratore o criteri di gruppo, è consigliabile hello impostazione criteri troppo "notifica prima del Download" in modo esplicito di Windows Update.

### <a name="optional-enable-azure-diagnostics"></a>Facoltativo: abilitare Diagnostica di Azure

Per i cluster che eseguono la versione di runtime di Service Fabric `5.6.220.9494` e livelli successivi, verranno raccolti i log dell'app di orchestrazione come parte dei log di Service Fabric.
È possibile ignorare questo passaggio se il cluster è in esecuzione nella versione di runtime di Service Fabric `5.6.220.9494` e nelle versioni successive.

Per i cluster che eseguono la versione di runtime Service Fabric minore `5.6.220.9494`, i registri per app di orchestrazione patch hello vengono raccolti in locale in ognuno dei nodi del cluster hello.
È consigliabile configurare il log di diagnostica Azure tooupload da tutti i nodi tooa centrale.

Per altre informazioni su come abilitare Diagnostica di Azure, vedere [Raccogliere log con Diagnostica di Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).

Per app di orchestrazione patch hello di registri generati in hello seguente ID di provider predefinito:

- e39b723c-590c-4090-abb0-11e3e6616346
- fc0028ff-bfdc-499f-80dc-ed922c52c5e9
- 24afa313-0d3b-4c7c-b485-1047fd964b60
- 05dc046c-60e9-4ef7-965e-91660adffa68

In Gestione risorse modello goto `EtwEventSourceProviderConfiguration` sezione nel `WadCfg` e aggiungere hello seguenti voci:

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> Se il cluster di Service Fabric con più tipi di nodo, quindi è necessario aggiungere la sezione precedente di hello per hello tutti `WadCfg` sezioni.

## <a name="download-hello-app-package"></a>Scaricare il pacchetto di app hello

Scaricare l'applicazione hello da hello [collegamento per il download](https://go.microsoft.com/fwlink/P/?linkid=849590).

## <a name="configure-hello-app"></a>Configurare l'applicazione hello

comportamento dell'app di orchestrazione patch hello Hello può essere configurato toomeet le proprie esigenze. Eseguire l'override di valori predefiniti di hello passando il parametro applicazione hello durante la creazione dell'applicazione o l'aggiornamento. È possibile specificare i parametri dell'applicazione specificando `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` o `New-ServiceFabricApplication` cmdlet.

|**Parametro**        |**Tipo**                          | **Dettagli**|
|:-|-|-|
|MaxResultsToCache    |long                              | Numero massimo di risultati di Windows Update memorizzabili nella cache. <br>Il valore predefinito è 3000 presumendo che il: <br> - Numero di nodi sia 20. <br> - Numero di aggiornamenti eseguiti su un nodo per ogni mese sia pari a cinque. <br> - Numero di risultati per ogni operazione sia pari a 10. <br> -Risultati per tre mesi hello devono essere archiviati. |
|TaskApprovalPolicy   |Enum <br> {NodeWise, UpgradeDomainWise}                          |TaskApprovalPolicy indica i criteri di hello toobe utilizzato per gli aggiornamenti di Windows hello servizio Coordinator tooinstall tra nodi del cluster di Service Fabric hello.<br>                         I valori consentiti sono i seguenti: <br>                                                           <b>NodeWise</b>. Windows Update viene installato un nodo alla volta. <br>                                                           <b>UpgradeDomainWise</b>. Windows Update viene installato un dominio di aggiornamento alla volta (Al massimo hello, tutti i nodi di hello appartenenti tooan dominio di aggiornamento possono andare a Windows Update).
|LogsDiskQuotaInMB   |long  <br> Predefinito: 1024               |Dimensione massima in MB dei log di Patch Orchestration App che è possibile salvare in modo permanente e locale sui nodi.
| WUQuery               | string<br>Impostazione predefinita: "IsInstalled = 0"                | Eseguire una query tooget gli aggiornamenti di Windows. Per altre informazioni, vedere [WuQuery](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx).
| InstallWindowsOSOnlyUpdates | Booleano <br> Predefinito: True                 | Questo flag consente operativo toobe gli aggiornamenti di sistema installato Windows.            |
| WUOperationTimeOutInMinutes | int <br>Predefinito: 90                   | Specifica il timeout di hello per le operazioni di aggiornamento di Windows (ricerca o scaricare o installare). Se l'operazione di hello non viene completata entro hello timeout specificato, che sia interrotto.       |
| WURescheduleCount     | int <br> Predefinito: 5                  | numero massimo di Hello di volte in cui il servizio hello Ripianifica hello Windows update in caso di un'operazione in modo permanente.          |
| WURescheduleTimeInMinutes | int <br>Predefinito: 30 | intervallo di Hello in cui hello servizio Ripianifica l'aggiornamento di Windows hello in caso di errore persiste. |
| WUFrequency           | Stringa separata da virgole Predefinito: "Weekly, Wednesday, 7:00:00"     | frequenza di Hello per l'installazione di Windows Update. Hello formato e i possibili valori sono: <br>-   Monthly, DD,HH:MM:SS, ad esempio, Monthly, 5,12:22:32. <br> -   Weekly, DAY,HH:MM:SS, ad esempio, Weekly, Tuesday, 12:22:32.  <br> -   Daily, HH:MM:SS, ad esempio, Daily, 12:22:32.  <br> - None: indica che non deve essere eseguito Windows Update.  <br><br> Si noti che tutti gli orari di hello in formato UTC.|
| AcceptWindowsUpdateEula | Booleano <br>Predefinito: True | Impostando questo flag, l'applicazione hello accetta hello contratto di licenza dell'utente finale per Windows Update per conto del proprietario di hello della macchina hello.              |

> [!TIP]
> Se si desidera immediatamente toohappen Windows Update, impostare `WUFrequency` toohello relativo tempo di distribuzione dell'applicazione. Ad esempio, si supponga che un'applicazione prova cinque nodi cluster e piano toodeploy hello a circa 17:00:00 UTC. Se si presuppone che l'aggiornamento dell'applicazione hello o distribuzione richiede 30 minuti hello hello massima, imposta WUFrequency "Giornalieri, 17:30:00."

## <a name="deploy-hello-app"></a>Distribuire l'applicazione hello

1. Completare tutti i cluster del hello tooprepare hello passaggi preliminari.
2. Distribuire app di orchestrazione patch hello come qualsiasi altra app Service Fabric. È possibile distribuire l'applicazione hello tramite PowerShell. Seguire i passaggi di hello in [distribuire e rimuovere le applicazioni con PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).
3. un'applicazione hello tooconfigure in fase di distribuzione, passare hello di hello `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet. Per praticità, è stato fornito uno script hello Deploy.ps1 insieme a un'applicazione hello. script di hello toouse:

    - Connettere il cluster di Service Fabric tooa utilizzando `Connect-ServiceFabricCluster`.
    - Eseguire lo script di PowerShell di hello Deploy.ps1 con hello appropriato `ApplicationParameter` valore.

> [!NOTE]
> Consente di mantenere script hello e cartella dell'applicazione hello PatchOrchestrationApplication hello stessa directory.

## <a name="upgrade-hello-app"></a>Aggiornare l'applicazione hello

tooupgrade un'app di orchestrazione patch esistente tramite PowerShell, seguire i passaggi hello [aggiornamento dell'applicazione di Service Fabric con PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).

## <a name="remove-hello-app"></a>Rimuovere l'applicazione hello

un'applicazione hello tooremove, seguire la procedura seguente hello in [distribuire e rimuovere le applicazioni con PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).

Per praticità, è stato fornito uno script hello Undeploy.ps1 insieme a un'applicazione hello. script di hello toouse:

  - Connettere il cluster di Service Fabric tooa utilizzando ```Connect-ServiceFabricCluster```.

  - Esecuzione di script di PowerShell hello Undeploy.ps1.

> [!NOTE]
> Consente di mantenere script hello e cartella dell'applicazione hello PatchOrchestrationApplication hello stessa directory.

## <a name="view-hello-windows-update-results"></a>Visualizzare i risultati di aggiornamento di Windows hello

app di orchestrazione patch Hello espone utente toohello di API REST toodisplay hello risultati cronologici. Un esempio di risultato hello JSON:
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
Se l'aggiornamento non è stato ancora pianificato, il risultato di hello JSON è vuoto.

Accedi toohello cluster tooquery Windows Update risultati. Trovare l'indirizzo di replica hello per il sito primario di hello di hello servizio Coordinator quindi hit hello URL dal browser hello: http://&lt;REPLICA IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 / GetWindowsUpdateResults.

endpoint REST Hello per il servizio coordinatore hello dispone di una porta dinamica. toocheck hello URL esatto, fare riferimento toohello Service Fabric Explorer. Ad esempio, i risultati di hello sono disponibili in `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.

![Immagine dell'endpoint REST](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


Se il proxy inverso hello è abilitata sul cluster hello, è possibile accedere hello URL esterni nonché cluster hello.
endpoint che deve toobe Hello hit è http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.

proxy inverso di hello tooenable nel cluster hello, seguire i passaggi hello [inverso in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy). 

> 
> [!WARNING]
> Dopo la configurazione proxy inverso hello, tutti i servizi cluster hello micro che espongono un endpoint HTTP sono indirizzabili da all'esterno del cluster di hello.

## <a name="diagnosticshealth-events"></a>Eventi di diagnostica/integrità

### <a name="collect-patch-orchestration-app-logs"></a>Raccogliere i log di Patch Orchestration App

Vengono raccolti i log di Patch Orchestration App come parte dei log di Service Fabric dalla versione di runtime `5.6.220.9494` e versioni successive.
Per i cluster che eseguono la versione di runtime Service Fabric minore `5.6.220.9494`, i registri possono essere raccolti utilizzando uno dei seguenti metodi hello.

#### <a name="locally-on-each-node"></a>In locale in ogni nodo

I log vengono raccolti localmente su ogni nodo del cluster di Service Fabric se la versione del runtime di Service Fabric è precedente a `5.6.220.9494`. Hello percorso tooaccess hello viene \[Service Fabric\_installazione\_unità\]:\\PatchOrchestrationApplication\\log.

Ad esempio, se Service Fabric viene installato nell'unità D, percorso hello è d:\\PatchOrchestrationApplication\\log.

#### <a name="central-location"></a>Posizione centrale

Se diagnostica Azure è configurata come parte di alcuni passaggi, i registri per app di orchestrazione hello patch sono disponibili in archiviazione di Azure.

### <a name="health-reports"></a>Report sull'integrità

app di orchestrazione patch Hello pubblica anche rapporti di integrità in base hello servizio Coordinator o hello servizio agente del nodo in hello seguenti casi:

#### <a name="a-windows-update-operation-failed"></a>Un'operazione di Windows Update ha avuto esito negativo

Se un'operazione di aggiornamento di Windows non riesce in un nodo, viene generato un report di integrità su hello servizio agente del nodo. Dettagli del rapporto di stato hello contengono il nome di nodo problematico hello.

Dopo l'applicazione di patch è stata completata nel nodo problematico hello, report hello viene automaticamente cancellato.

#### <a name="hello-node-agent-ntservice-is-down"></a>Hello NTService agente nodo è inattivo

Se hello NTService agente nodo è attivo in un nodo, viene generato un report di integrità a livello di avviso su hello servizio agente del nodo.

#### <a name="hello-repair-manager-service-is-not-enabled"></a>servizio di gestione di Hello riparazione non è abilitato.

Se il servizio di gestione ripristino hello non viene trovato nel cluster hello, viene generato un report di integrità a livello di avviso per il servizio coordinatore hello.

## <a name="frequently-asked-questions"></a>Domande frequenti

D: **Perché è presente il cluster in uno stato di errore durante l'esecuzione di app di orchestrazione patch hello?**

R. Durante il processo di installazione di hello, hello patch orchestrazione app disabilita o riavvia nodi, che possono comportare temporaneamente integrità hello del cluster di hello risulti non disponibile.

In base ai criteri di hello per un'applicazione hello, entrambi un nodo può scendere durante un'operazione di gestione delle patch *o* un intero dominio di aggiornamento può scendere contemporaneamente.

Fine hello di installazione dell'aggiornamento di Windows hello, hello nodi vengono riabilitati dopo il riavvio.

Nell'esempio seguente di hello, cluster hello è verificato un stato di errore tooan temporaneamente perché i due nodi sono inattivi e hello MaxPercentageUnhealthNodes criterio violato. Errore di Hello è temporanea fino a quando non è in corso l'applicazione di patch operazione hello.

![Immagine del cluster non integro](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

Se hello problema persiste, consultare la sezione Risoluzione dei problemi toohello.

D: **Patch Orchestration App è in stato di avviso**

R. Se un rapporto di stato registrato a fronte di un'applicazione hello hello radice causa, controllare toosee. Avviso di hello contiene in genere, i dettagli del problema hello. Se il problema di hello è temporaneo, un'applicazione hello è previsto tooauto-Ripristina da questo stato.

D: **Che cosa può fare se il cluster è integro ed è necessario un aggiornamento del sistema operativo urgenti toodo**

R. app di orchestrazione Hello patch non installare gli aggiornamenti mentre il cluster hello è integro. Provare toobring cluster tooa integro toounblock hello patch orchestrazione app flusso di lavoro.

D: **Perché l'applicazione di patch per i cluster richiede molto tempo toorun?**

R. tempo di Hello necessario dall'app di orchestrazione patch hello dipende principalmente hello seguenti fattori:

- criteri di Hello di hello servizio coordinatore. 
  - criteri predefiniti, Hello `NodeWise`, comporta l'applicazione di patch solo un nodo alla volta. In particolare nel caso di hello di cluster più grande, è consigliabile utilizzare hello `UpgradeDomainWise` tooachieve criteri più veloce l'applicazione di patch per i cluster.
- numero di Hello degli aggiornamenti disponibili per il download e installazione. 
- installare un aggiornamento, che non deve superare un paio d'ore Hello toodownload tempo medio necessario.
- prestazioni Hello di larghezza di banda di rete e macchina virtuale hello.

D: **Motivo per cui è non vengono visualizzati alcuni aggiornamenti in Windows Update risultati ottenuti tramite l'api REST, ma non nella cronologia di Windows Update sul computer hello?**

R. Alcuni aggiornamenti del prodotto è necessario toobe archiviata la cronologia delle rispettive/patch di aggiornamento. Ad esempio: gli aggiornamenti di Windows Defender non vengono visualizzati nella cronologia di Windows Update in Windows Server 2016.

## <a name="disclaimers"></a>Dichiarazioni di non responsabilità

- app di Hello patch orchestrazione accetta hello contratto di licenza dell'utente finale di Windows Update per conto di utente hello. Facoltativamente, hello impostazione può essere disattivata nella configurazione di hello di un'applicazione hello.

- Hello patch orchestrazione app raccoglie dati di telemetria tootrack utilizzo e delle prestazioni. dati di telemetria dell'applicazione Hello segue l'impostazione di hello dell'impostazione di telemetria del runtime di Service Fabric hello (che è attivata per impostazione predefinita).

## <a name="troubleshooting"></a>Risoluzione dei problemi

### <a name="a-node-is-not-coming-back-tooup-state"></a>Un nodo non tornerà tooup stato

**nodo Hello potrebbe essere bloccata in uno stato di disattivazione perché**:

Un controllo di sicurezza è in sospeso. tooremedy questa situazione, verificare che siano disponibili sufficienti nodi in uno stato integro.

**nodo Hello potrebbe essere bloccata in uno stato disabilitato perché**:

- nodo Hello è stata disabilitata manualmente.
- nodo Hello è stata disabilitata a causa di processo di tooan dell'infrastruttura di Azure in corso.
- nodo Hello è stata disabilitata temporaneamente dal nodo di hello patch orchestrazione app toopatch hello.

**Hello nodo potrebbe essere bloccato in uno stato inattivo perché**:

- nodo Hello è stato inserito manualmente in uno stato inattivo.
- nodo Hello è in fase di riavvio (che potrebbe essere attivato da hello patch orchestrazione app).
- nodo Hello è inattivo a causa di tooa difettoso VM o computer o rete problemi di connettività.

### <a name="updates-were-skipped-on-some-nodes"></a>Gli aggiornamenti sono stati ignorati in alcuni nodi

app di orchestrazione patch Hello tenta tooinstall un aggiornamento in base toohello riprogrammazione criterio di Windows. servizio Hello tenta nodo hello toorecover e ignorare i criteri di applicazione di hello aggiornamento secondo toohello.

In tal caso, viene generato un report di integrità a livello di avviso su hello servizio agente del nodo. il risultato di Hello di Windows Update contiene anche motivo possibile: hello errore hello.

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a>integrità Hello del cluster di hello passa tooerror durante l'installazione dell'aggiornamento hello

Un aggiornamento di Windows non corretto può compromettere l'integrità di hello di un'applicazione o del cluster in un nodo particolare o di un dominio di aggiornamento. Hello patch orchestrazione app interrompe un'operazione di aggiornamento di Windows successive fino a cluster hello è integro nuovamente.

Un amministratore deve intervenire e determinare perché un'applicazione hello o il cluster è diventato non integro scadenza tooWindows Update.

## <a name="release-notes-"></a>Note sulla versione:

### <a name="version-110"></a>Versione 1.1.0
- Versione pubblica

### <a name="version-111"></a>Versione 1.1.1
- Correzione di un bug in SetupEntryPoint di NodeAgentService che ha impedito l'installazione di NodeAgentNTService.

### <a name="version-120-latest"></a>Versione 1.2.0 (versione più recente)

- Correzioni di bug nel flusso di lavoro di riavvio del sistema.
- Correzione di bug nella creazione di attività RM a causa di controllo di integrità toowhich durante la preparazione delle attività di ripristino si verificava come previsto.
- Hello modificato la modalità di avvio del servizio windows POANodeSvc toodelayed automatico.
