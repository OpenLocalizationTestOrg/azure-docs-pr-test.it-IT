---
title: un cluster di Azure Service Fabric aaaUpgrade | Documenti Microsoft
description: "Aggiornare il codice di Service Fabric hello e/o di configurazione che esegue un cluster di Service Fabric, inclusa l'impostazione di modalità di aggiornamento del cluster, aggiornamento dei certificati, aggiunta di porte di applicazione, questa patch del sistema operativo, e così via. Cosa può aspettarsi quando vengono eseguiti gli aggiornamenti di hello?"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 15190ace-31ed-491f-a54b-b5ff61e718db
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/10/2017
ms.author: chackdan
ms.openlocfilehash: 94ac3833ec0810f79de06ecb50f254028fa90408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-azure-service-fabric-cluster"></a>Aggiornare un cluster di Azure Service Fabric
> [!div class="op_single_selector"]
> * [Cluster di Azure](service-fabric-cluster-upgrade.md)
> * [Cluster autonomo](service-fabric-cluster-upgrade-windows-server.md)
> 
> 

Per qualsiasi sistema moderna, progettazione aggiornabilità è successo a lungo termine di tooachieving chiave del prodotto. Un cluster di Azure Service Fabric è una risorsa di proprietà dell'utente parzialmente gestita da Microsoft. Questo articolo descrive ciò che viene gestito automaticamente e ciò che è possibile configurare manualmente.

## <a name="controlling-hello-fabric-version-that-runs-on-your-cluster"></a>Controllo della versione di fabric hello che esegue il cluster
È possibile impostare l'infrastruttura di cluster tooreceive automatica gli aggiornamenti rilasciati da Microsoft o è possibile selezionare una versione supportata dell'infrastruttura desiderato toobe il cluster.

A tale scopo, configurazione del cluster "upgradeMode" hello impostazione nel portale di hello o tramite Gestione risorse in fase di creazione di hello o in seguito a un cluster in tempo reale 

> [!NOTE]
> Verificare che tookeep il cluster che esegue una versione supportata dell'infrastruttura sempre. Come e quando è annunciare il rilascio di hello di una nuova versione dell'infrastruttura di servizio, la versione precedente di hello è contrassegnata per la fine del supporto dopo un minimo di 60 giorni dalla data. Hello nuove versioni hello vengono annunciate [sul blog del team di infrastruttura servizio hello](https://blogs.msdn.microsoft.com/azureservicefabric/). nuova versione di Hello è quindi disponibile toochoose. 
> 
> 

14 giorni precedenti toohello scadenza della versione di hello nel cluster è in esecuzione, viene generato un evento di integrità che inserisce il cluster in uno stato di integrità di avviso. cluster di Hello rimane in uno stato di avviso fino a quando non si esegue l'aggiornamento di versione di fabric supportati tooa.

### <a name="setting-hello-upgrade-mode-via-portal"></a>Impostazione della modalità di aggiornamento hello tramite portale
Quando si crea il cluster hello, è possibile impostare hello cluster tooautomatic o manuale.

![Creazione - Modalità manuale][Create_Manualmode]

È possibile impostare hello cluster tooautomatic o manuale quando in un cluster in tempo reale, utilizzando hello gestire l'esperienza. 

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-portal"></a>L'aggiornamento di tooa nuova versione in un cluster che è impostato la modalità tooManual tramite portale.
nuova versione tooa tooupgrade, toodo è sufficiente selezionare la versione disponibile hello dall'elenco a discesa hello e salvare. aggiornamento di Fabric Hello Ottiene avviata automaticamente. Hello criteri di integrità del cluster (una combinazione di integrità del nodo e l'integrità di hello tutti hello applicazioni in esecuzione nel cluster hello) siano rispettati aggiornamento hello tooduring.

Se non vengono soddisfatti i criteri di integrità del cluster di hello, viene eseguito il rollback di aggiornamento hello. Scorrere verso il basso tooread questo documento altre su come tooset tali criteri di integrità personalizzato. 

Dopo aver risolto i problemi di hello che ha comportato il rollback di hello, necessari, l'aggiornamento di hello tooinitiate nuovamente, hello seguente stessi passaggi come prima.

![Gestione - Modalità automatica][Manage_Automaticmode]

### <a name="setting-hello-upgrade-mode-via-a-resource-manager-template"></a>Impostazione della modalità di aggiornamento hello tramite un modello di gestione risorse
Aggiungere hello definizione di risorsa Microsoft.ServiceFabric/clusters toohello "upgradeMode" configurazione e set hello "clusterCodeVersion" tooone di hello supportate versioni dell'infrastruttura, come illustrato di seguito e quindi distribuire il modello di hello. i valori validi di Hello per "upgradeMode" sono "Manuale" o "Automatico"

![Modalità di aggiornamento tramite Azure Resource Manager][ARMUpgradeMode]

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-a-resource-manager-template"></a>L'aggiornamento di tooa nuova versione in un cluster che è impostato la modalità tooManual tramite un modello di gestione risorse.
Quando il cluster di hello è in modalità manuale, tooupgrade tooa nuova versione, modificare una versione supportata di tooa clusterCodeVersion"hello" e distribuirlo. distribuzione di Hello del modello di hello, viene attivata di aggiornamento di Fabric hello Ottiene avviata automaticamente. Hello criteri di integrità del cluster (una combinazione di integrità del nodo e l'integrità di hello tutti hello applicazioni in esecuzione nel cluster hello) siano rispettati aggiornamento hello tooduring.

Se non vengono soddisfatti i criteri di integrità del cluster di hello, viene eseguito il rollback di aggiornamento hello. Scorrere verso il basso tooread questo documento altre su come tooset tali criteri di integrità personalizzato. 

Dopo aver risolto i problemi di hello che ha comportato il rollback di hello, necessari, l'aggiornamento di hello tooinitiate nuovamente, hello seguente stessi passaggi come prima.

### <a name="get-list-of-all-available-version-for-all-environments-for-a-given-subscription"></a>Ottenere l'elenco di tutte le versioni disponibili per tutti gli ambienti per una determinata sottoscrizione
Eseguire hello comando seguente ed è necessario ottenere un toothis simili di output.

"supportExpiryUtc" indica la scadenza di una determinata versione. Hello versione più recente non hanno una data valida: è il valore "9999-12-31T23:59:59.9999999", che significa che la data di scadenza hello non è ancora impostata.

```REST
GET https://<endpoint>/subscriptions/{{subscriptionId}}/providers/Microsoft.ServiceFabric/locations/{{location}}/clusterVersions?api-version=2016-09-01

Example: https://management.azure.com/subscriptions/1857f442-3bce-4b96-ad95-627f76437a67/providers/Microsoft.ServiceFabric/locations/eastus/clusterVersions?api-version=2016-09-01

Output:
{
                  "value": [
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/5.0.1427.9490",
                      "name": "5.0.1427.9490",
                      "type": "Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.0.1427.9490",
                        "supportExpiryUtc": "2016-11-26T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.0.1427.9490",
                      "name": "5.1.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.1.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.4.1427.9490",
                      "name": "4.4.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "4.4.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Linux"
                      }
                    }
                  ]
                }


```

## <a name="fabric-upgrade-behavior-when-hello-cluster-upgrade-mode-is-automatic"></a>Comportamento dell'aggiornamento dell'infrastruttura quando la modalità di aggiornamento del cluster hello è automatico
Microsoft gestisce il codice di fabric hello e la configurazione che viene eseguito in un cluster di Azure. Software toohello gli aggiornamenti automatici di monitorato eseguita in base alle esigenze. Gli aggiornamenti possono interessare il codice, la configurazione o entrambi. Assicurarsi che l'applicazione non subisce alcun impatto o un impatto minimo a causa di aggiornamenti toothese toomake, eseguita aggiornamenti hello in hello seguenti fasi:

### <a name="phase-1-an-upgrade-is-performed-by-using-all-cluster-health-policies"></a>Fase 1: Un aggiornamento viene eseguito usando tutti i criteri di integrità del cluster
Durante questa fase, gli aggiornamenti di hello procedere a un dominio di aggiornamento in un momento e le applicazioni di hello che erano in esecuzione nel cluster hello continuano toorun senza alcun tempo di inattività. Hello criteri di integrità del cluster (una combinazione di integrità del nodo e l'integrità di hello tutti hello applicazioni in esecuzione nel cluster hello) siano rispettati aggiornamento hello tooduring.

Se non vengono soddisfatti i criteri di integrità del cluster di hello, viene eseguito il rollback di aggiornamento hello. Quindi toohello proprietario della sottoscrizione hello viene inviato un messaggio. messaggio di posta elettronica Hello contiene hello le seguenti informazioni:

* Notifica che è stato nuovamente tooroll un aggiornamento del cluster.
* Eventuali azioni correttive suggerite.
* numero di Hello di giorni (n) fino a quando non viene eseguita la fase 2.

Si tenta di hello tooexecute che stesso aggiornare alcune altre volte in caso di eventuali aggiornamenti non riuscita per motivi di infrastruttura. Dopo aver hello n giorni dal messaggio di posta elettronica hello data hello è stato inviato, procedere tooPhase 2.

Se vengono soddisfatti i criteri di integrità del cluster di hello, l'aggiornamento di hello è considerata riuscita e contrassegnata come completata. Ciò può verificarsi durante l'aggiornamento iniziale hello o una qualsiasi delle repliche aggiornamento hello in questa fase. Non viene inviato alcun messaggio di posta elettronica di conferma in caso di esecuzione riuscita. Si tratta di tooavoid invio si troppi messaggi di posta elettronica, la ricezione di un messaggio di posta elettronica dovrebbero essere considerate come toonormal un'eccezione. È probabile che la maggior parte delle toosucceed gli aggiornamenti di hello cluster senza conseguenze per la disponibilità dell'applicazione.

### <a name="phase-2-an-upgrade-is-performed-by-using-default-health-policies-only"></a>Fase 2: Un aggiornamento viene eseguito usando solo i criteri di integrità predefiniti
criteri di integrità Hello in questa fase vengono impostati in modo che il numero di hello di applicazioni che sono stati integro all'inizio di hello dell'aggiornamento di hello rimane uguale per hello durata del processo di aggiornamento hello hello. Fase 1, gli aggiornamenti di hello fase 2 procedere a un dominio di aggiornamento in un momento e le applicazioni di hello che erano in esecuzione nel cluster hello continuano toorun senza alcun tempo di inattività. criteri di integrità del cluster Hello (una combinazione di integrità del nodo e l'integrità di hello che tutti hello applicazioni in esecuzione nel cluster hello) sono rispettate toofor hello durata dell'aggiornamento hello.

Se i criteri di integrità del cluster hello attive non vengono soddisfatte, viene eseguito il rollback di aggiornamento hello. Quindi toohello proprietario della sottoscrizione hello viene inviato un messaggio. messaggio di posta elettronica Hello contiene hello le seguenti informazioni:

* Notifica che è stato nuovamente tooroll un aggiornamento del cluster.
* Eventuali azioni correttive suggerite.
* numero di Hello di giorni (n) fino a quando non viene eseguita una fase 3.

Si tenta di hello tooexecute che stesso aggiornare alcune altre volte in caso di eventuali aggiornamenti non riuscita per motivi di infrastruttura. Viene inviato un messaggio di sollecito alcuni giorni prima della scadenza degli n giorni. Dopo aver hello n giorni dal messaggio di posta elettronica hello data hello è stato inviato, procedere tooPhase 3. messaggi di posta elettronica Hello che ti abbiamo inviato nella fase 2 devono essere prese gravemente ed è necessario eseguire le azioni correttive.

Se vengono soddisfatti i criteri di integrità del cluster di hello, l'aggiornamento di hello è considerata riuscita e contrassegnata come completata. Ciò può verificarsi durante l'aggiornamento iniziale hello o una qualsiasi delle repliche aggiornamento hello in questa fase. Non viene inviato alcun messaggio di posta elettronica di conferma in caso di esecuzione riuscita.

### <a name="phase-3-an-upgrade-is-performed-by-using-aggressive-health-policies"></a>Fase 3: Un aggiornamento viene eseguito usando criteri di integrità aggressivi
Questi criteri di integrità in questa fase sono pensati per il completamento dell'aggiornamento hello anziché hello dello stato di hello applicazioni. In questa fase verranno completati pochi aggiornamenti del cluster. Se il cluster Ottiene toothis fase, è probabile che l'applicazione diventa non integro e/o perdere la disponibilità.

Toohello simile ad altre due fasi, gli aggiornamenti di fase 3 procedere un dominio di aggiornamento alla volta.

Se non vengono soddisfatti i criteri di integrità del cluster di hello, viene eseguito il rollback di aggiornamento hello. Si tenta di hello tooexecute che stesso aggiornare alcune altre volte in caso di eventuali aggiornamenti non riuscita per motivi di infrastruttura. Successivamente, cluster hello è bloccata, in modo che non riceveranno più supporto e/o gli aggiornamenti.

Proprietario della sottoscrizione toohello, insieme a operazioni correttive hello viene inviato un messaggio con queste informazioni. Non Prevediamo tooget qualsiasi cluster in uno stato in fase 3 non è riuscita.

Se vengono soddisfatti i criteri di integrità del cluster di hello, l'aggiornamento di hello è considerata riuscita e contrassegnata come completata. Ciò può verificarsi durante l'aggiornamento iniziale hello o una qualsiasi delle repliche aggiornamento hello in questa fase. Non viene inviato alcun messaggio di posta elettronica di conferma in caso di esecuzione riuscita.

## <a name="cluster-configurations-that-you-control"></a>Configurazioni del cluster controllate manualmente
Modalità di aggiornamento cluster hello tooset possibilità di toohello inoltre, ecco le configurazioni di hello che è possibile modificare in un cluster in tempo reale.

### <a name="certificates"></a>Certificati
È possibile aggiungere o eliminare i certificati per cluster hello e client tramite il portale di hello facilmente. Fare riferimento troppo[questo documento per istruzioni dettagliate](service-fabric-cluster-security-update-certs-azure.md)

![Schermata che mostra identificazioni personali del certificato nel portale di Azure hello.][CertificateUpgrade]

### <a name="application-ports"></a>Porte dell'applicazione
È possibile modificare le porte applicazione modificando le proprietà delle risorse di bilanciamento del carico hello associati al tipo di nodo hello. È possibile utilizzare il portale di hello oppure è possibile utilizzare Gestione risorse di PowerShell direttamente.

hello tooopen una nuova porta in tutte le macchine virtuali in un tipo di nodo seguenti:

1. Aggiungere un nuovo bilanciamento del carico appropriato toohello probe.
   
    Se il cluster è stata distribuita tramite il portale di hello, servizi di bilanciamento del carico hello sono denominati "LB-nome del gruppo di risorse hello-NodeTypename", uno per ogni tipo di nodo. Poiché i nomi del bilanciamento del carico di hello sono univoci solo all'interno di un gruppo di risorse, è consigliabile se la ricerca in un gruppo di risorse specifico.
   
    ![Schermata che mostra l'aggiunta di un tooa probe bilanciamento del carico nel portale di hello.][AddingProbes]
2. Aggiungere un nuovo servizio di bilanciamento del carico toohello regola.
   
    Aggiungere un nuovo toohello regola stesso il bilanciamento del carico tramite probe hello creato nel passaggio precedente hello.
   
    ![Aggiunta di un nuovo servizio di bilanciamento del carico tooa regola nel portale di hello.][AddingLBRules]

### <a name="placement-properties"></a>Proprietà di posizionamento
Per ognuno dei tipi di nodo hello, è possibile aggiungere proprietà di posizionamento personalizzati che si desidera toouse nelle applicazioni. NodeType è una proprietà predefinita che è possibile usare senza aggiungerla in modo esplicito.

> [!NOTE]
> Per informazioni dettagliate sull'uso di hello di vincoli di posizionamento, proprietà del nodo, e come toodefine, vedere toohello sezione "Vincoli di posizionamento e proprietà del nodo" nel documento di servizio di gestione delle risorse Cluster dell'infrastruttura hello in [che descrive il Cluster ](service-fabric-cluster-resource-manager-cluster-description.md).
> 
> 

### <a name="capacity-metrics"></a>Metriche della capacità
Per ognuno dei tipi di nodo hello, è possibile aggiungere le metriche di capacità personalizzato che si desidera toouse del carico tooreport applicazioni. Per informazioni dettagliate sull'uso di hello del carico tooreport metriche di capacità, vedere toohello documenti di servizio di gestione delle risorse Cluster dell'infrastruttura su [che descrive il Cluster](service-fabric-cluster-resource-manager-cluster-description.md) e [metriche e carico](service-fabric-cluster-resource-manager-metrics.md).

### <a name="fabric-upgrade-settings---health-polices"></a>Impostazioni di aggiornamento di Fabric: criteri di integrità
È possibile specificare criteri di integrità personalizzati per l'aggiornamento di Fabric. Se è stata impostata la tooAutomatic cluster gli aggiornamenti dell'infrastruttura, questi criteri otterranno applicato toohello fase 1 di aggiornamento automatico dell'infrastruttura hello.
Se è stato impostato il cluster per l'infrastruttura manuale degli aggiornamenti, quindi questi criteri vengono applicati a ogni volta che si seleziona una nuova versione di hello sistema tookick disattivare l'aggiornamento dell'infrastruttura di hello del cluster di trigger. Se si esegue l'override criteri hello, vengono utilizzati i valori predefiniti di hello.

È possibile specificare i criteri di integrità personalizzato hello o rivedere le impostazioni correnti di hello nel Pannello di "aggiornamento di fabric" hello, selezionando le impostazioni di aggiornamento avanzata hello. Esaminare hello seguendo come immagine. 

![Gestire criteri di integrità personalizzati][HealthPolices]

### <a name="customize-fabric-settings-for-your-cluster"></a>Personalizzare le impostazioni di Fabric per il cluster
Fare riferimento troppo[le impostazioni dell'infrastruttura di cluster di infrastruttura del servizio](service-fabric-cluster-fabric-settings.md) su cosa e come è possibile personalizzare.

### <a name="os-patches-on-hello-vms-that-make-up-hello-cluster"></a>Patch del sistema operativo su macchine virtuali che costituiscono il cluster hello hello
Fare riferimento troppo[applicazione di Patch orchestrazione](service-fabric-patch-orchestration-application.md) che può essere distribuito in modo orchestrato, mantenendo servizi hello disponibili tutto il tempo hello le patch tooinstall cluster da Windows Update. 

### <a name="os-upgrades-on-hello-vms-that-make-up-hello-cluster"></a>Aggiornamenti del sistema operativo su macchine virtuali che costituiscono il cluster hello hello
Se è necessario aggiornare l'immagine del sistema operativo hello in hello di macchine virtuali del cluster di hello, è necessario utilizzare una macchina virtuale alla volta. L'esecuzione dell'aggiornamento è un'operazione manuale, non è attualmente disponibile alcun tipo di automazione.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come toocustomize alcune hello [le impostazioni dell'infrastruttura di cluster di infrastruttura del servizio](service-fabric-cluster-fabric-settings.md)
* Informazioni su come troppo[aumentare e ridurre il cluster](service-fabric-cluster-scale-up-down.md)
* Informazioni su come eseguire [aggiornamenti dell'applicazione](service-fabric-application-upgrade.md)

<!--Image references-->
[CertificateUpgrade]: ./media/service-fabric-cluster-upgrade/CertificateUpgrade2.png
[AddingProbes]: ./media/service-fabric-cluster-upgrade/addingProbes2.PNG
[AddingLBRules]: ./media/service-fabric-cluster-upgrade/addingLBRules.png
[HealthPolices]: ./media/service-fabric-cluster-upgrade/Manage_AutomodeWadvSettings.PNG
[ARMUpgradeMode]: ./media/service-fabric-cluster-upgrade/ARMUpgradeMode.PNG
[Create_Manualmode]: ./media/service-fabric-cluster-upgrade/Create_Manualmode.PNG
[Manage_Automaticmode]: ./media/service-fabric-cluster-upgrade/Manage_Automaticmode.PNG
