---
title: aaaService gestione delle risorse dell'infrastruttura Cluster - integrazione di gestione | Documenti Microsoft
description: Panoramica dei punti di integrazione hello tra hello gestione delle risorse Cluster e gestione dei servizi dell'infrastruttura.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 956cd0b8-b6e3-4436-a224-8766320e8cd7
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9a24c9de121fbe2e8e5e8e4d117e64686918936a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-integration-with-service-fabric-cluster-management"></a>Integrazione di Cluster Resource Manager con la gestione dei cluster di Service Fabric
Hello servizio di gestione delle risorse Cluster dell'infrastruttura non unità gli aggiornamenti nell'infrastruttura del servizio, ma è interessato. primo modo hello consente di gestione delle risorse Cluster con la gestione da rilevamento hello Hello desiderato stato del cluster hello e servizi di hello in essa contenuti. Gestione delle risorse Cluster Hello Invia rapporti di stato quando non è inserito cluster hello nella configurazione desiderata hello. Ad esempio, se è sufficiente hello capacità gestione delle risorse Cluster invia avvisi salute e gli errori che indicano il problema di hello. Un altro componente di integrazione è toodo con funzionamento degli aggiornamenti. Gestione delle risorse Cluster Hello modifica il comportamento leggermente durante gli aggiornamenti.  

## <a name="health-integration"></a>Integrazione di integrità
Gestione delle risorse Cluster Hello tiene traccia costantemente regole hello definite per il posizionamento dei servizi. Tiene inoltre traccia hello residua per ogni metrica nei nodi di hello e in cluster hello e in cluster hello nel suo complesso. Se non riesce a soddisfare queste regole o se la capacità è insufficiente vengono generati errori e avvisi di integrità. Ad esempio, se un nodo è sulla capacità e hello gestione delle risorse Cluster tenterà situazione hello toofix spostando i servizi. Se è possibile correggere la situazione hello emette un avviso di integrità che indica il nodo è di capacità di failover e per le metriche.

Un altro esempio di avvisi di integrità di gestione risorse di hello è violazioni dei vincoli di posizionamento. Ad esempio, se è stato definito un vincolo di posizione (ad esempio `“NodeColor == Blue”`) e Gestione risorse di hello rileva la violazione di vincolo, che viene generato un avviso di integrità. Questo vale per i vincoli personalizzati e hello predefinito (ad esempio, i vincoli di dominio di errore e dominio di aggiornamento hello).

Di seguito è riportato un esempio di rapporto di integrità. In questo caso, il rapporto di stato hello è per una delle partizioni del servizio di sistema hello. messaggio di stato Hello indica hello repliche di tale partizione temporaneamente vengono compressi in domini di aggiornamento troppo pochi.

```posh
PS C:\Users\User > Get-WindowsFabricPartitionHealth -PartitionId '00000000-0000-0000-0000-000000000001'


PartitionId           : 00000000-0000-0000-0000-000000000001
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.PLB', Property='ReplicaConstraintViolation_UpgradeDomain', HealthState='Warning', ConsiderWarningAsError=false.

ReplicaHealthStates   :
                        ReplicaId             : 130766528804733380
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577821
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528854889931
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577822
                        AggregatedHealthState : Ok

                        ReplicaId             : 130837073190680024
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.PLB
                        Property              : ReplicaConstraintViolation_UpgradeDomain
                        HealthState           : Warning
                        SequenceNumber        : 130837100116930204
                        SentAt                : 8/10/2015 7:53:31 PM
                        ReceivedAt            : 8/10/2015 7:53:33 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer has detected a Constraint Violation for this Replica: fabric:/System/FailoverManagerService Secondary Partition 00000000-0000-0000-0000-000000000001 is
                        violating hello Constraint: UpgradeDomain Details: UpgradeDomain ID -- 4, Replica on NodeName -- Node.8 Currently Upgrading -- false Distribution Policy -- Packing
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Ok->Warning = 8/10/2015 7:13:02 PM, LastError = 1/1/0001 12:00:00 AM
```

Ecco che cosa indica questo messaggio di stato:

1. Tutte le repliche di hello stessi sono integri: ognuno ha AggregatedHealthState: Ok
2. attualmente viene violato Hello vincolo di distribuzione di aggiornamento del dominio. Ciò significa che un particolare dominio di aggiornamento ha più repliche di questa partizione rispetto a quanto previsto.
3. Il nodo contiene la violazione hello replica che provocano hello. In questo caso è il nodo hello con nome hello "Node.8"
4. Se è in corso un aggiornamento per questa partizione ("Currently Upgrading -- false")
5. criteri di distribuzione per questo servizio Hello: "Distribuzione dei criteri--compressione". Questo è disciplinato dalle hello `RequireDomainDistribution` [criteri di selezione](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing). "Packing" indica che in questo caso DomainDistribution _non_ era necessario e quindi che per questo servizio il criterio di selezione non è stato specificato. 
6. Quando sono report hello - 8/10/2015 19:13:02: 00

Informazioni quali avvisi questo potenze incendio in produzione toolet si conosce si è verificato un errore e viene inoltre utilizzato toodetect e interrompere gli aggiornamenti non validi. In questo caso, sarebbe necessario toosee se è possibile scoprire perché Gestione risorse di hello era repliche hello toopack in hello al dominio di aggiornamento. In genere di compressione è temporaneo perché i nodi hello hello altri domini di aggiornamento sono state verso il basso, ad esempio.

Si supponga hello gestione delle risorse Cluster sta tentando tooplace alcuni servizi, ma non vi sono le soluzioni di lavoro. Quando i servizi non possono essere inseriti, è in genere per uno dei seguenti motivi hello:

1. Una condizione temporanea ha reso possibile tooplace questa istanza del servizio o una replica correttamente
2. requisiti di posizionamento del servizio Hello sono situazione.

In questi casi, i rapporti di stato dal gestore delle risorse Cluster hello consentono di determinare perché non è possibile inserire il servizio di hello. Si chiama questa sequenza di eliminazione processo hello vincolo. Durante, hello viene elaborato che interessano i record e il servizio hello cui eliminare i vincoli di hello configurato. In questo modo quando i servizi non sono in grado di toobe inserito, è possibile vedere quali nodi sono stati eliminati e sul motivo.

## <a name="constraint-types"></a>Tipi di vincolo
Esaminiamo i vincoli di diversi hello in questi rapporti di integrità. I vincoli di integrità messaggi correlati toothese verrà visualizzato quando non è possibile inserire le repliche.

* **ReplicaExclusionStatic** e **ReplicaExclusionDynamic**: questi vincoli indica che una soluzione è stata rifiutata perché i due oggetti servizio da hello stessa partizione avrebbe toobe posizionato su hello stesso nodo. Ciò non è consentito perché l'errore su quel nodo avrebbe un impatto eccessivo sulla partizione. ReplicaExclusionStatic e ReplicaExclusionDynamic sono quasi hello differenze regola e hello stesso non è importante. Se si verifica una sequenza di eliminazione vincolo contenente un vincolo ReplicaExclusionStatic o ReplicaExclusionDynamic, gestione delle risorse Cluster hello hello ritiene che non vi sono nodi sufficienti. Questa operazione richiede rimanenti soluzioni toouse queste posizioni non validi che non sono consentiti. Hello altri vincoli nella sequenza hello in genere dirà perché i nodi in fase di eliminazione in primo luogo hello.
* **PlacementConstraint**: se viene visualizzato questo messaggio, significa che è stato eliminato alcuni nodi perché i vincoli di posizionamento del servizio hello non corrispondono. Si traccia i vincoli di posizionamento hello attualmente configurato come parte di questo messaggio. Questo è normale se è stato definito un vincolo di posizionamento. Tuttavia, vincoli di posizionamento in modo non corretto causa troppi toobe nodi eliminato se si tratta di come è possibile notare.
* **NodeCapacity**: questo vincolo significa che hello gestione delle risorse Cluster non è stato possibile collocare repliche hello in hello indicato nodi perché che inserirli capacità di failover.
* **Affinità**: indica che è stato possibile inserire replica di hello nei nodi interessato hello perché si verificherebbe una violazione del vincolo di affinità hello. Ulteriori informazioni sull'affinità sono riportate in [questo articolo](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
* **FaultDomain** e **UpgradeDomain**: questo vincolo Elimina nodi se immissione replica hello hello indicato nodi causerebbe compressione in un dominio di aggiornamento o un errore specifico. Vengono presentati alcuni esempi che illustrano il vincolo in argomento hello nella [i vincoli di dominio di errore e di aggiornamento e il comportamento risulta](service-fabric-cluster-resource-manager-cluster-description.md)
* **PreferredLocation**: È in genere non deve visualizzare questo vincolo rimozione di nodi dalla soluzione hello poiché viene eseguito come un'ottimizzazione per impostazione predefinita. Hello preferito vincolo di percorso deve essere presente anche durante gli aggiornamenti. Durante l'aggiornamento è toomove utilizzati servizi back-toowhere quando avviare aggiornamento hello.

## <a name="blocklisting-nodes"></a>Nodi sottoposti a blocklisting
Un altro gestore delle risorse Cluster rapporti di stato messaggio hello è quando i nodi sono blocklisted. È possibile considerare il blocklisting come un vincolo temporaneo che viene applicato automaticamente per l'utente. I nodi vengono sottoposti a blocklisting quando si verificano errori ripetuti durante l'avvio di istanze di quel tipo di servizio. I nodi vengono sottoposti a blocklisting in base al tipo di servizio. Un nodo può essere sottoposto a blocklisting per un tipo di servizio ma non per un altro. 

Si noterà blocklisting avviare spesso durante lo sviluppo: alcuni errori che toocrash di host del servizio all'avvio. Service Fabric tenta l'host del servizio hello toocreate più volte e continua a verificarsi errori di hello. Dopo alcuni tentativi, nodo hello Ottiene blocklisted e hello gestione delle risorse Cluster tenterà di servizio di hello toocreate altrove. Se l'errore persiste in più nodi, è possibile che tutti i nodi valido hello cluster hello finire bloccata. Blocklisting è inoltre possibile rimuovere molti nodi che non è sufficiente avviare correttamente la scala di hello servizio toomeet hello desiderato. Verrà visualizzato in genere altri errori o avvisi dal gestore delle risorse Cluster di hello, che indica che il servizio di hello è inferiore alla replica desiderata hello o conteggio delle istanze, nonché i messaggi di integrità che indicano quali errore hello è che è leader toohello blocklisting in primo luogo hello.

Il blocklisting non è una condizione permanente. Dopo alcuni minuti, hello nodo viene rimosso dal blocco di indirizzi hello e Service Fabric potrebbe attivare nuovamente i servizi di hello in tale nodo. Se servizi continua toofail, nodo hello è blocklisted per tale tipo di servizio. 

### <a name="constraint-priorities"></a>Priorità dei vincoli

> [!WARNING]
> Modificare le priorità dei vincoli non è consigliato e può avere effetti negativi significativi nel cluster. Hello sotto informazioni viene fornita per riferimento di priorità di vincolo default hello e il relativo comportamento. 
>

Per tutti questi vincoli, si potrebbe avere pensato "Hey, ritengo che i vincoli di dominio di errore sono hello più importante nel sistema. In ordine tooensure hello vincoli di dominio di errore non viene violato, sto disposto tooviolate altri vincoli. "

I vincoli possono essere configurati con diversi livelli di priorità. Si tratta di:

   - “hard” (0)
   - “soft” (1)
   - “optimization” (2)
   - “off” (-1). 
   
Per impostazione predefinita, la maggior parte dei vincoli hello sono configurata come vincoli di disco rigidi.

Modifica priorità hello dei vincoli è comune. Sono stati volte in cui le priorità di vincolo necessari toochange, in genere toowork intorno a un altro bug o comportamento che stava incidendo sulle ambiente hello. In genere flessibilità hello dell'infrastruttura di priorità vincolo hello ha funzionato molto bene, ma non è necessaria spesso. Maggior parte del tempo di hello tutto ciò che si trova sulle priorità predefinita. 

livelli di priorità Hello non significa che uno specifico vincolo _verrà_ violate, né che sarà sempre soddisfatto. Le priorità dei vincoli definiscono un ordine in cui i vincoli vengono applicati. Priorità definiscono compromessi hello quando è Impossibile toosatisfy tutti i vincoli. In genere tutti i vincoli di hello possono essere soddisfatta solo se è presente scegliere un'altra risposta nell'ambiente di hello. Alcuni esempi di scenari che potrebbero causare violazioni tooconstraint sono i vincoli in conflitto, o un numero elevato di errori simultanei.

In casi avanzati, è possibile modificare le priorità di vincolo hello. Se ad esempio, si desiderava tooensure che affinità verrebbe violata sempre quando problemi di capacità del nodo toosolve necessarie. tooachieve, è possibile impostare la priorità di hello di hello affinità vincolo troppo "soft" (1) e lasciare vincolo capacità hello impostato troppo "disco" (0).

i valori di priorità predefinito di Hello per vincoli diversi hello vengono specificati hello seguente configurazione:

ClusterManifest.xml

```xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PlacementConstraintPriority" Value="0" />
            <Parameter Name="CapacityConstraintPriority" Value="0" />
            <Parameter Name="AffinityConstraintPriority" Value="0" />
            <Parameter Name="FaultDomainConstraintPriority" Value="0" />
            <Parameter Name="UpgradeDomainConstraintPriority" Value="1" />
            <Parameter Name="PreferredLocationConstraintPriority" Value="2" />
        </Section>
```

mediante ClusterConfig.json per le distribuzioni autonome o Template.json per i cluster ospitati in Azure:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PlacementConstraintPriority",
          "value": "0"
      },
      {
          "name": "CapacityConstraintPriority",
          "value": "0"
      },
      {
          "name": "AffinityConstraintPriority",
          "value": "0"
      },
      {
          "name": "FaultDomainConstraintPriority",
          "value": "0"
      },
      {
          "name": "UpgradeDomainConstraintPriority",
          "value": "1"
      },
      {
          "name": "PreferredLocationConstraintPriority",
          "value": "2"
      }
    ]
  }
]
```

## <a name="fault-domain-and-upgrade-domain-constraints"></a>Vincoli di dominio di errore e di dominio di aggiornamento
Gestione delle risorse Cluster Hello vuole tookeep servizi distribuiti tra i domini di errore e di aggiornamento. Modella questo come un vincolo all'interno del motore di gestione risorse del Cluster di hello. Per ulteriori informazioni sulla modalità di utilizzo e il relativo comportamento specifico, l'archiviazione articolo hello [configurazione cluster](service-fabric-cluster-resource-manager-cluster-description.md#fault-and-upgrade-domain-constraints-and-resulting-behavior).

potrebbe essere necessario toopack due repliche Hello gestione delle risorse Cluster in un dominio di aggiornamento nell'ordine toodeal con gli aggiornamenti, errori o altre violazioni di vincolo. Compressione in domini di errore o l'aggiornamento è in genere si verifica solo quando sono presenti numerosi errori o altri varianza nel sistema hello impedendo posizione corretta. Se si desidera tooprevent compressione anche durante queste situazioni, è possibile usare hello `RequireDomainDistribution` [criteri di selezione](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing). Si noti che questo può influire sulla disponibilità e l'affidabilità del servizio come effetto collaterale e pertanto valutarlo attentamente.

Se l'ambiente di hello è configurato correttamente, tutti i vincoli sono completamente rispettati, anche durante gli aggiornamenti. aspetto chiave Hello è tale hello Controlla gestione delle risorse Cluster out per i vincoli. Quando rileva una violazione viene immediatamente il report e si tenta di problema hello toocorrect.

## <a name="hello-preferred-location-constraint"></a>vincolo di percorso Hello preferito
vincolo PreferredLocation Hello è leggermente diversa, perché contiene due diversi utilizzi. Un uso di questo vincolo avviene durante gli aggiornamenti dell'applicazione. Gestione delle risorse Cluster Hello gestisce automaticamente questo vincolo durante gli aggiornamenti. È utilizzato tooensure Aggiorna che quando vengono completate che repliche restituiscano tootheir posizioni iniziale. Hello altri hello PreferredLocation vincolo viene utilizzata per di hello [ `PreferredPrimaryDomain` criteri di selezione](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md). Entrambe queste sono le ottimizzazioni e pertanto hello PreferredLocation vincolo solo vincolo hello impostato troppo "Ottimizzazione" per impostazione predefinita.

## <a name="upgrades"></a>Aggiornamenti
Gestione delle risorse Cluster Hello consente inoltre di durante l'applicazione e gli aggiornamenti di cluster, durante i quali dispone di due processi:

* Verificare che le regole di hello del cluster di hello non vengano compromesse.
* Provare agevolmente go di aggiornamento hello toohelp

### <a name="keep-enforcing-hello-rules"></a>Mantenere attivate le regole di hello
Hello aspetto principale toobe comunicata è che le regole di hello vincoli strict: hello come vincoli di posizionamento e capacità - ancora vengono applicate durante gli aggiornamenti. I vincoli di posizionamento assicurano che i carichi di lavoro siano eseguiti solo dove consentito, anche durante gli aggiornamenti. Quando i servizi sono altamente vincolati, gli aggiornamenti possono richiedere più tempo. Quando il servizio di hello o è in esecuzione nel nodo di hello diventa inattivo per un aggiornamento potrebbero essere presenti alcune opzioni per cui possono accedere.

### <a name="smart-replacements"></a>Sostituzioni intelligenti
Quando viene avviato un aggiornamento, hello Gestione risorse di un'istantanea dell'accordo corrente di hello del cluster di hello. Poiché ogni dominio di aggiornamento viene completata, Cerca servizi hello tooreturn che erano in tale disposizione originale tootheir di aggiornamento del dominio. In questo modo vi sono al massimo due transizioni per un servizio durante l'aggiornamento di hello. È presente uno spostamento out del nodo interessato hello e uno riportare. Restituzione di hello toohow cluster o del servizio che prima dell'aggiornamento hello assicura anche l'aggiornamento di hello non influenzano il layout di hello del cluster di hello. 

### <a name="reduced-churn"></a>Varianza ridotta
Un altro elemento che si verifica durante l'aggiornamento è tale hello Disattiva bilanciamento del carico di gestione delle risorse Cluster. Prevenzione di bilanciamento del carico impedisce inutili effetti collaterali toohello aggiornamento stesso, ad esempio lo spostamento di servizi in nodi che sono stati svuotare per l'aggiornamento di hello. Se l'aggiornamento di hello in questione è un aggiornamento di Cluster, l'intero cluster hello non viene bilanciato durante l'aggiornamento di hello. Controlli dei vincoli rimangono attivi, lo spostamento solo in base a hello proattiva bilanciamento del carico delle metriche è disabilitato.

### <a name="buffered-capacity--upgrade"></a>Capacità in buffering e aggiornamento
In genere si desidera toocomplete aggiornamento hello anche se il cluster hello toofull vincolata o close. Gestione delle capacità di hello del cluster hello è ancora più importante durante gli aggiornamenti del normale. A seconda di hello numero di domini di aggiornamento, compreso tra 5 e 20 per cento della capacità deve essere migrata come hello aggiornamento transita in cluster hello. Tale lavoro è in qualche punto toogo. In cui questo è hello nozione di [memorizzato nel buffer capacità](service-fabric-cluster-resource-manager-cluster-description.md#buffered-capacity) è utile. Durante il normale funzionamento il buffer di capacità viene rispettato. Gestione delle risorse Cluster Hello può occupare nodi fino tootheir capacità totale (utilizzo di buffer hello) durante gli aggiornamenti, se necessario.

## <a name="next-steps"></a>Passaggi successivi
* Iniziare dall'inizio hello e [ottenere un servizio di gestione delle risorse Cluster dell'infrastruttura di toohello introduzione](service-fabric-cluster-resource-manager-introduction.md)
