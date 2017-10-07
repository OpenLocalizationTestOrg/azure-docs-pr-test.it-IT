---
title: 'Azure Cosmos DB: risorse, SDK e API Java di DocumentDB | Microsoft Docs'
description: Altre informazioni sui hello Java API e SDK tra date di rilascio, date di ritiro e le modifiche apportate tra ogni versione di hello Azure SDK per Java DocumentDB DB Cosmos.
services: cosmos-db
documentationcenter: java
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 7861cadf-2a05-471a-9925-0fec0599351b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 07/11/2017
ms.author: khdang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8ef43ebeb7ae1bfc55512c4a7489c1b7930122d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a>Azure Cosmos DB: risorse e note sulla versione di DocumentDB Java SDK
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

<tr><td>**Download dell'SDK**</td><td>[Maven](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td>**Documentazione sull'API**</td><td>[Documentazione di riferimento API Java](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td>**Contribuiscono tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td>**Introduzione**</td><td>[Introduzione a hello SDK per Java](documentdb-java-get-started.md)</td></tr>

<tr><td>**Esercitazione sull'app Web**</td><td>[Sviluppo di applicazioni Web con Azure Cosmos DB](documentdb-java-application.md)</td></tr>

<tr><td>**Runtime attualmente supportato**</td><td>[JDK 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a>Note sulla versione

### <a name="a-name11201120"></a><a name="1.12.0"/>1.12.0
* Correzioni di bug importanti toorequest elaborazione durante partizione divide.
* Risolto un problema con hello sicuro e BoundedStaleness livelli di coerenza.

### <a name="a-name11101110"></a><a name="1.11.0"/>1.11.0
* Aggiunta del supporto per un nuovo livello di coerenza denominato ConsistentPrefix.
* Risolto un bug nella raccolta in modalità di sessione di lettura.

### <a name="a-name11001100"></a><a name="1.10.0"/>1.10.0
* Supporto abilitato per la raccolta partizionata con valore ridotto di 2.500 UR/s e riduzione con incrementi di 100 UR/s.
* Correzione di un bug in assembly nativo hello in alcune query possono essere NullRef eccezione.

### <a name="a-name196196"></a><a name="1.9.6"/>1.9.6
* Correzione di un bug nella configurazione del motore di query hello che può generare eccezioni per le query in modalità di Gateway.
* Corretti alcuni bug nel contenitore di sessione hello che possono generare un'eccezione "Resource proprietario non trovato" per le richieste immediatamente dopo la creazione della raccolta.

### <a name="a-name195195"></a><a name="1.9.5"/>1.9.5
* Aggiunta del supporto per le query di aggregazione (COUNT, MIN, MAX, SUM e AVG). Vedere [Supporto dell'aggregazione](documentdb-sql-query.md#Aggregates).
* Aggiunta del supporto per la modifica del feed.
* Aggiunta del supporto per informazioni sulla quota della raccolta tramite RequestOptions.setPopulateQuotaInfo.
* Aggiunta del supporto per la registrazione dello script della procedura archiviata tramite RequestOptions.setScriptLoggingEnabled.
* Risoluzione di un bug in cui una query in modalità DirectHttps rischiava di bloccarsi in presenza di errori di limitazione.
* Risoluzione di un bug in modalità di coerenza di sessione.
* Risoluzione di un bug che potrebbe causare l'eccezione NullReferenceException in HttpContext quando la frequenza delle richieste è elevata.
* Miglioramento delle prestazioni della modalità DirectHttps.

### <a name="a-name194194"></a><a name="1.9.4"/>1.9.4
* Aggiunta del supporto del proxy basato su istanza di client semplice con l'API ConnectionPolicy.setProxy().
* Aggiunta API DocumentClient.close() tooproperly arresto DocumentClient dell'istanza.
* Prestazioni migliorate di query in modalità di connettività diretta mediante derivazione hello piano di query da un assembly nativo hello anziché hello Gateway.
* Impostare FAIL_ON_UNKNOWN_PROPERTIES = false, in modo che gli utenti non devono toodefine JsonIgnoreProperties nella loro POJO.
* Sottoposta a refactoring registrazione toouse SLF4J.
* Risoluzione di altri bug nel lettore di coerenza.

### <a name="a-name193193"></a><a name="1.9.3"/>1.9.3
* Correzione di un bug in hello connessione gestione tooprevent perdite di connessione in modalità di connettività diretta.
* Correzione di un bug nella query TOP hello in cui è possibile eccezione NullReferenece.
* Miglioramento delle prestazioni, riducendo il numero di hello di chiamata di rete per la cache interna di hello.
* Aggiunta del codice di stato, di ActivityID e dell'URI della richiesta in DocumentClientException per una migliore risoluzione dei problemi.

### <a name="a-name192192"></a><a name="1.9.2"/>1.9.2
* Risolto un problema nella gestione connessione hello per la stabilità.

### <a name="a-name191191"></a><a name="1.9.1"/>1.9.1
* Aggiunta del supporto per il livello di coerenza BoundedStaleness.
* Aggiunta del supporto per la connettività diretta per le operazioni CRUD delle raccolte partizionate.
* Risoluzione di un bug in una query di un database con SQL.
* Correzione di un bug nella cache di hello sessione in cui i token di sessione può essere impostato in modo non corretto.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* Aggiunta del supporto per le query in parallelo nelle raccolte partizionate.
* Aggiunta del supporto per le query TOP/ORDER BY nelle raccolte partizionate.
* Aggiunta del supporto per la coerenza assoluta.
* Aggiunta del supporto per le richieste basate su nomi quando si utilizza la connettività diretta.
* Toomake fisso ActivityId rimangono coerenti tra tutti i tentativi di richiesta.
* Correzione di un bug relativi toohello cache della sessione durante la ricreazione di una raccolta con hello stesso nome.
* Aggiunta Polygon e LineString DataTypes quando si specifica il criterio di indicizzazione per la raccolta criteri per le query spaziali di geo-fencing.
* Risoluzione dei problemi con Java Doc per Java 1.8.

### <a name="a-name181181"></a><a name="1.8.1"/>1.8.1
* Correzione di un bug in PartitionKeyDefinitionMap toocache raccolte con partizione singola e non crea aggiuntivo recuperare partizione richieste di chiavi.
* Correzione di un nuovo tentativo toonot bug quando viene fornito un valore di chiave di partizione corretto.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Supporto aggiunto hello per gli account di database con più aree.
* Aggiunta del supporto per la ripetizione automatica per le richieste limitate con hello toocustomize opzioni max tentativi e ripetere max tempo di attesa.  Vedere RetryOptions e ConnectionPolicy.getRetryOptions().
* IPartitionResolver basato su codice di partizionamento personalizzato è stato deprecato. Usare le raccolte partizionate per un'archiviazione e una velocità effettiva superiori.

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
* Aggiunta del supporto per il criterio di ripetizione per la limitazione.  

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Aggiunto il supporto di (durata TTL) toolive di tempo per i documenti.

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* Implementazione delle [raccolte partizionate](partition-data.md) e dei [livelli di prestazioni definiti dall'utente](performance-levels.md).

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1
* Correzione di un bug in valori di hash toogenerate HashPartitionResolver in toobe little-endian coerente con altri SDK.

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Aggiungi intervallo & Hash tooassist resolver partizione con le applicazioni di partizionamento orizzontale tra più partizioni.

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0
* Implementazione di Upsert. Aggiunta di nuovi metodi di upsertXXX toosupport Upsert funzionalità.
* Implementazione del routing basato su ID. Nessuna modifica API pubblica, tutte modifiche interne.

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0
* Versione ignorato il numero di versione toobring in allineamento con altri SDK

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Supporta l'indice geospaziale
* Convalida la proprietà id per tutte le risorse. Gli ID per le risorse non possono contenere i caratteri ?, /, #, \, o terminare con uno spazio.
* Aggiunge una nuova intestazione "indice trasformazione lo stato di avanzamento" tooResourceResponse.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Implementa criteri di indicizzazione V2

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* SDK con disponibilità generale

## <a name="release--retirement-dates"></a>Date di rilascio e di ritiro
Microsoft invierà una notifica almeno **12 mesi** prima di ritirare un SDK in ordine toosmooth hello transizione tooa più recente/supportata versione.

Nuove caratteristiche e funzionalità e le ottimizzazioni vengono aggiunti solo toohello corrente SDK, pertanto è consigliabile che è sempre aggiornamento toohello SDK più recente non appena possibile.

Qualsiasi tooCosmos richiesta database usando un SDK ritirato verranno rifiutati dal servizio hello.

> [!WARNING]
> Tutte le versioni di hello DocumentDB SDK per Java precedente tooversion **1.0.0** verrà ritirato **29 febbraio 2016**.
> 
> 

<br/>

| Versione | Data di rilascio | Data di ritiro |
| --- | --- | --- |
| [1.12.0](#1.12.0) |11 luglio 2017 |--- |
| [1.11.0](#1.11.0) |10 maggio 2017 |--- |
| [1.10.0](#1.10.0) |11 marzo 2017 |--- |
| [1.9.6](#1.9.6) |21 febbraio 2017 |--- |
| [1.9.5](#1.9.5) |31 gennaio 2017 |--- |
| [1.9.4](#1.9.4) |24 novembre 2016 |--- |
| [1.9.3](#1.9.3) |30 ottobre 2016 |--- |
| [1.9.2](#1.9.2) |28 ottobre 2016 |--- |
| [1.9.1](#1.9.1) |26 ottobre 2016 |--- |
| [1.9.0](#1.9.0) |03 ottobre 2016 |--- |
| [1.8.1](#1.8.1) |30 giugno 2016 |--- |
| [1.8.0](#1.8.0) |14 giugno 2016 |--- |
| [1.7.1](#1.7.1) |30 aprile 2016 |--- |
| [1.7.0](#1.7.0) |27 aprile 2016 |--- |
| [1.6.0](#1.6.0) |29 marzo 2016 |--- |
| [1.5.1](#1.5.1) |31 dicembre 2015 |--- |
| [1.5.0](#1.5.0) |04 dicembre 2015 |--- |
| [1.4.0](#1.4.0) |05 ottobre 2015 |--- |
| [1.3.0](#1.3.0) |05 ottobre 2015 |--- |
| [1.2.0](#1.2.0) |05 agosto 2015 |--- |
| [1.1.0](#1.1.0) |09 luglio 2015 |--- |
| [1.0.1](#1.0.1) |12 maggio 2015 |--- |
| [1.0.0](#1.0.0) |07 aprile 2015 |--- |
| 0.9.5-prelease |09 marzo 2015 |29 febbraio 2016 |
| 0.9.4-prelease |17 febbraio 2015 |29 febbraio 2016 |
| 0.9.3-prelease |13 gennaio 2015 |29 febbraio 2016 |
| 0.9.2-prelease |19 dicembre 2014 |29 febbraio 2016 |
| 0.9.1-prelease |19 dicembre 2014 |29 febbraio 2016 |
| 0.9.0-prelease |10 dicembre 2014 |29 febbraio 2016 |

## <a name="faq"></a>Domande frequenti
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Vedere anche
toolearn ulteriori informazioni su Cosmos DB, vedere [DB di Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) pagina del servizio.

