---
title: "Testabilità: comunicazione tra servizi | Documentazione Microsoft"
description: Le comunicazioni da servizio a servizio sono un punto di integrazione critico di un'applicazione Infrastruttura di servizi. Questo articolo illustra alcune considerazioni di progettazione e tecniche di test.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 017557df-fb59-4e4a-a65d-2732f29255b8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 4a8f941c1e8e641384a9ee3a1149dabaaf9983cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-testability-scenarios-service-communication"></a>Scenari di Testabilità di Service Fabric: comunicazione tra servizi
Gli stili dell'architettura orientata ai microservizi e ai servizi vengono visualizzati naturalmente in Azure Service Fabric. In questi tipi di architetture distribuite, microservizio componenti applicazioni sono in genere composti da più servizi necessari tootalk tooeach altri. In casi più semplici anche hello, è in genere almeno un servizio web senza stato e un servizio di archiviazione di dati con stato che richiedono toocommunicate.

Comunicazione da servizio a servizio è un punto di integrazione critici di un'applicazione, perché ogni servizio espone un servizi tooother API remoto. L'uso di un set di limiti di API che coinvolgono l'I/O richiede in genere particolare attenzione e diverse operazioni di test e di convalida.

Esistono numerosi toomake considerazioni quando questi limiti di servizio sono collegati in un sistema distribuito:

* *Protocollo di trasporto*. Si userà HTTP per una maggiore interoperabilità o un protocollo binario personalizzato per la velocità effettiva massima?
* *Gestione degli errori*. Come vengono gestiti gli errori permanenti e temporanei? Cosa succede quando un servizio sposta nodo diverso tooa?
* *Timeout e latenza*. Nelle applicazioni multilivello, la modalità di ogni livello di servizio Gestione latenza attraverso l'utente di stack e toohello hello?

Se si utilizza uno dei componenti di comunicazione servizio integrato hello forniti dall'infrastruttura di servizio o si compila la propria, il test di interazioni hello tra i servizi è critico tooensuring resilienza nell'applicazione.

## <a name="prepare-for-services-toomove"></a>Preparare servizi toomove
Le istanze del servizio possono spostarsi nel tempo. Ciò vale soprattutto se vengono configurate con la metrica di caricamento per il bilanciamento delle risorse ottimizzato personalizzato. Service Fabric Sposta toomaximize di istanze del servizio alla disponibilità anche durante gli aggiornamenti, i failover, scalabilità orizzontale e altre situazioni che si verificano nel corso della durata di un sistema distribuito hello.

Come spostare i servizi cluster hello, i client e altri servizi devono essere preparata toohandle due scenari quando dibattito tooa servizio:

* replica del servizio Hello istanza o una partizione è stata spostata dall'ultima volta che è parlato tooit hello. Questa è una parte di un ciclo di vita del servizio normale e deve essere toohappen previsto nel corso della durata hello dell'applicazione.
* replica partizione o l'istanza del servizio Hello è in corso di hello dello spostamento. Anche se si verifica il failover di un servizio da un nodo tooanother molto rapidamente nell'infrastruttura del servizio, si potrebbe verificarsi un ritardo nella disponibilità se il componente di comunicazione hello del servizio è toostart lento.

La gestione normale di questi scenari è importante per garantire che il sistema funzioni senza problemi. toodo in tal caso, tenere presente che:

* Ogni servizio che può essere connesso toohas un *indirizzo* che è in ascolto (ad esempio, HTTP o WebSocket). Quando un'istanza o una partizione del servizio si sposta, il relativo endpoint dell'indirizzo cambia. (Sposta tooa nodo diverso con un indirizzo IP diverso). Se si utilizzano i componenti di comunicazione predefiniti hello, gestiscono nuovamente risoluzione indirizzi del servizio per l'utente.
* Potrebbe esserci un aumento della latenza di servizio come servizio hello istanza viene avviato il listener del temporaneo nuovamente. Dipende dal servizio hello apre rapidamente come listener hello dopo lo spostamento di istanza del servizio hello.
* Tutte le connessioni esistenti necessario toobe chiuso e riaperto dopo l'apertura di servizio hello in un nuovo nodo. Riavvio o arresto normale nodo consente di tempo per arrestare normalmente esistente toobe di connessioni.

### <a name="test-it-move-service-instances"></a>Test: spostare istanze del servizio
Tramite strumenti testabilità dell'infrastruttura servizio, è possibile creare un tootest uno scenario di test queste situazioni in modi diversi:

1. Spostare la replica primaria di un servizio con stato.
   
    Hello replica primaria di una partizione di servizio con stato può essere spostato per diversi motivi. Utilizzare questa replica primaria di hello tootarget di toosee una partizione specifica come il toohello react servizi vengono spostati in modo molto controllato.
   
    ```powershell
   
    PS > Move-ServiceFabricPrimaryReplica -PartitionId 6faa4ffa-521a-44e9-8351-dfca0f7e0466 -ServiceName fabric:/MyApplication/MyService
   
    ```
2. Arrestare un nodo.
   
    Quando un nodo viene arrestato, Service Fabric passa tutti hello service istanze o le partizioni presenti tooone tale nodo di hello altri nodi disponibili nel cluster hello. Utilizzare questa situazione in cui un nodo viene perduto dal cluster e tutte le istanze del servizio hello e delle repliche su tale nodo hanno toomove tootest.
   
    È possibile arrestare un nodo utilizzando hello PowerShell **Stop ServiceFabricNode** cmdlet:
   
    ```powershell
   
    PS > Restart-ServiceFabricNode -NodeName Node_1
   
    ```

## <a name="maintain-service-availability"></a>Mantenere la disponibilità del servizio
Come piattaforma, Service Fabric è progettato tooprovide elevata disponibilità dei servizi. In casi estremi, tuttavia, i problemi dell'infrastruttura sottostante possono comunque causare indisponibilità. È importante tootest per questi scenari, troppo.

Stato servizi utilizzano uno stato di sistema basato su quorum tooreplicate per la disponibilità elevata. Ciò significa che un quorum di repliche necessita di operazioni di scrittura toobe tooperform disponibile. In rari casi, ad esempio nel caso di errore hardware diffuso, potrebbe non essere disponibile un quorum di repliche. In questi casi, non sarà in grado di tooperform operazioni di scrittura, ma sarà comunque in grado di tooperform le operazioni di lettura.

### <a name="test-it-write-operation-unavailability"></a>Test: mancata disponibilità delle operazioni di scrittura
Tramite gli strumenti di testabilità hello nell'infrastruttura del servizio, è possibile inserire un errore che causa la perdita di quorum di un test. Sebbene tale scenario è poco frequente, è importante che i client e servizi che dipendono da un servizio con stato siano preparati toohandle situazioni in cui non sarà possibile prendere tooit le richieste di scrittura. È inoltre importante hello con stato servizio consapevole di questa possibilità che sia possano normalmente comunica toocallers.

Si può provocare perdita del quorum utilizzando hello PowerShell **Invoke ServiceFabricPartitionQuorumLoss** cmdlet:

```powershell

PS > Invoke-ServiceFabricPartitionQuorumLoss -ServiceName fabric:/Myapplication/MyService -QuorumLossMode QuorumReplicas -QuorumLossDurationInSeconds 20

```

In questo esempio viene impostato in modo `QuorumLossMode` troppo`QuorumReplicas` tooindicate da perdita del quorum tooinduce senza chiudere tutte le repliche. In questo modo è comunque possibile eseguire le operazioni di lettura. tootest uno scenario in cui un'intera partizione non è disponibile, è possibile impostare questa opzione troppo`AllReplicas`.

## <a name="next-steps"></a>Passaggi successivi
[Azioni di Testabilità](service-fabric-testability-actions.md)

[Scenari di Testabilità](service-fabric-testability-scenarios.md)

