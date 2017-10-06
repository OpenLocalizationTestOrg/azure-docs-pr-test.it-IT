---
title: Panoramica di aaaAzure SQL Database benchmark
description: Questo argomento descrive hello Azure SQL Database Benchmark utilizzato nella valutazione delle prestazioni di hello del Database SQL di Azure.
services: sql-database
documentationcenter: na
author: jan-eng
manager: jhubbard
editor: monicar
ms.assetid: e26f8a66-2c12-49d7-8297-45b4d48a5c01
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/21/2016
ms.author: janeng
ms.openlocfilehash: 1024e9ada511935f911cb1345b4dc5508997c702
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-benchmark-overview"></a>Informazioni generali sul benchmark del database SQL di Azure
## <a name="overview"></a>Panoramica
Il database SQL di Microsoft Azure offre tre [livelli di servizio](sql-database-service-tiers.md) con diversi livelli di prestazioni. Ogni livello di prestazioni fornisce un'incremento set di risorse, o 'power' progettato toodeliver aumento della velocità effettiva.

È importante toobe tooquantify in grado di come potenza crescente di hello di ogni livello di prestazioni converte in prestazioni del database maggiore. Microsoft ha sviluppato toodo hello Azure SQL Database Benchmark ASDB (). Hello esegue una combinazione di operazioni di base per trovare tutti i carichi di lavoro OLTP. Lo scopo è misurare la velocità effettiva hello raggiunta per i database in esecuzione in ogni livello di prestazioni.

Hello risorse e la potenza di ogni livello e le prestazioni del servizio sono espressi in termini di [unità transazione Database (Dtu)](sql-database-what-is-a-dtu.md). Le Dtu consentono capacità relativa di hello toodescribe di un livello di prestazioni in base a una misura combinata di CPU, memoria, leggere e scrivere tassi offerti da ogni livello di prestazioni. Raddoppiando classificazione DTU hello di un database equivale a potenza toodoubling hello. Hello benchmark consente impatto hello tooassess sulle prestazioni del database di hello l'aumento di potenza offerto da ogni livello di prestazioni eseguendo operazioni di database effettivo, durante il ridimensionamento delle dimensioni del database, il numero di utenti e velocità delle transazioni in proporzione database di toohello toohello risorse fornite.

Esprimendo la velocità effettiva hello del livello di servizio Basic hello utilizzando transazioni per ora, il livello di servizio Standard hello utilizzando transazioni al minuto e livello di servizio Premium hello utilizzo delle transazioni al secondo, rende più semplice tooquickly correlare hello potenziale di ogni requisiti toohello livello di servizio di un'applicazione.

## <a name="correlating-benchmark-results-tooreal-world-database-performance"></a>Correlazione di prestazioni del database world tooreal risultati benchmark
Importante toounderstand che ASDB, come tutti i benchmark, è rappresentativa e indicativa solo. Hello transazione velocità ottenuti con un'applicazione hello benchmark non essere hello stesso come quelle che è possibile ottenere con altre applicazioni. benchmark Hello è costituito da una raccolta di diversi tipi di transazioni eseguiti rispetto a uno schema contenente una gamma di tabelle e tipi di dati. Durante gli esercizi benchmark hello hello stesse operazioni di base che sono comuni carichi di lavoro OLTP tooall, non rappresenta una specifica classe di database o dell'applicazione. obiettivo di Hello del benchmark hello è tooprovide prestazioni relative di toohello un'indicazione ragionevole di un database che potrebbe non essere previsto in caso di ridimensionamento verso l'alto o verso il basso tra i livelli di prestazioni. Nella realtà i database hanno dimensioni e complessità diverse, gestiscono combinazioni diverse di carichi di lavoro e rispondono in modi diversi. Ad esempio, un'applicazione con un utilizzo elevato di I/O può raggiungere le soglie di I/O prima, così come un'applicazione con un utilizzo elevato di CPU può raggiungere i limiti di CPU in tempi più brevi. Non c'è garanzia che un determinato database nella stessa maniera benchmark hello in caso di aumento di carico hello.

Hello benchmark e la relativa metodologia sono descritti in dettaglio più avanti.

## <a name="benchmark-summary"></a>Riepilogo del benchmark
ASDB misura le prestazioni di hello di una combinazione di operazioni di database di base che si verificano più di frequente con carichi di lavoro (OLTP) di elaborazione delle transazioni online. Sebbene benchmark hello è progettata con il cloud computing presente, lo schema del database hello, popolamento di dati e transazioni sono stati progettati toobe su vasta scala rappresentativo di elementi di base hello più comunemente usati nei carichi di lavoro OLTP.

## <a name="schema"></a>Schema
schema di Hello è progettato toohave sufficiente toosupport varietà e la complessità di una vasta gamma di operazioni. i benchmark di Hello viene eseguito su un database costituito da sei tabelle. Hello tabelle rientrano in tre categorie: a dimensione fissa, scalabili ed espandibili. Sono presenti due tabelle a dimensione fissa, tre tabelle ridimensionabili e una tabella espandibile. Le tabelle a dimensione fissa includono un numero costante di righe. Le tabelle scalabili prevedono una cardinalità proporzionale toodatabase prestazioni, ma non viene modificato durante il benchmark hello. Hello aumento delle dimensioni di tabella viene ridimensionata di una tabella scalabile durante il caricamento iniziale, ma successivamente la cardinalità hello le modifiche nel corso di hello di esecuzione benchmark hello come inserimento e l'eliminazione delle righe.

schema Hello include una combinazione di tipi di dati, tra cui valori integer, numeric, carattere e data/ora. Hello include chiavi primarie e secondarie, ma non chiavi esterne, vale a dire, non sono presenti vincoli di integrità referenziale tra tabelle.

Un programma di generazione dati genera dati hello per il database iniziale hello. I dati integer e numeric vengono generati con diverse strategie. In alcuni casi, i valori vengono distribuiti in modo casuale su un intervallo. In altri casi, un set di valori viene permutato in modo casuale tooensure il mantenimento di una distribuzione specifica. I campi di testo vengono generati da un elenco di parole tooproduce dati realistici.

database Hello viene ridimensionato in base a un "fattore di scala". fattore di scala Hello (abbreviato SF) determina la cardinalità hello di hello tabelle scalabili ed espandibili. Come descritto di seguito hello sezione utenti e velocità, dimensioni del database hello, il numero di utenti e tutti ridimensionare in proporzione tooeach altri livelli massimi di prestazioni.

## <a name="transactions"></a>Transazioni
carico di lavoro Hello è costituito da nove tipi di transazioni, come illustrato nella tabella hello riportata di seguito. Ogni transazione è progettata toohighlight un particolare set di caratteristiche di sistema nell'hardware del sistema e del motore di database hello, con un contrasto elevato da hello altre transazioni. Questo approccio rende più semplice impatto di hello tooassess delle prestazioni toooverall diversi componenti. Transazione hello "Operazioni lettura intense" ad esempio, produce un numero significativo di operazioni di lettura dal disco.

| Tipo di transazione | Descrizione |
| --- | --- |
| Operazioni lettura leggere |SELECT, in memoria, sola lettura |
| Operazioni lettura medie |SELECT, principalmente in memoria, sola lettura |
| Operazioni lettura intense |SELECT, principalmente non in memoria, sola lettura |
| Operazioni aggiornamento leggere |UPDATE, in memoria, lettura/scrittura |
| Operazioni aggiornamento intense |UPDATE, principalmente non in memoria, lettura/scrittura |
| Operazioni inserimento leggere |INSERT, in memoria, lettura/scrittura |
| Operazioni inserimento intense |INSERT, principalmente non in memoria, lettura/scrittura |
| Eliminazione |DELETE, combinazione in memoria e non in memoria, lettura/scrittura |
| Operazioni CPU intense |SELECT, in memoria, carico CPU relativamente pesante, sola lettura |

## <a name="workload-mix"></a>Combinazione di carichi di lavoro
Le transazioni vengono selezionate casualmente da una distribuzione ponderata con hello seguente combinazione globale. Hello combinazione globale presenta un rapporto di lettura/scrittura di circa 2:1.

| Tipo di transazione | % di combinazione |
| --- | --- |
| Operazioni lettura leggere |35 |
| Operazioni lettura medie |20 |
| Operazioni lettura intense |5 |
| Operazioni aggiornamento leggere |20 |
| Operazioni aggiornamento intense |3 |
| Operazioni inserimento leggere |3 |
| Operazioni inserimento intense |2 |
| Eliminazione |2 |
| Operazioni CPU intense |10 |

## <a name="users-and-pacing"></a>Utenti e velocità
carico di lavoro benchmark Hello viene gestita da uno strumento che invia transazioni attraverso un insieme di comportamenti di hello toosimulate connessioni di un numero di utenti simultanei. Anche se tutte le transazioni e connessioni hello sono generate da un computer, per semplicità vengono indicate le connessioni toothese come "utenti". Sebbene ogni utente agisca in modo indipendente da tutti gli altri utenti, tutti gli utenti eseguono hello stesso ciclo di passaggi illustrato di seguito:

1. Stabilire una connessione di database.
2. Ripetere fino a quando tooexit segnalato:
   * Selezionare una transazione in modo casuale (da una distribuzione ponderata).
   * Eseguire la transazione selezionata hello e tempi di risposta hello misura.
   * Attendere un ritardo velocità.
3. Chiudere una connessione al database hello.
4. Uscire.

Hello ritardo velocità (nel passaggio 2c) viene selezionato in modo casuale, ma con una distribuzione che presenta una media di 1,0 secondi. Pertanto, ogni utente in media può generare al massimo una transazione al secondo.

## <a name="scaling-rules"></a>Regole di ridimensionamento
numero di Hello degli utenti è determinato dalle dimensioni di database hello (in unità di fattore di scala). Esiste un utente per ogni unità di fattore di scala. A causa di hello ritardo velocità, un utente può generare al massimo una transazione al secondo, in Media.

Ad esempio, un database con fattore di scala pari a 500 (SF=500) avrà 100 utenti e potrà raggiungere una frequenza massima di 100 TPS. toodrive soggette a TPS necessari più utenti e un database di dimensioni maggiori.

tabella Hello seguente mostra il numero di hello di utenti effettivamente supportati per ogni livello e le prestazioni del servizio.

| Livello di servizio (livello di prestazioni) | Utenti | Dimensioni database |
| --- | --- | --- |
| Basic |5 |720 MB |
| Standard (S0) |10 |1 GB |
| Standard (S1) |20 |2,1 GB |
| Standard (S2) |50 |7,1 GB |
| Premium (P1) |100 |14 GB |
| Premium (P2) |200 |28 GB |
| Premium (P6/P3) |800 |114 GB |

## <a name="measurement-duration"></a>Durata della misurazione
Per l'esecuzione di un benchmark valido è necessaria una durata della misurazione in condizioni stabili di almeno un'ora.

## <a name="metrics"></a>Metrica
le metriche principali Hello nel benchmark hello sono velocità effettiva e tempo di risposta.

* Velocità effettiva è una misurazione delle prestazioni essenziali hello nel benchmark hello. Viene misurata in transazioni per unità di tempo, conteggiando tutti i tipi di transazioni.
* Il tempo di risposta consente di misurare la prevedibilità delle prestazioni. vincolo del tempo di risposta Hello varia in base alla classe di servizio e le classi più elevate del servizio che dispone di un requisito di tempo di risposta più rigorose, come illustrato di seguito.

| Classe di servizio | Misura della velocità effettiva | Requisito di tempi di risposta |
| --- | --- | --- |
| Premium |Transazioni al secondo |95° percentile a 0,5 secondi |
| Standard |Transazioni al minuto |90° percentile a 1,0 secondi |
| Basic |Transazioni all'ora |80° percentile a 2,0 secondi |

## <a name="conclusion"></a>Conclusioni
Hello Benchmark Asdb misura le prestazioni di relativo hello del Database SQL di Azure in esecuzione diversi hello di livelli di servizio disponibili e i livelli di prestazioni. Hello esegue una combinazione di operazioni di database di base che si verificano più di frequente con carichi di lavoro (OLTP) di elaborazione delle transazioni online. Misurando le prestazioni effettive, benchmark hello fornisce una valutazione più significativa dell'impatto di hello sulla velocità effettiva dalla modifica del livello delle prestazioni hello rispetto a quello ottenibile elencando semplicemente hello risorse fornite da ogni livello, ad esempio IOPS, dimensioni della memoria e velocità della CPU . In futuro hello, verrà continuare tooevolve hello benchmark toobroaden relativo ambito ed espandere hello dati forniti.

## <a name="resources"></a>Risorse
[Introduzione tooSQL Database](sql-database-technical-overview.md)

[Livelli di servizio e livelli di prestazioni](sql-database-service-tiers.md)

[Indicazioni sulle prestazioni per database singoli](sql-database-performance-guidance.md)
