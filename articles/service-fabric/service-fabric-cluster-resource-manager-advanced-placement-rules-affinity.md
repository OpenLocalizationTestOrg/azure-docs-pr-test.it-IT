---
title: "aaaService gestione delle risorse dell'infrastruttura Cluster - affinità | Documenti Microsoft"
description: "Informazioni generali sulla configurazione dell'affinità per i servizi di Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 678073e1-d08d-46c4-a811-826e70aba6c4
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 7dc9b6d9c18d9d615d39cff7de9d7cba1c040474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-service-affinity-in-service-fabric"></a>Configurazione e utilizzo dell'affinità del servizio in Service Fabric
Affinità è un controllo che viene fornito principalmente i transizione di hello facilità di toohelp di dimensioni maggiori monolitiche applicazioni nel cloud e microservizi HelloWorld. È utilizzato anche come un'ottimizzazione per migliorare le prestazioni di hello dei servizi, anche se possono avere effetti collaterali.

Si supponga che si sta riportare un'app di dimensioni maggiori, o che non è stato progettato con microservizi presente tooService dell'infrastruttura (o qualsiasi ambiente distribuito). Questo tipo di transizione è comune. È necessario innanzitutto sollevamento hello intera app nell'ambiente di hello, creandone un pacchetto e assicurandosi che è in esecuzione senza problemi. Quindi iniziare suddividerla in diversi servizi più piccoli che tutti comunicare tooeach altri.

Infine è possibile che un'applicazione hello si è verificati alcuni problemi. problemi di Hello rientrano in genere in una di queste categorie:

1. Alcuni componenti X nell'app monolitico hello include una dipendenza non trattati nella documentazione sul componente Y, ed è attivata solo tali componenti in servizi separati. Poiché questi servizi sono in esecuzione in nodi diversi cluster hello, ma sono interrotti.
2. Questi componenti comunicano tramite (named pipes locale | il protocollo shared memory | file su disco) ed è davvero necessaria toobe toowrite in grado di tooa condiviso locale risorse per motivi di prestazioni ora. Tale dipendenza rigida viene rimossa, forse, in un secondo momento.
3. La procedura è corretta, ma si scopre che questi due componenti comunicano tra loro o sono sensibili alle prestazioni. Quando sono stati spostati in servizi separati, le prestazioni globali hanno subito dell'applicazione ne hanno risentito pesantemente o hanno aumentato la latenza. Di conseguenza, hello complessive dell'applicazione non soddisfa le aspettative dei clienti.

In questi casi, è non deve toolose del lavoro refactoring e non toogo toohello indietro monolito. ultima condizione Hello può anche essere utile come un normale di ottimizzazione. Tuttavia, fino a quando non è possibile riprogettare hello componenti toowork naturalmente come servizi (o fino a quando non è in grado di risolvere le aspettative di prestazioni hello qualche altro modo) verrà tooneed realistico di località.

Quali toodo? Si può provare ad attivare il servizio di affinità.

## <a name="how-tooconfigure-affinity"></a>Come tooconfigure affinità
tooset l'affinità, definire una relazione di affinità tra due servizi diversi. Si tratta di fare in modo che un servizio "punti" a un altro servizio affinché il primo possa essere eseguito solo se anche il secondo è in esecuzione. A volte viene fatto riferimento tooaffinity come una relazione padre/figlio (in cui si posiziona il figlio hello padre hello). Affinità assicura che le repliche hello o istanze di un servizio vengano posizionate nel hello stessi nodi di quelli di un altro servizio.

```csharp
ServiceCorrelationDescription affinityDescription = new ServiceCorrelationDescription();
affinityDescription.Scheme = ServiceCorrelationScheme.Affinity;
affinityDescription.ServiceName = new Uri("fabric:/otherApplication/parentService");
serviceDescription.Correlations.Add(affinityDescription);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

> [!NOTE]
> Un servizio figlio può partecipare solo a una relazione di affinità singola. Se si desiderava contemporaneamente hello figlio viene creata un'affinità toobe tootwo padre services sono disponibili due opzioni:
> - Hello relazioni inverse, avere parentService1 e punto di servizio figlio corrente hello parentService2, o
> - Designare una padri hello come hub per convenzione e dispongono di punti a tale servizio di tutti i servizi. 
>
> Hello risultante il comportamento di selezione host in cluster hello devono essere hello stesso.
>

## <a name="different-affinity-options"></a>Diverse opzioni di affinità
L'affinità è rappresentata tramite vari possibili schemi di correlazione e ha due modalità diverse. modalità di affinità tra i più comuni Hello è ciò che viene definito NonAlignedAffinity. In NonAlignedAffinity, hello repliche o istanze di diversi servizi hello vengono inserite in hello stessi nodi. Hello altre modalità è AlignedAffinity. La modalità AlignedAffinity viene usata solo con i servizi con stato. Configurazione con stato di due servizi toohave allineato affinità assicura che primari hello di tali servizi vengono posizionate in hello stessi nodi come ogni altro. Fa inoltre in ogni coppia di repliche secondarie per tali toobe servizi posizionato su hello stessi nodi. È inoltre possibile (anche se meno comune) tooconfigure NonAlignedAffinity per i servizi con stati. Per NonAlignedAffinity, diverse repliche di hello di due servizi con stati vengono eseguite in hello hello stessi nodi, ma i relativi componenti primari potrebbero finire in nodi diversi.

<center>
![Modalità di affinità e loro effetti][Image1]
</center>

### <a name="best-effort-desired-state"></a>Stato desiderato del massimo sforzo
Una relazione di affinità è migliore. Non fornisce hello stesse garanzie di affidabilità che stesso processo eseguibile in esecuzione in hello o la collocazione. servizi Hello in una relazione di affinità sono fondamentalmente diverse entità che può avere esito negativo ed è possibile spostare in modo indipendente. Una relazione di affinità può anche subire un'interruzione, anche se tali interruzioni sono temporanee. Ad esempio, i limiti di capacità possono significare che solo alcuni degli oggetti servizio hello nella relazione di affinità hello può contenere un nodo specifico. In questi casi, anche se è disponibile una relazione di affinità, non può essere imposta scadenza toohello altri vincoli. Se è pertanto possibile toodo, violazione hello viene corretto automaticamente in un secondo momento.

### <a name="chains-vs-stars"></a>Modelli a catena o a stella
Oggi hello gestione delle risorse Cluster non è in grado di toomodel catene di relazioni di affinità. Ciò significa che un servizio che è un elemento figlio in una relazione di affinità non potrà essere un elemento padre in un'altra relazione di affinità. Se si desidera toomodel questo tipo di relazione, in realtà hanno toomodel come una stella, anziché una catena. toomove da una stella tooa catena, hello inferiori figlio sarebbe invece toohello padre prima padre dell'elemento figlio. A seconda della disposizione hello dei servizi, è possibile toodo l'operazione più volte. Se è presente alcun elemento padre naturale di servizio, è possibile toocreate uno che funge da segnaposto. A seconda dei requisiti, è inoltre possibile toolook in [gruppi di applicazioni](service-fabric-cluster-resource-manager-application-groups.md).

<center>
![Modelli a catena o Stelle nel contesto delle relazioni affinità hello][Image2]
</center>

Un altro aspetto toonote sulle relazioni di affinità è oggi che sono direzionale. Ciò significa che tale regola affinità hello impone solo che i figli hello posizionato con padre hello. Non garantisce che padre hello Trova con figlio hello. È anche importante toonote che hello relazione di affinità non può essere ideale o immediatamente imposta poiché diversi servizi e dispone di diversi cicli di vita possono avere esito negativo e spostare in modo indipendente. Ad esempio, supponiamo padre hello improvvisamente failover tooanother nodo perché è arrestato in modo anomalo. Hello gestione delle risorse Cluster e gestione Failover handle hello failover prima di tutto, poiché mantenendo servizi hello, coerenti e disponibili priorità hello. Al termine del failover hello, relazione di affinità hello viene interrotta, ma hello tutto ciò che è appropriato fino a quando non viene individuata tale elemento figlio hello ritiene di gestione delle risorse Cluster non viene individuato con elemento padre di hello. Questi tipi di controlli vengono eseguiti periodicamente. Ulteriori informazioni su come gestore delle risorse Cluster hello valuta vincoli sono disponibile in [questo articolo](service-fabric-cluster-resource-manager-management-integration.md#constraint-types), e [questo](service-fabric-cluster-resource-manager-balancing.md) altre informazioni su come tooconfigure hello frequenza in cui questi vincoli sono valutato.   


### <a name="partitioning-support"></a>Supporto del partizionamento
Hello ultimo toonotice sull'affinità è che le relazioni di affinità non sono supportate in padre hello è partizionata. I servizi padre partizionati potrebbero essere supportati alla fine, ma attualmente non è consentito.

## <a name="next-steps"></a>Passaggi successivi
- Per altre informazioni sulla configurazione dei servizi, [Informazioni sulla configurazione dei servizi](service-fabric-cluster-resource-manager-configure-services.md)
- i servizi toolimit tooa set ridotto di computer o carico hello aggregazione dei servizi, utilizzare [gruppi di applicazioni](service-fabric-cluster-resource-manager-application-groups.md)

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resrouce-manager-affinity-modes.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resource-manager-chains-vs-stars.png