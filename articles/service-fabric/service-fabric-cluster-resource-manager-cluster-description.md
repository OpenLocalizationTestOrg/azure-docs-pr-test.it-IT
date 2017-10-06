---
title: Descrizione del Cluster di gestione risorse aaaCluster | Documenti Microsoft
description: "Che descrive un cluster di Service Fabric specificando i domini di errore, domini di aggiornamento, le proprietà del nodo e le capacità dei nodi di hello gestione delle risorse Cluster."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 55f8ab37-9399-4c9a-9e6c-d2d859de6766
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f2822075976bd54402af5ad56991b5b360dfb1d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="describing-a-service-fabric-cluster"></a>Descrizione di un cluster di Service Fabric
Hello servizio di gestione delle risorse Cluster dell'infrastruttura offre diversi meccanismi per la descrizione di un cluster. Durante la fase di esecuzione, hello gestione delle risorse Cluster utilizza questa informazioni tooensure un'elevata disponibilità dei servizi di hello in esecuzione nel cluster hello. Durante l'applicazione di queste regole importanti, tenta anche l'utilizzo delle risorse hello toooptimize all'interno di cluster hello.

## <a name="key-concepts"></a>Concetti chiave
Hello gestione delle risorse Cluster supporta numerose funzioni che descrivono un cluster:

* Domini di errore
* Domini di aggiornamento
* Proprietà del nodo
* Capacità del nodo

## <a name="fault-domains"></a>Domini di errore
Un dominio di errore è un'area di errore coordinato. Un singolo computer è un dominio di errore (dal momento che può avere esito negativo nel proprio per vari motivi, dal firmware NIC power alimentatore errori toodrive errori toobad). Connesso toohello stesso commutatore Ethernet presenti hello stesso dominio di errore, come i computer sono macchine la condivisione di una singola origine di energia elettrica o in un'unica posizione. Poiché è naturale che toooverlap errori hardware, i domini di errore sono intrinsecamente gerarchici e sono rappresentati come URI di Service Fabric.

È importante che i domini di errore siano impostati correttamente poiché Service Fabric utilizza servizi di posizione toosafely questa informazioni. Service Fabric non desidera tooplace services tale perdita hello di un dominio di errore (a causa di errore hello di qualche componente) fa sì che un servizio toogo verso il basso. In ambiente Azure Service Fabric utilizza informazioni di dominio di errore hello fornite da hello ambiente toocorrectly hello configurare nodi hello hello cluster per conto dell'utente. Per il servizio Fabric autonomo, i domini di errore vengono definite in fase di hello tale cluster hello è impostato 

> [!WARNING]
> È importante che le informazioni di dominio di errore hello fornito tooService dell'infrastruttura sia corrette. Si supponga, ad esempio, che i nodi del cluster di Service Fabric siano in esecuzione all'interno di dieci macchine virtuali, a loro volta in esecuzione su cinque host fisici. In questo caso, anche se sono presenti dieci macchine virtuali, sono presenti solo cinque domini di errore diversi (livello superiore). Condivisione hello nello stesso host fisico fa sì che le macchine virtuali tooshare hello stesso dominio di errore di radice, poiché le macchine virtuali esperienza hello coordinato errore se ha esito negativo dell'host fisico.  
>
> Poiché Service Fabric prevede che il dominio di errore di un nodo non toochange hello. Altri meccanismi di garantire la disponibilità elevata di hello macchine virtuali, ad esempio [macchine virtuali a disponibilità elevata](https://technet.microsoft.com/en-us/library/cc967323.aspx), utilizzare transparent migrazione di macchine virtuali da un host tooanother. Questi meccanismi non riconfigurare o notificare hello in esecuzione di codice all'interno di hello macchina virtuale. Di conseguenza, **non sono supportati** come ambienti per l'esecuzione dei cluster di Service Fabric. Service Fabric deve essere utilizzata la tecnologia hello solo a disponibilità elevata. Non sono necessari meccanismi quali la migrazione in tempo reale della macchina virtuale, SAN, o altri. Se usati insieme a Service Fabric, questi meccanismi _riducono_ la disponibilità e l'affidabilità dell'applicazione, poiché introducono complessità aggiuntive, aggiungono origini centralizzate di errore e usano strategie di disponibilità e affidabilità che possono entrare in conflitto con quelle presenti in Service Fabric. 
>
>

Nella figura seguente hello è di colore tutte le entità hello che contribuiscono a domini tooFault ed elenco che tutti hello diversi domini di errore risultanti. In questo esempio sono presenti data center ("DC"), rack ("R") e pannelli ("B"). Ovviamente, ogni pannello contiene più di una macchina virtuale, potrebbe verificarsi un altro livello nella gerarchia di dominio di errore hello.

<center>
![Nodi organizzati tramite domini di errore][Image1]
</center>

Durante la fase di esecuzione, hello gestione delle risorse Cluster dell'infrastruttura del servizio prende in considerazione i domini di errore hello cluster hello e piani di layout. Hello repliche con state o istanze senza informazioni sullo stato per un determinato servizio vengono distribuite in modo che siano in domini di errore. Distribuzione del servizio hello tra domini di errore assicura la disponibilità di hello del servizio di hello non vengano compromessi quando si verifica un errore di un dominio di errore a qualsiasi livello della gerarchia di hello.

Gestione delle risorse dell'infrastruttura servizio Cluster non è rilevante il numero dei livelli nella gerarchia di dominio di errore hello non esistono. Tuttavia, viene effettuato tooensure che perdita hello di qualsiasi parte di una gerarchia hello di non avere alcun impatto servizi in esecuzione. 

È consigliabile se sono presenti hello stesso numero di nodi a ogni livello di profondità in hello gerarchia di dominio di errore. Se hello "struttura" di domini di errore è sbilanciato del cluster, rende più difficile per hello toofigure di gestione delle risorse Cluster out allocazione migliore di hello dei servizi. Layout di domini di errore sbilanciato significa tale perdita hello di alcuni domini disponibilità hello impatto dei servizi a più di altri domini. Di conseguenza, viene eliminata in hello gestione delle risorse Cluster tra i due obiettivi: desidera macchine hello toouse nel dominio "elevato" inserendo i servizi su di essi, e si desidera tooplace servizi negli altri domini in modo che la perdita di hello di un dominio non causa problemi. 

Come appaiono i domini sbilanciati? Nel seguente diagramma hello vengono illustrati due layout diversi cluster. Nel primo esempio hello, nodi hello vengono distribuiti uniformemente tra hello domini di errore. Nel secondo esempio hello, un dominio di errore ha molte più nodi rispetto hello altri domini di errore. 

<center>
![Due layout diversi per i cluster][Image2]
</center>

In Azure, scelta hello del quale dominio di errore contiene un nodo viene gestita. Tuttavia, in base al numero di hello di nodi che si esegue il provisioning è comunque possibile avere con domini di errore con più nodi in essi contenuti rispetto ad altri utenti. Ad esempio, si dispone di cinque domini di errore in cluster hello ma eseguire il provisioning di sette nodi per un determinato tipo di nodo. In questo caso, hello innanzitutto due domini di errore finire con più nodi. Se si continua toodeploy ulteriori NodeTypes con solo due istanze, problema hello Ottiene peggiore. Per questo motivo, è consigliabile che hello numero di nodi in ogni tipo di nodo è un multiplo del numero di hello di domini di errore.

## <a name="upgrade-domains"></a>Domini di aggiornamento
Domini di aggiornamento sono un'altra caratteristica che consente di hello servizio di gestione delle risorse Cluster dell'infrastruttura comprendere il layout di hello del cluster di hello. Domini di aggiornamento definiscono set di nodi che vengono aggiornati in hello contemporaneamente. Guida hello, gestione delle risorse Cluster comprendere e orchestrare le operazioni di gestione come gli aggiornamenti di domini di aggiornamento.

I domini di aggiornamento sono molto simili ai domini di errore, ma con un paio di differenze essenziali. Innanzitutto, i domini di errore vengono definiti da aree di errori hardware coordinati. Domini di aggiornamento, in hello invece, vengono definiti dai criteri. Viene visualizzato il numero desiderato, invece, la dettatura dall'ambiente hello toodecide. È possibile disporre dello stesso numero di domini di aggiornamento e di nodi. Un'altra differenza tra i domini di errore e i domini di aggiornamento è che questi ultimi non sono gerarchici. Sono invece più simili a un semplice tag. 

Hello diagramma seguente mostra tre che domini di aggiornamento sono suddivisi in tre domini di errore. Illustra anche una sola posizione possibile per tre repliche diverse di un servizio con stato, dove ciascuna finisce in diversi domini di errore e di aggiornamento. Questa posizione consente perdita hello di un dominio di errore in intermedio hello di un aggiornamento del servizio e ancora una copia di codice hello e i dati.  

<center>
![Posizionamento con domini di errore e di aggiornamento][Image3]
</center>

Esistono vantaggi e svantaggi toohaving un numero elevato di domini di aggiornamento. Più domini di aggiornamento significa che ogni passaggio dell'aggiornamento hello più granulare e pertanto influisce su un numero minore di nodi o servizi. Di conseguenza, i servizi meno hanno toomove contemporaneamente, introduzione meno varianza nel sistema hello. Questa impostazione tende tooimprove affidabilità, poiché è minore del servizio hello è interessato da qualsiasi problema introdotto durante l'aggiornamento di hello. Più domini di aggiornamento significa anche che è necessario meno buffer disponibile sull'impatto di hello toohandle altri nodi di hello eseguire l'aggiornamento. Ad esempio, se si dispone di cinque domini di aggiornamento, i nodi di hello in ogni gestisce circa 20% del traffico. Se è necessario tootake verso il basso tale dominio di aggiornamento per un aggiornamento, il carico deve in genere toogo in un punto. Poiché si dispone di quattro domini di aggiornamento rimanenti, ogni deve disporre di spazio per circa il 5% di traffico totale hello. Più domini di aggiornamento, che sono necessari meno buffer su nodi hello hello cluster. Si consideri, ad esempio, di disporre invece di dieci domini di aggiornamento. In tal caso, ogni UD verrebbe solo gestito circa il 10% del traffico totale hello. Quando un aggiornamento esaminato cluster hello, ogni dominio sufficiente spazio toohave per circa 1.1% del traffico totale hello. Più domini di aggiornamento consentono in genere toorun i nodi con un utilizzo superiore, poiché è necessaria una capacità riservata minore. Hello stesso vale per i domini di errore.  

svantaggio Hello di disporre di molti domini di aggiornamento è che gli aggiornamenti tendono tootake più lungo. Service Fabric attende un breve periodo di tempo dopo un aggiornamento del dominio viene completato ed esegue i controlli prima di avviare tooupgrade hello successivo. I ritardi consentono di rilevare i problemi introdotti dall'aggiornamento hello prima di avviare l'aggiornamento di hello. compromesso di Hello è accettabile in quanto impedisce le modifiche non valide di che interessano una quantità eccessiva servizio hello alla volta.

Anche l'uso di un numero troppo ridotto di domini di aggiornamento ha effetti collaterali negativi: mentre ogni singolo dominio di aggiornamento è inattivo e in fase di aggiornamento, una parte elevata della capacità complessiva non risulta disponibile. Ad esempio, se sono presenti solo tre domini di aggiornamento, 1/3 circa della capacità complessiva del servizio o del cluster non sarà disponibile in un determinato momento. Disporre moltissime operazioni del servizio verso il basso in una sola volta non è auspicabile poiché sono presenti toohave una capacità sufficiente rest hello cluster toohandle hello del carico di lavoro. Gestire quel buffer significa che durante il normale funzionamento i nodi avranno minor carico di quanto dovuto. In questo modo si aumenta il costo di hello dell'esecuzione del servizio.

Non vi è alcun limite effettivo toohello numero totale di domini di aggiornamento o di errore in un ambiente o i vincoli in modo che si sovrappongano. Ciò premesso, sono disponibili vari modelli comuni:

- Corrispondenza 1:1 fra domini di errore e domini di aggiornamento
- Un dominio di aggiornamento per nodo (istanza del sistema operativo fisico o virtuale)
- Un modello "striping" o "matrice" in domini di errore hello e domini di aggiornamento formano una matrice con computer che eseguono in genere verso il basso diagonali hello

<center>
![Layout dei domini di errore e di aggiornamento][Image4]
</center>

Non esiste che alcun meglio non risposta toochoose quali layout, ognuno presenta vantaggi e svantaggi. Ad esempio modello 1FD:1UD hello è tooset semplice. Hello dominio di aggiornamento 1 per ogni modello di nodo è più simile a quella vengono utilizzate per le persone. Durante l'aggiornamento, ogni nodo viene aggiornato in modo indipendente. Questa operazione è simile toohow piccoli set di computer sono stati aggiornati manualmente in hello precedente. 

modello più comune di Hello è una matrice di FD/UD hello, in cui hello domini di errore e domini di aggiornamento formano una tabella e i nodi vengono inseriti a partire lungo hello diagonale. Questo è il modello di hello utilizzato per impostazione predefinita nei cluster di Service Fabric in Azure. Per i cluster con molti nodi di tutti gli elementi finisce simile al modello di matrice di tipo dense hello precedente.

## <a name="fault-and-upgrade-domain-constraints-and-resulting-behavior"></a>Vincoli del dominio di errore e di aggiornamento e comportamento risultante
Gestione delle risorse Cluster Hello considera desiderio hello tookeep un servizio bilanciato tra domini di errore e l'aggiornamento come vincolo. È possibile trovare altre informazioni sui vincoli [in questo articolo](service-fabric-cluster-resource-manager-management-integration.md). Hello stato vincoli al dominio di aggiornamento e di errore: "per una partizione del servizio specificato non deve mai essere presente una differenza *maggiore di uno* numero hello degli oggetti servizio (istanze del servizio senza stato o le repliche di servizio con stato) tra due domini." Ciò impedisce determinati spostamenti o disposizioni che violano il vincolo.

Esaminiamo un esempio. Si supponga di avere un cluster con sei nodi, configurato con cinque domini di errore e cinque domini di aggiornamento.

|  | FD0 | FD1 | FD2 | FD3 | FD4 |
| --- |:---:|:---:|:---:|:---:|:---:|
| **UD0** |N1 | | | | |
| **UD1** |N6 |N2 | | | |
| **UD2** | | |N3 | | |
| **UD3** | | | |N4 | |
| **UD4** | | | | |N5 |

Si supponga ora di creare un servizio con TargetReplicaSetSize (oppure, per un servizio senza stato InstanceCount) pari a cinque. repliche Hello visualizzata N1 N5. N6 non verrà mai usato indipendentemente dal numero di servizi simili creati. Ma perché? Diamo un'occhiata differenza hello layout corrente hello e che cosa accadrebbe se si sceglie N6.

Ecco layout hello è ottenuto e hello numero massimo di repliche per ogni errore e dominio di aggiornamento:

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** |R1 | | | | |1 |
| **UD1** | |R2 | | | |1 |
| **UD2** | | |R3 | | |1 |
| **UD3** | | | |R4 | |1 |
| **UD4** | | | | |R5 |1 |
| **FDTotal** |1 |1 |1 |1 |1 |- |

Questo layout è equilibrato in termini di nodi per dominio di errore e dominio di aggiornamento. Inoltre viene bilanciato in termini di numero hello di repliche per ogni errore e di aggiornamento del dominio. Ogni dominio ha hello stesso numero di nodi e hello stesso numero di repliche.

A questo punto vediamo cosa accadrebbe se usassimo N6 invece di N2. Come repliche hello vengono distribuite quindi?

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** |R1 | | | | |1 |
| **UD1** |R5 | | | | |1 |
| **UD2** | | |R2 | | |1 |
| **UD3** | | | |R3 | |1 |
| **UD4** | | | | |R4 |1 |
| **FDTotal** |2 |0 |1 |1 |1 |- |

Questo layout viola la definizione per hello vincolo di dominio di errore. FD0 include due repliche, mentre FD1 include zero, la differenza di hello tra FD0 e FD1 un totale di due. Hello gestione delle risorse Cluster non consente tale disposizione. Allo stesso modo, se si scegliesse N2 e N6 (anziché N1 e N2) si otterrebbe:

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** | | | | | |0 |
| **UD1** |R5 |R1 | | | |2 |
| **UD2** | | |R2 | | |1 |
| **UD3** | | | |R3 | |1 |
| **UD4** | | | | |R4 |1 |
| **FDTotal** |1 |1 |1 |1 |1 |- |

Questo layout è bilanciato in termini di domini di errore. Tuttavia, ora è violano il vincolo di aggiornamento del dominio hello. Ciò avviene perché UD0 ha zero repliche mentre UD1 ne ha due. Pertanto, questo layout inoltre non è valido e non verranno utilizzato dal gestore delle risorse Cluster hello. 

## <a name="configuring-fault-and-upgrade-domains"></a>Configurazione dei domini di errore e di aggiornamento
La definizione dei domini di errore e dei domini di aggiornamento viene eseguita automaticamente nelle distribuzioni di Service Fabric ospitate in Azure. Service Fabric preleva e utilizza le informazioni sull'ambiente hello da Azure.

Se si sta creando un cluster personale (o toorun una topologia in fase di sviluppo), è possibile fornire informazioni di dominio di errore e dominio di aggiornamento hello. In questo esempio definiamo un cluster di sviluppo locale con nove nodi che si estende su tre "data center" (ognuno con tre rack). Il cluster ha anche tre domini di aggiornamento distribuiti sui tre data center. Di seguito viene riportato un esempio di configurazione hello: 

ClusterManifest.xml

```xml
  <Infrastructure>
    <!-- IsScaleMin indicates that this cluster runs on one-box /one single server -->
    <WindowsServer IsScaleMin="true">
      <NodeList>
        <Node NodeName="Node01" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType01" FaultDomain="fd:/DC01/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node02" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType02" FaultDomain="fd:/DC01/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node03" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType03" FaultDomain="fd:/DC01/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node04" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType04" FaultDomain="fd:/DC02/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node05" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType05" FaultDomain="fd:/DC02/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node06" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType06" FaultDomain="fd:/DC02/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node07" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType07" FaultDomain="fd:/DC03/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node08" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType08" FaultDomain="fd:/DC03/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node09" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType09" FaultDomain="fd:/DC03/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
      </NodeList>
    </WindowsServer>
  </Infrastructure>
```

mediante ClusterConfig.json per le distribuzioni autonome

```json
"nodes": [
  {
    "nodeName": "vm1",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm2",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm3",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm4",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm5",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm6",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm7",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm8",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm9",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD3"
  }
],
```

> [!NOTE]
> Quando si definiscono i cluster con Azure Resource Manager, Azure assegna i domini di errore e i domini di aggiornamento. Pertanto, la definizione di hello di set di scalabilità di macchine virtuali e i tipi di nodo di nel modello di gestione risorse di Azure include informazioni di aggiornamento del dominio o dominio di errore.
>

## <a name="node-properties-and-placement-constraints"></a>Proprietà dei nodi e vincoli di posizionamento
In alcuni casi (in effetti, la maggior parte del tempo di hello) sarà tooensure toowant alcuni carichi di lavoro eseguiti solo in determinati tipi di nodi nel cluster hello. Ad esempio, è possibile che alcuni carichi di lavoro richiedano GPU o SSD, mentre altri no. Un ottimo esempio di destinazione i carichi di lavoro di hardware tooparticular è quasi ogni architettura a più livelli disponibili. Alcune macchine fungono hello front-end o l'API del lato dell'applicazione hello e sono esposte toohello client o hello internet. Computer diversi, spesso con risorse hardware diverso, gestire il lavoro hello dei livelli di archiviazione o di calcolo hello. Si tratta in genere _non_ esposto direttamente tooclients o hello internet. Service Fabric è previsto che vi sono casi in cui i carichi di lavoro specifici necessario toorun sulle configurazioni hardware specifico. ad esempio:

* Un'applicazione esistente con n livelli è stata "elevata e spostata" in un ambiente Service Fabric.
* un carico di lavoro vuole toorun su hardware specifico per le prestazioni, scalabilità o motivi di isolamento di sicurezza
* Un carico di lavoro deve essere isolato da altri carichi di lavoro per motivi relativi ai criteri o all'uso delle risorse

toosupport questi tipi di configurazioni, Service Fabric è una nozione di tag che possono essere applicati toonodes prima classe. Questi tag vengono chiamati **proprietà del nodo**. **Vincoli di posizionamento** sono istruzioni hello associati servizi tooindividual selezionato per uno o più proprietà del nodo. Definiscono la posizione in cui i servizi devono essere eseguiti. Hello set di vincoli è estendibile, può utilizzare qualsiasi coppia chiave/valore. 

<center>
![Layout di cluster con carichi di lavoro diversi][Image5]
</center>

### <a name="built-in-node-properties"></a>Proprietà predefinite del nodo
Service Fabric definisce alcune proprietà di nodo predefinito che può essere utilizzato automaticamente senza utente hello toodefine con essi. le proprietà predefinite di Hello definite in ogni nodo sono hello **NodeType** hello e **NodeName**. Ad esempio è possibile scrivere un vincolo di posizionamento come `"(NodeType == NodeType03)"`. In genere sono stati rilevati NodeType toobe una delle proprietà hello comunemente utilizzato. È utile poiché ha una corrispondenza di 1:1 con un tipo di computer. Ogni tipo di computer corrisponde tooa tipo di carico di lavoro in un'applicazione a più livelli tradizionale.

<center>
![Vincoli di posizionamento e proprietà dei nodi][Image6]
</center>

## <a name="placement-constraint-and-node-property-syntax"></a>Vincoli di posizionamento e sintassi delle proprietà dei nodi 
il valore di Hello specificato nelle proprietà dei nodi hello può essere una stringa, bool, o una firma lunga. istruzione Hello servizio hello viene chiamato un posizionamento *vincolo* poiché vincola in cui è possibile eseguire il servizio di hello cluster hello. vincolo Hello può essere qualsiasi istruzione booleana che opera sulle proprietà di nodo diverso hello cluster hello. i selettori valido Hello in queste istruzioni booleane sono:

1) controlli condizionali per la creazione di istruzioni specifiche

| Istruzione | Sintassi |
| --- |:---:|
| "uguale a" | "==" |
| "diverso da" | "!=" |
| "maggiore di" | ">" |
| "maggiore o uguale a" | ">=" |
| "minore di" | "<" |
| "minore o uguale a" | "<=" |

2) istruzioni booleane per il raggruppamento e le operazioni logiche

| Istruzione | Sintassi |
| --- |:---:|
| "and" | "&&" |
| "or" | "&#124;&#124;" |
| "not" | "!" |
| "raggruppamento come singola istruzione" | "()" |

Di seguito sono riportati alcuni esempi di semplici istruzioni di vincolo.

  * `"Value >= 5"`
  * `"NodeColor != green"`
  * `"((OneProperty < 100) || ((AnotherProperty == false) && (OneProperty >= 100)))"`

Solo i nodi in cui hello complessiva posizionamento vincolo istruzione restituisce troppo "True" possono avere servizio hello posizionato su di esso. I nodi per i quali sono state definite proprietà non corrispondono ad alcun vincolo di posizionamento che contiene proprietà.

Si supponga che hello successivo nodo proprietà sono state definite per un tipo di nodo specificato:

ClusterManifest.xml

```xml
    <NodeType Name="NodeType01">
      <PlacementProperties>
        <Property Name="HasSSD" Value="true"/>
        <Property Name="NodeColor" Value="green"/>
        <Property Name="SomeProperty" Value="5"/>
      </PlacementProperties>
    </NodeType>
```

mediante ClusterConfig.json per le distribuzioni autonome o Template.json per cluster ospitati in Azure. 

> [!NOTE]
> Nel nodo hello Azure Resource Manager modello tipo è in genere con parametri. e più simile a "[parameters('vmNodeType1Name')]" che non a "NodeType01".
>

```json
"nodeTypes": [
    {
        "name": "NodeType01",
        "placementProperties": {
            "HasSSD": "true",
            "NodeColor": "green",
            "SomeProperty": "5"
        },
    }
],
```

È possibile creare *vincoli* di posizionamento del servizio per un servizio in modo analogo al seguente:

C#

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
serviceDescription.PlacementConstraints = "(HasSSD == true && SomeProperty >= 4)";
// add other required servicedescription fields
//...
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceType -Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementConstraint "HasSSD == true && SomeProperty >= 4"
```

Se tutti i nodi di NodeType01 sono validi, è possibile anche selezionare un tipo di nodo con il vincolo hello "(NodeType == NodeType01)".

Una delle operazioni più interessanti hello sui vincoli di posizionamento di un servizio è che possono essere aggiornate in modo dinamico in fase di esecuzione. Pertanto se si desidera, è possibile spostarsi di un servizio cluster hello, aggiungere e rimuovere requisiti e così via. Si occupa Service Fabric per garantire che servizio hello rimane attivo e disponibili anche quando questi tipi di modifiche vengono apportati.

C#:

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.PlacementConstraints = "NodeType == NodeType01";
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

Powershell:

```posh
Update-ServiceFabricService -Stateful -ServiceName $serviceName -PlacementConstraints "NodeType == NodeType01"
```

I vincoli di posizionamento vengono specificati per ogni istanza del servizio denominata in modo differente. Eseguire gli aggiornamenti sempre hello di (sovrascrittura) quanto specificato in precedenza.

definizione di cluster Hello definisce le proprietà di hello in un nodo. Per modificare le proprietà di un nodo è necessario un aggiornamento della configurazione del cluster. L'aggiornamento di proprietà di un nodo richiede ogni tooreport toorestart nodo interessato le nuove proprietà. Questi aggiornamenti in sequenza sono gestiti da Service Fabric.

## <a name="describing-and-managing-cluster-resources"></a>Descrizione e gestione delle risorse del cluster
Uno dei più importanti dei processi di qualsiasi orchestrator è toohelp hello gestire il consumo di risorse cluster hello. Gestione delle risorse del cluster può avere significati diversi. Innanzitutto, è necessario verificare che i computer non siano sovraccarichi, ovvero che non eseguano più servizi di quanti ne possano gestire. In secondo luogo, è bilanciamento del carico e ottimizzazione che è critico toorunning servizi in modo efficiente. Costo effettivo o prestazioni offerte di servizio riservati non possono consentire a caldo toobe alcuni nodi mentre altri sono freddi. I nodi a caldo provocare contesa tooresource riduzioni delle prestazioni e nodi freddo rappresentano sprecato e risorse aumento dei costi. 

Service Fabric rappresenta le risorse come `Metrics`. Le metriche sono qualsiasi risorsa fisica o logica che si desidera toodescribe tooService dell'infrastruttura. ad esempio "WorkQueueDepth" o "MemoryInMb". Per informazioni sulle risorse fisiche hello che può essere regolato a Service Fabric in nodi, vedere [governance delle risorse](service-fabric-resource-governance.md). Per informazioni sulla configurazione di metriche personalizzate e sul loro utilizzo, vedere [questo articolo](service-fabric-cluster-resource-manager-metrics.md)

Le metriche sono diverse dai vincoli di posizionamento e dalle proprietà del nodo. Proprietà dei nodi sono statici descrittori degli stessi nodi di hello. Le metriche descrivono le risorse di cui dispongono i nodi e che vengono consumate dai servizi quando vengono eseguiti in un nodo. Proprietà di un nodo può essere "HasSSD" ed è stato possibile impostare tootrue o false. quantità di Hello di spazio disponibile su tale unità SSD e la quantità è utilizzato da servizi sarebbe una metrica, ad esempio "DriveSpaceInMb". 

È importante toonote che esattamente come per i vincoli di posizione e le proprietà di nodo, hello gestione delle risorse Cluster dell'infrastruttura del servizio non ha capito quali nomi hello hello metriche medio. I nomi delle metriche sono semplicemente stringhe. È un'unità toodeclare buona norma come parte di nomi di metrica hello creati quando potrebbe essere ambigua.

## <a name="capacity"></a>Capacity
Se si disattiva completamente il *bilanciamento*di tutte le risorse, Cluster Resource Manager di Service Fabric tenta comunque di assicurare che nessun nodo superi la propria capacità consentita. I sovraccarichi di capacità di gestione è possibile, a meno che non cluster hello è piena o il carico di lavoro di hello è maggiore di qualsiasi nodo. Capacità è un altro *vincolo* tale gestore delle risorse Cluster hello utilizza toounderstand la quantità di una risorsa di un nodo è. La capacità residua viene registrata anche per i cluster di hello nel suo complesso. Sia la capacità di hello e utilizzo di hello a livello di servizio hello sono espressi in termini di metriche. Ad esempio, la metrica hello potrebbe essere "ClientConnections" e un determinato nodo potrebbe avere una capacità per "ClientConnections" di 32768. Gli altri nodi possono avere altri limiti di un servizio in esecuzione nel nodo possono ad esempio attualmente richiedere 32256 della metrica hello "ClientConnections".

Durante la fase di esecuzione, hello gestione delle risorse Cluster tiene traccia delle relative capacità rimanenti nel cluster hello e sui nodi. In ordine tootrack hello capacità gestione delle risorse Cluster sottrae sull'utilizzo di ciascun servizio dalla capacità del nodo in cui viene eseguito il servizio di hello. Con queste informazioni, hello servizio di gestione delle risorse Cluster dell'infrastruttura può stabilire dove tooplace o spostare le repliche in modo che i nodi non superare la capacità.

<center>
![Nodi e capacità del cluster][Image7]
</center>

C#:

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
ServiceLoadMetricDescription metric = new ServiceLoadMetricDescription();
metric.Name = "ClientConnections";
metric.PrimaryDefaultLoad = 1024;
metric.SecondaryDefaultLoad = 0;
metric.Weight = ServiceLoadMetricWeight.High;
serviceDescription.Metrics.Add(metric);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ClientConnections,High,1024,0)
```

È possibile visualizzare i valori riferiti alla capacità definita nel manifesto del cluster hello:

ClusterManifest.xml

```xml
    <NodeType Name="NodeType03">
      <Capacities>
        <Capacity Name="ClientConnections" Value="65536"/>
      </Capacities>
    </NodeType>
```

mediante ClusterConfig.json per le distribuzioni autonome o Template.json per cluster ospitati in Azure. 

```json
"nodeTypes": [
    {
        "name": "NodeType03",
        "capacities": {
            "ClientConnections": "65536",
        }
    }
],
```

In genere il carico di un servizio cambia in modo dinamico. Si supponga che il caricamento di una replica di "ClientConnections" è stato modificato da 1024 too2048, ma nodo hello è in esecuzione su quindi disponesse di 512 capacità rimanente per tale metrica. Ora il posizionamento della replica o dell'istanza non è valido, poiché in quel nodo non c'è spazio sufficiente. Gestione delle risorse Cluster Hello può tookick in e ottenere nodo hello capacità minore. Riduce il carico sul nodo hello capacità di failover mediante lo spostamento di uno o più repliche hello o istanze da tale tooother dei nodi. Quando si spostano le repliche, hello gestione delle risorse Cluster tenta costo hello toominimize di tali spostamenti di tipo. Viene descritto il costo dello spostamento in [questo articolo](service-fabric-cluster-resource-manager-movement-cost.md) più su hello gestione delle risorse Cluster di ribilanciamento strategie e le regole è descritto [qui](service-fabric-cluster-resource-manager-metrics.md).

## <a name="cluster-capacity"></a>Capacità del cluster
In che modo hello gestione delle risorse Cluster di Service Fabric keep hello complessivo del cluster da troppo piena? Con il carico dinamico non è possibile intervenire in modo netto. I servizi possono avere i picchi di carico indipendentemente dalle azioni eseguite da gestore delle risorse Cluster hello. Di conseguenza un cluster che dispone di molta capacità oggi può non essere abbastanza potente domani se l'utilizzo aumenta. Ciò premesso, esistono alcuni controlli sono ricorrere alla tooprevent problemi. innanzitutto Hello che possiamo è impedire hello creazione di nuovi carichi di lavoro che provocherebbero hello cluster toobecome completo.

Si supponga di creare un servizio senza stato al quale è associato un carico. Si supponga che il servizio hello interessare la metrica "DiskSpaceInMb" hello. Si supponga inoltre che sia continua tooconsume cinque unità del "DiskSpaceInMb" per ogni istanza del servizio hello. Si desidera toocreate tre istanze del servizio hello. L'installazione è riuscita. In modo che significa che è necessario 15 unità del toobe "DiskSpaceInMb" presenti nel cluster hello in ordine per noi tooeven essere in grado di toocreate queste istanze del servizio. Gestione delle risorse Cluster Hello calcola continuamente capacità hello e l'utilizzo di ogni metrica pertanto può determinare residua hello cluster hello. Se non vi è spazio sufficiente, gestione delle risorse Cluster Rifiuta hello hello creare chiamata del servizio.

Poiché il requisito di hello è solo che vi siano 15 unità disponibile, questo stato possibile allocare spazio molti modi diversi. Ad esempio potrebbe esserci un'unità di capacità rimanente in 15 nodi diversi oppure tre unità di capacità rimanenti in cinque nodi diversi. Se hello Gestione risorse di Cluster possibile ridisporre operazioni in modo è 5 unità disponibile in tre nodi, viene inserito il servizio di hello. La ridisposizione cluster hello è generalmente possibile, a meno che non cluster hello è quasi pieno o servizi esistenti hello non possono essere consolidati per qualche motivo.

## <a name="buffered-capacity"></a>Capacità in buffering
Capacità di memorizzazione nel buffer è un'altra funzionalità di gestione delle risorse Cluster hello. Consente di prenotazione di alcune parti del hello capacità del nodo Generale. Questo buffer di capacità è servizi tooplace utilizzato solo durante gli aggiornamenti e gli errori di nodo. La capacità in buffering è specificata a livello globale per ogni metrica e per tutti i nodi. il valore di Hello selezionato per la capacità riservata hello è una funzione del numero di hello di domini di errore e l'aggiornamento disporre nel cluster hello. Quando è presente un numero maggiore di domini di errore e di aggiornamento è possibile scegliere un valore inferiore per il buffer di capacità. Se si hanno più domini, è possibile prevedere più piccole quantità di toobe il cluster non disponibile durante gli aggiornamenti e gli errori. Specifica di capacità del buffer ha senso solo se si dispone anche di capacità del nodo hello specificato per una metrica.

Di seguito è riportato un esempio di come toospecify memorizzato nel buffer di capacità:

ClusterManifest.xml

```xml
        <Section Name="NodeBufferPercentage">
            <Parameter Name="SomeMetric" Value="0.15" />
            <Parameter Name="SomeOtherMetric" Value="0.20" />
        </Section>
```

mediante ClusterConfig.json per le distribuzioni autonome o Template.json per i cluster ospitati in Azure:

```json
"fabricSettings": [
  {
    "name": "NodeBufferPercentage",
    "parameters": [
      {
          "name": "SomeMetric",
          "value": "0.15"
      },
      {
          "name": "SomeOtherMetric",
          "value": "0.20"
      }
    ]
  }
]
```

creazione di Hello dei nuovi servizi non riesce quando cluster hello ha esaurito la capacità di memorizzazione nel buffer per una metrica. Impedire la creazione di hello di nuovo buffer di hello toopreserve services garantisce che gli errori e gli aggiornamenti non comportano nodi toogo capacità di failover. Il buffer di capacità è un'opzione facoltativa ma consigliata per tutti i cluster che definiscono una capacità per una metrica.

Gestione delle risorse Cluster Hello espone queste informazioni di carico. Per ogni metrica, le informazioni includono: 
  - Hello memorizzato nel buffer delle impostazioni di capacità
  - capacità totale Hello
  - utilizzo corrente di Hello
  - se ogni metrica può essere considerata bilanciata oppure no
  - statistiche relative a deviazione standard hello
  - nodi di Hello che hanno hello carico minimo e la maggior parte delle  
  
Di seguito un esempio dell'output:

```posh
PS C:\Users\user> Get-ServiceFabricClusterLoadInformation
LastBalancingStartTimeUtc : 9/1/2016 12:54:59 AM
LastBalancingEndTimeUtc   : 9/1/2016 12:54:59 AM
LoadMetricInformation     :
                            LoadMetricName        : Metric1
                            IsBalancedBefore      : False
                            IsBalancedAfter       : False
                            DeviationBefore       : 0.192450089729875
                            DeviationAfter        : 0.192450089729875
                            BalancingThreshold    : 1
                            Action                : NoActionNeeded
                            ActivityThreshold     : 0
                            ClusterCapacity       : 189
                            ClusterLoad           : 45
                            ClusterRemainingCapacity : 144
                            NodeBufferPercentage  : 10
                            ClusterBufferedCapacity : 170
                            ClusterRemainingBufferedCapacity : 125
                            ClusterCapacityViolation : False
                            MinNodeLoadValue      : 0
                            MinNodeLoadNodeId     : 3ea71e8e01f4b0999b121abcbf27d74d
                            MaxNodeLoadValue      : 15
                            MaxNodeLoadNodeId     : 2cc648b6770be1bc9824fa995d5b68b1
```

## <a name="next-steps"></a>Passaggi successivi
* Per informazioni sul flusso hello di architettura e le informazioni all'interno di gestione delle risorse Cluster hello, estrarre [in questo articolo](service-fabric-cluster-resource-manager-architecture.md)
* La definizione di metriche di deframmentazione in linea è tooconsolidate unidirezionale carico sui nodi anziché distribuirlo. toolearn come tooconfigure deframmentazione, fare riferimento troppo[in questo articolo](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
* Iniziare dall'inizio hello e [ottenere un servizio di gestione delle risorse Cluster dell'infrastruttura di toohello introduzione](service-fabric-cluster-resource-manager-introduction.md)
* toofind out sulla modalità di gestione delle risorse Cluster hello gestisce e bilancia il carico nel cluster hello, controllare l'articolo hello [bilanciamento del carico](service-fabric-cluster-resource-manager-balancing.md)

[Image1]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-domains.png
[Image2]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-uneven-fault-domain-layout.png
[Image3]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domains-with-placement.png
[Image4]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domain-layout-strategies.png
[Image5]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-layout-different-workloads.png
[Image6]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-placement-constraints-node-properties.png
[Image7]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-nodes-and-capacity.png
