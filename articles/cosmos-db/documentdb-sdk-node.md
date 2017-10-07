---
title: aaaAzure Cosmos DB Node.js API, risorse e SDK | Documenti Microsoft
description: Altre informazioni sui hello Node.js API e SDK tra date di rilascio, date di ritiro e le modifiche apportate tra ogni versione di hello Azure Cosmos DB Node.js SDK.
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a>Azure Cosmos DB Node.js SDK: risorse e note sulla versione
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [Feed delle modifiche .NET](documentdb-sdk-dotnet-changefeed.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.js](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/documentdb/)
> * [Provider di risorse REST](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td>**Download dell'SDK**</td><td>[NPM](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td>**Documentazione sull'API**</td><td>[Documentazione di riferimento delle API di Node.js](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td>**Istruzioni per l'installazione dell'SDK**</td><td>[Istruzioni di installazione](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td>**Contribuiscono tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td>**Esempi**</td><td>[Esempi di codice Node.js](documentdb-nodejs-samples.md)</td></tr>

<tr><td>**esercitazione introduttiva**</td><td>[Introduzione a hello Node.js SDK](documentdb-nodejs-get-started.md)</td></tr>

<tr><td>**Esercitazione sull'app Web**</td><td>[Creare un'applicazione Web Node.js con Azure Cosmos DB](documentdb-nodejs-application.md)</td></tr>

<tr><td>**Piattaforma attualmente supportata**</td><td> 
[Node.js v6.x](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[Node.js v4.2.0](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[Node.js v0.12](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</td></tr>
</table></br>

## <a name="release-notes"></a>Note sulla versione

### <a name="1.12.2"/>1.12.2</a>
*   Correzione della documentazione di npm.

### <a name="1.12.1"/>1.12.1</a>
* Correzione di un bug in executeStoredProcedure per cui i documenti coinvolti contenevano caratteri Unicode speciali (LS, PS).
* Correzione di un bug nella gestione di documenti con i caratteri Unicode in una chiave di partizione hello.
* Supporto predefinito per la creazione di raccolte con i supporti di nome hello. Problema GitHub n. 114.
* Correzione del supporto per il token di autorizzazione. Problema GitHub n. 178.

### <a name="1.12.0"/>1.12.0</a>
* Aggiunta del supporto per nuovi [livelli di coerenza](consistency-levels.md) denominati ConsistentPrefix.
* Aggiunta del supporto per UriFactory.
* Correzione di un bug del supporto Unicode. Problema GitHub n. 171.

### <a name="1.11.0"/>1.11.0</a>
* Supporto aggiunto hello per le query di aggregazione (COUNT, MIN, MAX, SUM e AVG).
* Opzione hello aggiunto per il controllo degree of parallelism per tra query della partizione.
* Opzione hello aggiunto per disabilitare la verifica SSL durante l'esecuzione dell'emulatore di Azure Cosmos DB.
* Più basso di velocità effettiva minima per le raccolte partizionate da 10,100 UR/sec too2500 UR/sec.
* Bug token continuazione di hello predefinito per la raccolta singola partizione. Problema GitHub n. 107.
* Bug di executeStoredProcedure hello predefinito in Gestione 0 come param singolo. Problema GitHub n. 155.

### <a name="1.10.2"/>1.10.2</a>
* Versione SDK hello tooinclude intestazione agente utente predefinito.
* Pulizia del codice di minore entità.

### <a name="1.10.1"/>1.10.1</a>
* Quando si utilizza hello SDK tootarget hello emulator(hostname=localhost), disabilitare la verifica SSL.
* Aggiunta del supporto per l'abilitazione della registrazione degli script durante l'esecuzione di stored procedure.

### <a name="1.10.0"/>1.10.0</a>
* Aggiunta del supporto per le query in parallelo nelle raccolte partizionate.
* Aggiunta del supporto per le query TOP/ORDER BY nelle raccolte partizionate.

### <a name="1.9.0"/>1.9.0</a>
* Aggiunta del supporto per il criterio di ripetizione dei tentativi delle richieste limitate (le richieste limitate ricevano un'eccezione troppo grande per la frequenza delle richieste, con codice di errore 429). Per impostazione predefinita, Azure Cosmos DB Ritenta nove volte per ogni richiesta quando viene rilevato il codice di errore 429, rispettando la distinzione tra tempo retryAfter hello nell'intestazione di risposta hello. Un intervallo di tempo predefinito di tentativi ora è possibile impostare come parte di hello RetryOptions proprietà nell'oggetto ConnectionPolicy hello se si desidera che l'ora di retryAfter hello tooignore restituito dal server tra i tentativi di hello. Azure DB Cosmos ora attende per un massimo di 30 secondi per ogni richiesta che è limitata (indipendentemente dal numero di tentativi) e restituisce risposte hello con codice di errore 429. Questa volta possa anche essere sottoposto a override in hello proprietà RetryOptions ConnectionPolicy oggetto.
* COSMOS DB restituisce x-ms-limitazione--numero di tentativi e x-ms-throttle-retry-wait-time-ms come intestazioni di risposta hello in ogni velocità di richiesta toodenote hello ripetere conteggio e hello cumulativo tempo di richiesta hello attesa tra i tentativi di hello.
* classe RetryOptions Hello è stato aggiunto, esposizione hello RetryOptions proprietà sulla classe ConnectionPolicy hello che può essere utilizzati toooverride alcune predefinito hello le opzioni di ripetizione.

### <a name="1.8.0"/>1.8.0</a>
* Supporto aggiunto hello per gli account di database con più aree.

### <a name="1.7.0"/>1.7.0</a>
* Hello aggiunto il supporto per funzionalità tooLive(TTL) Time per i documenti.

### <a name="1.6.0"/>1.6.0</a>
* Implementazione delle [raccolte partizionate](partition-data.md) e dei [livelli di prestazioni definiti dall'utente](performance-levels.md).

### <a name="1.5.6"/>1.5.6</a>
* Correzione del bug RangePartitionResolver.resolveForRead in cui non restituivano i collegamenti a causa di tooa concat non valido di risultati.

### <a name="1.5.5"/>1.5.5</a>
* Corretto hashParitionResolver resolveForRead(): quando la mancata indicazione di una chiave di partizione generava un'eccezione, invece di restituire un elenco di tutti i collegamenti registrati.

### <a name="1.5.4"/>1.5.4</a>
* Consente di correggere problema [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -dedicato agente HTTPS: evitare di modificare l'agente di globale hello per scopi di Azure Cosmos DB. Utilizzare un agente dedicato per tutte le richieste del lib hello.

### <a name="1.5.3"/>1.5.3</a>
* Correzione del problema [n. 81](https://github.com/Azure/azure-documentdb-node/issues/81) : gestione corretta dei trattini negli ID dei file multimediali.

### <a name="1.5.2"/>1.5.2</a>
* Correzione del problema [n. 95](https://github.com/Azure/azure-documentdb-node/issues/95) : avviso di perdita del listener EventEmitter.

### <a name="1.5.1"/>1.5.1</a>
* Consente di correggere problema [&#92;](https://github.com/Azure/azure-documentdb-node/issues/90) -rinominare toohash Hash cartella per i sistemi tra maiuscole e minuscole.

### <a name="1.5.0"/>1.5.0</a>
* Implementazione del supporto per il partizionamento orizzontale mediante l'aggiunta di resolver della partizione a intervalli e hash.

### <a name="1.4.0"/>1.4.0</a>
* Implementazione di Upsert. Nuovi metodi upsertXXX in documentClient.

### <a name="1.3.0"/>1.3.0</a>
* Numeri di versione toobring ignorata in allineamento con altri SDK.

### <a name="1.2.2"/>1.2.2</a>
* Domande E Split promesse repository toonew wrapper.
* Aggiornare il file toopackage per npm del Registro di sistema.

### <a name="1.2.1"/>1.2.1</a>
* Implementazione del routing basato su ID
* Correzione del problema [n. 49](https://github.com/Azure/azure-documentdb-node/issues/49) : conflitto tra la proprietà current e il metodo current().

### <a name="1.2.0"/>1.2.0</a>
* Aggiunta del supporto per l'indice GeoSpatial
* Convalida la proprietà id per tutte le risorse. Gli ID per le risorse non possono contenere i caratteri ?, /, #, &#47;&#47; o terminare con uno spazio.
* Aggiunge una nuova intestazione "indice trasformazione lo stato di avanzamento" tooResourceResponse.

### <a name="1.1.0"/>1.1.0</a>
* Implementazione del criterio di indicizzazione V2.

### <a name="1.0.3"/>1.0.3</a>
* Problema [&#40;](https://github.com/Azure/azure-documentdb-node/issues/40) - implementato eslint e grunt le configurazioni di base hello e promise SDK.

### <a name="1.0.2"/>1.0.2</a>
* Problema [#45](https://github.com/Azure/azure-documentdb-node/issues/45) : il wrapper promise non include l'intestazione con errore

### <a name="1.0.1"/>1.0.1</a>
* Implementato tooquery possibilità di conflitti aggiungendo readConflicts readConflictAsync e queryConflicts.
* Aggiornamento della documentazione relativa alle API
* Problema [n. 41](https://github.com/Azure/azure-documentdb-node/issues/41) : errore client.createDocumentAsync.

### <a name="1.0.0"/>1.0.0</a>
* SDK con disponibilità generale.

## <a name="release--retirement-dates"></a>Date di rilascio e di ritiro
Microsoft fornisce una notifica almeno **12 mesi** prima di ritirare un SDK in ordine toosmooth hello transizione tooa più recente/supportata versione.

Nuove caratteristiche e funzionalità e le ottimizzazioni vengono aggiunti solo toohello corrente SDK, pertanto è consigliabile che è sempre aggiornamento toohello SDK più recente non appena possibile.

Qualsiasi richiesta tooCosmos database usando un SDK ritirato viene rifiutata dal servizio hello.

<br/>

| Versione | Data di rilascio | Data di ritiro |
| --- | --- | --- |
| [1.12.2](#1.12.2) |10 agosto 2017 |--- |
| [1.12.1](#1.12.1) |10 agosto 2017 |--- |
| [1.12.0](#1.12.0) |10 maggio 2017 |--- |
| [1.11.0](#1.11.0) |16 marzo 2017 |--- |
| [1.10.2](#1.10.2) |27 gennaio 2017 |--- |
| [1.10.1](#1.10.1) |22 dicembre 2016 |--- |
| [1.10.0](#1.10.0) |03 ottobre 2016 |--- |
| [1.9.0](#1.9.0) |07 luglio 2016 |--- |
| [1.8.0](#1.8.0) |14 giugno 2016 |--- |
| [1.7.0](#1.7.0) |26 aprile 2016 |--- |
| [1.6.0](#1.6.0) |29 marzo 2016 |--- |
| [1.5.6](#1.5.6) |08 marzo 2016 |--- |
| [1.5.5](#1.5.5) |02 febbraio 2016 |--- |
| [1.5.4](#1.5.4) |01 febbraio 2016 |--- |
| [1.5.2](#1.5.2) |26 gennaio 2016 |--- |
| [1.5.2](#1.5.2) |22 gennaio 2016 |--- |
| [1.5.1](#1.5.1) |4 gennaio 2016 |--- |
| [1.5.0](#1.5.0) |31 dicembre 2015 |--- |
| [1.4.0](#1.4.0) |06 ottobre 2015 |--- |
| [1.3.0](#1.3.0) |06 ottobre 2015 |--- |
| [1.2.2](#1.2.2) |10 settembre 2015 |--- |
| [1.2.1](#1.2.1) |15 agosto 2015 |--- |
| [1.2.0](#1.2.0) |05 agosto 2015 |--- |
| [1.1.0](#1.1.0) |09 luglio 2015 |--- |
| [1.0.3](#1.0.3) |04 giugno 2015 |--- |
| [1.0.2](#1.0.2) |23 maggio 2015 |--- |
| [1.0.1](#1.0.1) |15 maggio 2015 |--- |
| [1.0.0](#1.0.0) |08 aprile 2015 |--- |

## <a name="faq"></a>domande frequenti
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Vedere anche
toolearn ulteriori informazioni su Cosmos DB, vedere [DB di Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) pagina del servizio.

