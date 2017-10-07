---
title: pianificazione per le applicazioni di Service Fabric aaaCapacity | Documenti Microsoft
description: Viene descritto come tooidentify hello numero di nodi di calcolo necessarie per un'applicazione di Service Fabric
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: markfuss
editor: 
ms.assetid: 9fa47be0-50a2-4a51-84a5-20992af94bea
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 44a69e9d8ec5efcc43122dc42e8f923ef37378f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="capacity-planning-for-service-fabric-applications"></a>Pianificazione della capacità per le applicazioni Service Fabric
Questo documento illustra come tooestimate hello quantità di risorse (CPU, RAM, l'archiviazione su disco) è necessario toorun le applicazioni Azure Service Fabric. È comune per i toochange requisiti di risorse nel tempo. In genere sono necessarie poche risorse durante lo sviluppo e il test del servizio e un numero maggiore nella fase di produzione e di aumento della popolarità dell'applicazione. Quando si progetta un'applicazione, valutare i requisiti a lungo termine hello e le decisioni che consentono la richiesta di servizio tooscale toomeet cliente elevata.

 Quando si crea un cluster di Service Fabric, si decide quali tipi di macchine virtuali (VM) costituiscono cluster hello. Ogni macchina virtuale dotata di una quantità limitata di risorse nel modulo hello di CPU (Core e velocità), la larghezza di banda di rete, RAM e spazio su disco. Man mano che aumenta il servizio nel corso del tempo, è possibile aggiornare tooVMs che offrono una maggiore quantità di risorse e/o aggiungere altre macchine virtuali tooyour cluster. hello toodo quest'ultimo, è necessario progettare il servizio inizialmente in modo possibile usufruire delle nuove macchine virtuali che vengono aggiunti dinamicamente toohello cluster.

Alcuni servizi di gestiscono i pochi dati toono hello macchine virtuali. Pertanto, per questi servizi devono concentra principalmente sulle prestazioni, ovvero la selezione di hello la pianificazione della capacità appropriata CPU (Core e velocità) di macchine virtuali hello. È consigliabile valutare anche la larghezza di banda della rete, compresa la frequenza con cui si verificano trasferimenti di rete nonché la quantità dei dati trasferiti. Se il servizio deve tooperform nonché l'aumento dell'utilizzo del servizio, è possibile aggiungere altre macchine virtuali toohello cluster e il carico hello bilanciamento delle richieste di rete tra tutte le macchine virtuali hello.

Per i servizi che gestiscono su hello macchine virtuali di grandi quantità di dati, la pianificazione della capacità è consigliabile concentrarsi principalmente sulle dimensioni. Di conseguenza, è necessario valutare attentamente la capacità di hello di hello della macchina virtuale RAM e spazio su disco. sistema di gestione della memoria virtuale Hello in Windows rende lo spazio su disco RAM tooapplication codice. Inoltre, il runtime di Service Fabric hello fornisce mantenendo i dati attivi solo in memoria e lo spostamento hello dati ad accesso sporadico toodisk il paging intelligente. Le applicazioni possono pertanto utilizzare più memoria fisica disponibile su hello VM. Con una maggiore quantità di RAM sufficiente aumentano le prestazioni, poiché hello VM è possibile mantenere più spazio di archiviazione su disco nella RAM. Hello VM selezionato deve avere un dati hello toostore sufficientemente grande del disco che si desidera includere hello VM. Analogamente, hello VM deve essere sufficiente tooprovide RAM è con hello prestazioni desiderate. Se i dati del servizio aumentano nel tempo, è possibile aggiungere altre macchine virtuali toohello cluster e per partizionare dati hello in tutte le macchine virtuali hello.

## <a name="determine-how-many-nodes-you-need"></a>Determinare il numero di nodi necessari
Il servizio di partizionamento consente tooscale i dati del servizio. Per altre informazioni sul partizionamento, vedere l'articolo sul [partizionamento di Service Fabric](service-fabric-concepts-partitioning.md). Ogni partizione deve essere contenuta in una singola VM, ma è possibile posizionare più partizioni (di piccole dimensioni) in una singola VM. La presenza di un maggior numero di partizioni piccole offre maggiore flessibilità rispetto alla presenza di poche partizioni grandi. compromesso di Hello è che la presenza di un numero elevato di partizioni aumenta l'overhead di Service Fabric e non è possibile eseguire le operazioni transazionali in partizioni. È inoltre disponibile maggiore traffico di rete potenziale se il codice di servizio deve spesso tooaccess porzioni di dati che risiedono in partizioni diverse. Quando si progetta il servizio, è necessario valutare attentamente queste tooarrive i vantaggi e svantaggi in una strategia di partizionamento efficace.

Si supponga che l'applicazione dispone di un servizio con stato singolo che ha una dimensione di archivio che si prevede di toogrow tooDB_Size GB in un anno. Si è disposti tooadd altre applicazioni (e le partizioni) come si verifichi l'aumento delle dimensioni oltre tale anno.  Hello fattore di replica (RF), che determina il numero di hello di repliche per il servizio di impatto hello DB_Size totale. Hello DB_Size totale tra tutte le repliche è hello moltiplicato per DB_Size fattore di replica.  Node_Size rappresenta lo spazio su disco di hello/RAM per ogni nodo desiderato toouse per il servizio. Per prestazioni ottimali, hello DB_Size deve caricare in memoria in cluster hello e una Node_Size intorno hello RAM di hello che VM deve essere scelto. Allocando un Node_Size maggiore di hello capacità di RAM, ci si basa sul paging hello forniti dal runtime di Service Fabric hello. Di conseguenza, le prestazioni potrebbero non essere ottimali se i dati intera viene considerati toobe a caldo (poiché hello quindi paging dei dati viene eseguiti in/out). Tuttavia, per molti servizi, in cui solo una frazione di dati hello è attiva, è più conveniente.

numero di Hello di nodi necessari per le massime prestazioni può essere calcolata come segue:

```
Number of Nodes = (DB_Size * RF)/Node_Size

```


## <a name="account-for-growth"></a>Account per l'espansione
È opportuno toocompute hello numero di nodi in base hello DB_Size che si prevede inoltre il servizio toogrow, toohello DB_Size che inizia con. Quindi, aumento delle dimensioni numero hello di nodi man mano che aumenta il servizio, in modo che si è non eseguire un provisioning eccessivo numero hello di nodi. Ma hello numero di partizioni deve essere in base hello numero di nodi che sono necessari quando si esegue il servizio al massimo.

Si è buona toohave alcune macchine aggiuntive disponibili in qualsiasi momento, in modo che sia possibile gestire eventuali picchi imprevisti o negativo (ad esempio, se alcune macchine virtuali si disattivano).  Sebbene hello capacità aggiuntive deve essere determinata utilizzando i picchi previsto, un punto di partenza è tooreserve alcuni ulteriori macchine virtuali (% 5-10 aggiuntivi).

Hello precedente si presuppone che un singolo servizio informazioni sullo stato. Se si dispone di più di un servizio con stato, è necessario tooadd hello DB_Size associato hello altri servizi in equazione hello. In alternativa, è possibile calcolare il numero di hello di nodi separatamente per ogni servizio con stato.  Il servizio può includere repliche o partizioni non bilanciate. Si tenga presente che alcune partizioni potrebbero includere più dati di altre. Per altre informazioni sul partizionamento, vedere l' [articolo sulle procedure consigliate relative al partizionamento](service-fabric-concepts-partitioning.md). Tuttavia, hello precedente equazione è partizione e replica agnostico perché Service Fabric assicura che le repliche hello sono distribuite tra i nodi di hello in modo ottimizzato.

## <a name="use-a-spreadsheet-for-cost-calculation"></a>Usare un foglio di calcolo per il calcolo dei costi
Ora consente di inserire alcuni numeri reali in formula hello. Un [foglio di calcolo di esempio](https://servicefabricsdkstorage.blob.core.windows.net/publicrelease/SF%20VM%20Cost%20calculator-NEW.xlsx) viene illustrato come tooplan hello capacità per un'applicazione che contiene tre tipi di oggetti dati. Per ogni oggetto è approssimativo delle dimensioni e quanti oggetti che prevediamo toohave. Viene anche definito il numero di repliche per ogni tipo di oggetto. foglio di calcolo Hello calcola hello totale memoria toobe archiviate in cluster hello.

Viene quindi immessa una dimensione di VM e il costo mensile. In base alle dimensioni della macchina virtuale hello, foglio di calcolo hello indica che Hello numero minimo di partizioni che è necessario utilizzare toosplit adatta toophysically i dati nei nodi hello. Si potrebbe volere un numero elevato di partizioni tooaccommodate che esigenze di traffico di rete e calcolo specifico dell'applicazione. foglio di calcolo Hello Mostra il numero di hello di partizioni che gestiscono oggetti di profilo utente hello è aumentato da uno toosix.

A questo punto, in base a tutte queste informazioni, foglio di calcolo hello viene illustrato che è possibile ottenere tutti i dati di hello con hello desiderato partizioni e repliche fisicamente in un cluster di 26-nodo. Tuttavia, questo cluster potrebbe essere compresse al, pertanto è consigliabile alcuni errori di nodo tooaccommodate nodi aggiuntivi e gli aggiornamenti. foglio di calcolo Hello inoltre illustrato che con più di 57 nodi non fornisce alcun valore aggiuntivo perché è necessario che i nodi vuoti. Nuovamente, è opportuno toogo sopra 57 nodi comunque gli aggiornamenti e gli errori di nodo tooaccommodate. È possibile modificare hello foglio di calcolo toomatch esigenze specifiche dell'applicazione.   

![Foglio di calcolo per il calcolo dei costi][Image1]

## <a name="next-steps"></a>Passaggi successivi
Estrarre [servizi Service Fabric partizionamento] [ 10] toolearn ulteriori informazioni sul partizionamento del servizio.

<!--Image references-->
[Image1]: ./media/SF-Cost.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-concepts-partitioning.md
