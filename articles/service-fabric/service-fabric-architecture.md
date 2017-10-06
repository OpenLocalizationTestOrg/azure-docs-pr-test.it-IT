---
title: aaaArchitecture di Azure Service Fabric | Documenti Microsoft
description: "Service Fabric è che una piattaforma di sistemi distribuiti utilizzato toobuild scalabile, affidabile e facile da gestire le applicazioni per cloud hello. Questo articolo illustra l'architettura di hello di Service Fabric."
services: service-fabric
documentationcenter: .net
author: rishirsinha
manager: timlt
editor: rishirsinha
ms.assetid: 6b554243-70cb-4c22-9b28-1a8b4703f45e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rsinha
ms.openlocfilehash: 0268578094ad1a0010ef44ed940f828b985f6c40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-architecture"></a>Architettura di Service Fabric
Service Fabric è costituito da sottosistemi a più livelli. Tali sottosistemi consentono toowrite applicazioni che sono:

* Disponibilità elevata
* Scalabilità
* Gestione
* Testabilità

Hello seguente diagramma mostra i sottosistemi principali hello di Service Fabric.

![Diagramma dell'architettura di Service Fabric](media/service-fabric-architecture/service-fabric-architecture.png)

In un sistema distribuito, hello possibilità toosecurely la comunicazione tra nodi in un cluster è fondamentale. Base dello stack hello hello è sottosistema di trasporto hello, che fornisce una comunicazione protetta tra i nodi. Di sopra di trasporto hello sottosistema si trova il sottosistema di federazione hello, quali cluster hello nodi diversi in una singola entità (denominata cluster) in modo che Service Fabric possibile rilevare errori, eseguire elezione leader e implementare un routing coerente. il sottosistema di affidabilità Hello, ai livelli più alti il sottosistema di federazione hello, è responsabile per l'affidabilità di hello dei servizi di Service Fabric tramite meccanismi di replica, la gestione delle risorse e il failover. il sottosistema di federazione Hello sottostante anche hello hosting e attivazione sottosistema che gestisce hello del ciclo di vita di un'applicazione in un singolo nodo. il sottosistema di gestione di Hello gestisce hello del ciclo di vita delle applicazioni e servizi. sottosistema testabilità Hello consente agli sviluppatori di applicazioni provare i servizi tramite errori simulati prima e dopo la distribuzione di applicazioni e servizi ambienti tooproduction. Service Fabric consente hello tooresolve posizioni del servizio tramite il sottosistema di comunicazione. Hello i modelli di programmazione dell'applicazione esposti toodevelopers sono disposti sopra questi sottosistemi insieme a strumenti di tooenable modello applicazione hello.

## <a name="transport-subsystem"></a>Sottosistema di trasporto
il sottosistema di trasporto Hello implementa un canale di comunicazione punto a punto datagramma. Questo canale viene usato per la comunicazione tra client e i cluster di service fabric hello e la comunicazione all'interno di cluster di infrastruttura del servizio. Supporta unidirezionale e modelli di comunicazione richiesta-risposta, che prevede l'implementazione di trasmissione e multicast in base hello hello a livello di federazione. il sottosistema di trasporto Hello protegge le comunicazioni usando X509 certificati o la sicurezza di Windows. Questo sottosistema viene utilizzato internamente dall'infrastruttura di servizio e non è direttamente accessibile toodevelopers per la programmazione dell'applicazione.

## <a name="federation-subsystem"></a>Sottosistema di federazione
In ordine tooreason su un set di nodi in un sistema distribuito, è necessario toohave una visualizzazione coerente del sistema hello. il sottosistema di federazione Hello Usa primitive di comunicazione hello fornite dal sottosistema di trasporto hello e giunture hello vari nodi in un unico cluster unificato che è possibile ragionare su. Fornisce le primitive di sistemi distribuito hello necessari hello da altri sottosistemi - rilevamento degli errori, elezione leader e coerente di routing. il sottosistema di federazione Hello si basa su tabelle hash distribuita con uno spazio di token a 128 bit. sottosistema Hello crea una topologia ad anello nodi hello, con ogni anello hello allocato un subset di spazio di hello token per la proprietà del nodo. Per il rilevamento degli errori, il livello di hello utilizza un meccanismo di leasing basato su cuore elevati e arbitraggio. il sottosistema di federazione Hello garantisce anche tramite join più complessi e i protocolli di partenza che esiste solo un singolo proprietario di un token in qualsiasi momento. Ciò consente di offrire garanzie di algoritmi di elezione e routing coerenti.

## <a name="reliability-subsystem"></a>Sottosistema di affidabilità
sottosistema di affidabilità Hello fornisce hello meccanismo toomake hello lo stato di un servizio di Service Fabric a disponibilità elevata tramite l'utilizzo di hello di hello *Replicator*, *gestione Failover*, e  *Bilanciamento delle risorse*.

* Hello. Replicator assicura che le modifiche dello stato di replica del servizio primario hello saranno automaticamente replicati toosecondary repliche, mantenere la coerenza tra le repliche primarie e secondarie hello in un set di repliche del servizio. Replicatore Hello è responsabile per la gestione del quorum tra le repliche hello hello set. Interagisce con elenco hello tooget delle unità di failover di hello di operazioni tooreplicate e agente di riconfigurazione hello fornisce configurazione hello del set di repliche hello. Tale configurazione indica che le operazioni di hello repliche necessitano toobe replicati. Service Fabric fornisce un replicatore predefinito denominato Replicator dell'infrastruttura, che può essere utilizzato da hello programmazione API toomake hello servizio lo stato del modello affidabile e a disponibilità elevata.
* Hello gestione Failover assicura che quando i nodi vengono aggiunti tooor rimossa dal cluster hello, hello carico viene automaticamente ridistribuito tra i nodi disponibili hello. Se un nodo nel cluster hello non riesce, cluster hello verrà riconfigurato automaticamente la disponibilità toomaintain di repliche del servizio di hello.
* Hello Gestione risorse inserisce le repliche del servizio tra dominio di errore in cluster hello e assicura che tutte le unità di failover siano operative. Hello Gestione risorse bilancia anche le risorse del servizio tra hello sottostante pool condiviso del cluster nodi tooachieve ottimale uniforme di distribuzione del carico.

## <a name="management-subsystem"></a>Sottosistema di gestione
il sottosistema di gestione di Hello fornisce servizi end-to-end e application lifecycle management. Cmdlet di PowerShell e le API di amministrazione consentono di tooprovision, distribuiscono, patch, aggiornamenti e il deprovisioning applicazioni senza perdita di disponibilità. il sottosistema di gestione di Hello esegue questa tramite hello seguenti servizi.

* **Gestione cluster di**: si tratta di servizio primario hello che interagisce con hello gestione Failover dalle applicazioni di hello tooplace l'affidabilità nei nodi hello in base ai vincoli di posizionamento del servizio hello. Gestione risorse di Hello nel sottosistema di failover garantisce che i vincoli di hello mai interrotti. Gestione cluster di Hello gestisce hello del ciclo di vita delle applicazioni hello da toode occorre eseguire il provisioning. Si integra con hello health manager tooensure che la disponibilità dell'applicazione non verrà persa dal punto di vista semantico integrità durante gli aggiornamenti.
* **Health Manager**: questo servizio consente il monitoraggio dell'integrità di applicazioni e servizi ed entità del cluster. Entità di cluster (ad esempio nodi, servizio partizioni e repliche) può segnalare informazioni di integrità, che vengono quindi aggregate nell'archivio integrità centralizzata hello. Informazioni sull'integrità fornisce uno snapshot di integrità globale in un momento di servizi di hello e nodi distribuiti su più nodi nel cluster hello, consentendo tootake eventuali azioni correttive necessarie. Query di integrità che API consentono di eventi di integrità hello tooquery segnalato toohello sottosistema di integrità. query di integrità Hello API restituire dati di integrità non elaborati hello archiviati in integrità hello archiviano o hello aggregati, interpretare i dati di integrità per un'entità di cluster specifico.
* **Archivio immagini**: il servizio fornisce archiviazione e la distribuzione di hello file binari dell'applicazione. Questo servizio fornisce un semplice file distribuito archivio in cui le applicazioni di hello tooand caricato scaricato da.

## <a name="hosting-subsystem"></a>Sottosistema di hosting
Gestione cluster di Hello informa hello sottosistema (in esecuzione su ciascun nodo) in servizi di hosting deve toomanage per un determinato nodo. Hello hosting sottosistema quindi gestisce hello del ciclo di vita dell'applicazione hello in tale nodo. Questa utilità interagisce con hello affidabilità e integrità al tooensure di componenti che repliche hello siano posizionate correttamente e siano integri.

## <a name="communication-subsystem"></a>Sottosistema di comunicazione
Questo sottosistema fornisce la messaggistica affidabile all'interno di individuazione di cluster e il servizio hello tramite il servizio di denominazione hello. Hello Naming service risolve percorso tooa i nomi del servizio cluster hello e consente di proprietà e i nomi di servizio toomanage utenti. Usa servizio di denominazione hello, i client possono in modo sicuro comunicano con tutti i nodi hello cluster tooresolve un nome di servizio e recuperare i metadati del servizio. Utilizzando un semplice client di denominazione API, gli utenti di Service Fabric possono sviluppare servizi e client in grado di risolvere hello attuale percorso di rete nonostante Web nodo o hello modifica delle dimensioni del cluster di hello.

## <a name="testability-subsystem"></a>Sottosistema di testabilità
Il sottosistema di testabilità è costituito da strumenti progettati specificamente per il test di servizi basati su Service Fabric. Hello strumenti consentono allo sviluppatore di facilmente provoca errori significativi eseguire tooexercise scenari di test e convalidare hello numerosi Stati e transizioni che un servizio si verifica in tutta la durata, in modo controllato e sicuro. Testabilità fornisce inoltre un meccanismo toorun più test che può scorrere diversi errori possibili senza perdere la disponibilità. fornendo un ambiente di testing in produzione.

