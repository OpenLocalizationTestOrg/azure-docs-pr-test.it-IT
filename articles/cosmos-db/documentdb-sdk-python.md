---
title: aaaAzure Cosmos DB Python API, risorse e SDK | Documenti Microsoft
description: Altre informazioni sui hello Python API e SDK tra date di rilascio, date di ritiro e le modifiche apportate tra ogni versione di hello Azure Cosmos DB Python SDK.
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a>Azure Cosmos DB Python SDK: risorse e note sulla versione
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

<tr><td>**Download dell'SDK**</td><td>[PyPI](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td>**Documentazione sull'API**</td><td>[Documentazione di riferimento delle API di Python](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td>**Istruzioni per l'installazione dell'SDK**</td><td>[Istruzioni per l'installazione dell'SDK di Python](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td>**Contribuiscono tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td>**Introduzione**</td><td>[Introduzione a Python SDK hello](documentdb-python-application.md)</td></tr>

<tr><td>**Piattaforma attualmente supportata**</td><td>[Python 2.7](https://www.python.org/downloads/) e [Python 3.5](https://www.python.org/downloads/)</td></tr>
</table></br>

## <a name="release-notes"></a>Note sulla versione
### <a name="a-name220220"></a><a name="2.2.0"/>2.2.0
* Aggiunta del supporto per un nuovo livello di coerenza denominato ConsistentPrefix.


### <a name="a-name210210"></a><a name="2.1.0"/>2.1.0
* Aggiunta del supporto per le query di aggregazione (COUNT, MIN, MAX, SUM e AVG).
* Aggiunta di un'opzione per disabilitare la verifica SSL durante l'esecuzione sull'emulatore Cosmos DB.
* Rimuovere la restrizione hello di richieste dipendenti modulo toobe 2.10.0 esattamente.
* Più basso di velocità effettiva minima per le raccolte partizionate da 10,100 UR/sec too2500 UR/sec.
* Aggiunta del supporto per l'abilitazione della registrazione degli script durante l'esecuzione di stored procedure.
* Versione dell'API REST ha respinto troppo ' 2017-01-19' con questa versione.

### <a name="a-name201201"></a><a name="2.0.1"/>2.0.1
* Modifiche editoriali toodocumentation commenti.

### <a name="a-name200200"></a><a name="2.0.0"/>2.0.0
* Aggiunto il supporto per Python 3.5.
* Aggiunto il supporto per il pool di connessioni con modulo di richiesta.
* Aggiunto il supporto per la coerenza di sessione.
* Aggiunto il supporto per le query TOP/ORDERBY per le raccolte partizionate.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* Aggiunta del supporto per il criterio di ripetizione dei tentativi delle richieste limitate (le richieste limitate ricevano un'eccezione troppo grande per la frequenza delle richieste, con codice di errore 429). Per impostazione predefinita, Azure Cosmos DB Ritenta nove volte per ogni richiesta quando viene rilevato il codice di errore 429, rispettando la distinzione tra tempo retryAfter hello nell'intestazione di risposta hello. Un intervallo di tempo predefinito di tentativi ora è possibile impostare come parte di hello RetryOptions proprietà nell'oggetto ConnectionPolicy hello se si desidera che l'ora di retryAfter hello tooignore restituito dal server tra i tentativi di hello. Azure DB Cosmos ora attende per un massimo di 30 secondi per ogni richiesta che è limitata (indipendentemente dal numero di tentativi) e restituisce risposte hello con codice di errore 429. Questa fase può anche essere sottoposta a override in hello proprietà RetryOptions ConnectionPolicy oggetto.
* COSMOS DB restituisce x-ms-limitazione--numero di tentativi e x-ms-throttle-retry-wait-time-ms come intestazioni di risposta hello in ogni velocità di richiesta toodenote hello tempo di riesecuzione conteggio e hello cummulative hello richiesta di attesa tra i tentativi di hello.
* Classe RetryPolicy hello rimosso e la proprietà corrispondente hello (retry_policy) esposte nella classe document_client hello e introdotto invece una classe RetryOptions esposizione hello RetryOptions proprietà sulla classe ConnectionPolicy che può essere utilizzati toooverride alcune delle predefinito hello le opzioni di ripetizione.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Supporto aggiunto hello per gli account di database con più aree.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Hello aggiunto il supporto per funzionalità tooLive(TTL) Time per i documenti.

### <a name="a-name161161"></a><a name="1.6.1"/>1.6.1
* Correzioni di bug correlati lato tooserver partizionamento tooallow caratteri speciali nel percorso di partitionkey.

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* Implementazione delle [raccolte partizionate](partition-data.md) e dei [livelli di prestazioni definiti dall'utente](performance-levels.md). 

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Aggiungi intervallo & Hash tooassist resolver partizione con le applicazioni di partizionamento orizzontale tra più partizioni.

### <a name="a-name142142"></a><a name="1.4.2"/>1.4.2
* Implementazione di Upsert. Aggiunta di nuovi metodi di UpsertXXX toosupport Upsert funzionalità.
* Implementazione del routing basato su ID. Nessuna modifica API pubblica, tutte modifiche interne.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Supporta l'indice geospaziale.
* Convalida la proprietà id per tutte le risorse. Gli ID per le risorse non possono contenere i caratteri ?, /, #, \, o terminare con uno spazio.
* Aggiunge una nuova intestazione "indice trasformazione lo stato di avanzamento" tooResourceResponse.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Implementazione del criterio di indicizzazione V2.

### <a name="a-name101101"></a><a name="1.0.1"/>1.0.1
* Supporto della connessione proxy.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* SDK con disponibilità generale.

## <a name="release--retirement-dates"></a>Date di rilascio e di ritiro
Microsoft invierà una notifica almeno **12 mesi** prima di ritirare un SDK in ordine toosmooth hello transizione tooa più recente/supportata versione.

Nuove caratteristiche e funzionalità e le ottimizzazioni vengono aggiunti solo toohello corrente SDK, pertanto è consigliabile che è sempre aggiornamento toohello SDK più recente non appena possibile. 

Qualsiasi tooCosmos richiesta database usando un SDK ritirato verranno rifiutati dal servizio hello.

> [!WARNING]
> Tutte le versioni di hello Azure DocumentDB SDK per Python precedente tooversion **1.0.0** verrà ritirato **29 febbraio 2016**. 
> 
> 

<br/>

| Versione | Data di rilascio | Data di ritiro |
| --- | --- | --- |
| [2.2.0](#2.2.0) |10 maggio 2017 |--- |
| [2.1.0](#2.1.0) |01 maggio 2017 |--- |
| [2.0.1](#2.0.1) |30 ottobre 2016 |--- |
| [2.0.0](#2.0.0) |29 settembre 2016 |--- |
| [1.9.0](#1.9.0) |07 luglio 2016 |--- |
| [1.8.0](#1.8.0) |14 giugno 2016 |--- |
| [1.7.0](#1.7.0) |26 aprile 2016 |--- |
| [1.6.1](#1.6.1) |08 aprile 2016 |--- |
| [1.6.0](#1.6.0) |29 marzo 2016 |--- |
| [1.5.0](#1.5.0) |03 gennaio 2016 |--- |
| [1.4.2](#1.4.2) |06 ottobre 2015 |--- |
| [1.4.1](#1.4.1) |06 ottobre 2015 |--- |
| [1.2.0](#1.2.0) |06 agosto 2015 |--- |
| [1.1.0](#1.1.0) |09 luglio 2015 |--- |
| [1.0.1](#1.0.1) |25 maggio 2015 |--- |
| [1.0.0](#1.0.0) |07 aprile 2015 |--- |
| 0.9.4-prelease |14 gennaio 2015 |29 febbraio 2016 |
| 0.9.3-prelease |09 dicembre 2014 |29 febbraio 2016 |
| 0.9.2-prelease |25 novembre 2014 |29 febbraio 2016 |
| 0.9.1-prelease |23 settembre 2014 |29 febbraio 2016 |
| 0.9.0-prelease |21 agosto 2014 |29 febbraio 2016 |

## <a name="faq"></a>Domande frequenti
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Vedere anche
toolearn ulteriori informazioni su Cosmos DB, vedere [DB di Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) pagina del servizio. 

