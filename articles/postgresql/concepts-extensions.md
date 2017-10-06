---
title: estensioni PostgreSQL aaaUsing nel Database di Azure per PostgreSQL | Documenti Microsoft
description: "Viene descritta hello possibilità tooextend hello funzionalità del database utilizzando le estensioni nel Database di Azure per PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/29/2017
ms.openlocfilehash: af2462d7a923b934bc0329153be7079ba86e8856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="postgresql-extensions-in-azure-database-for-postgresql"></a>Estensioni di PostgreSQL nel database di Azure per PostgreSQL
PostgreSQL fornisce funzionalità di hello possibilità tooextend hello del database utilizzando le estensioni. Le estensioni consentono più toobe oggetti SQL correlate collegate tra loro in un singolo pacchetto e possono essere caricate o rimosso dal database con un unico comando. Estensioni una volta caricate nel database di hello come funzionalità incorporate in grado di funzionare. Per altre informazioni sulle estensioni di PostgreSQL, vedere [Packaging Related Objects into an Extension](https://www.postgresql.org/docs/9.6/static/extend-extensions.html) (Creare un pacchetto di oggetti correlati formando un'estensione).

## <a name="how-toouse-postgresql-extensions"></a>Come toouse PostgreSQL estensioni?
Estensioni PostgreSQL necessario toobe installato per il database prima di utilizzarli. tooinstall una particolare estensione, eseguire il [creazione estensione](https://www.postgresql.org/docs/9.6/static/sql-createextension.html) comando tooload strumento psql hello oggetti nel pacchetto nel database.

Il database di Azure per PostgreSQL supporta un subset delle estensioni chiave come indicato di seguito. Oltre a quelli elencati di hello, non sono supportate altre estensioni. È possibile creare estensioni personalizzate con il database di Azure per il servizio PostgreSQL.

## <a name="extensions-supported-by-azure-database-for-postgresql"></a>Estensioni supportate dal database di Azure per PostgreSQL
nelle tabelle seguenti Hello sono elenco hello PostgreSQL estensioni standard che sono attualmente supportate dal Database di Azure per PostgreSQL. È possibile ottenere queste informazioni anche eseguendo una query con pg\_available\_extensions. 

### <a name="data-types-extensions"></a>Estensioni di tipi di dati

> [!div class="mx-tableFixed"]
| **Estensione** | **Descrizione** |
|---|---|
| [citext](https://www.postgresql.org/docs/9.6/static/citext.html) | Fornisce un tipo stringa di caratteri che non distingue fra maiuscole e minuscole |
| [hstore](https://www.postgresql.org/docs/9.6/static/hstore.html) | Fornisce il tipo di dati per l'archiviazione dei set di coppie chiave/valore |

### <a name="functions-extensions"></a>Estensioni di funzioni

> [!div class="mx-tableFixed"]
| **Estensione** | **Descrizione** |
|---|---|
| [fuzzystrmatch](https://www.postgresql.org/docs/9.6/static/fuzzystrmatch.html) | Fornisce diverse analogie toodetermine funzioni e distanza tra stringhe. |
| [intarray](https://www.postgresql.org/docs/9.6/static/intarray.html) | Fornisce funzioni e operatori per la manipolazione delle matrici di interi senza null. |
| [pgcrypto](https://www.postgresql.org/docs/9.6/static/pgcrypto.html) | Fornisce funzioni di crittografia |
| [pg\_partman](https://pgxn.org/dist/pg_partman/doc/pg_partman.html) | Gestisce le tabelle partizionate per ora o ID |
| [pg\_trgm](https://www.postgresql.org/docs/9.6/static/pgtrgm.html) | Fornisce le funzioni e operatori per determinare la somiglianza di hello del testo alfanumerico in base alla corrispondenza di trigramma |
| [uuid-ossp](https://www.postgresql.org/docs/9.6/static/uuid-ossp.html) | Generare identificatori universalmente univoci (UUID) |

### <a name="full-text-search-extensions"></a>Estensioni di ricerca full-text

> [!div class="mx-tableFixed"]
| **Estensione** | **Descrizione** |
|---|---|
| [unaccent](https://www.postgresql.org/docs/9.6/static/unaccent.html) | Un dizionario di ricerca di testo che rimuove gli accenti (segni diacritici) dai lessemi. |

### <a name="index-types-extensions"></a>Estensioni di tipi di indice

> [!div class="mx-tableFixed"]
| **Estensione** | **Descrizione** |
|---|---|
| [btree\_gin](https://www.postgresql.org/docs/9.6/static/btree-gin.html) | Fornisce classi operatore GIN di esempio che implementano un comportamento simile alla struttura b-tree per determinati tipi di dati. |
| [btree\_gist](https://www.postgresql.org/docs/9.6/static/btree-gist.html) | Fornisce classi operatore indice GiST che implementano la struttura b-tree. |

### <a name="language-extensions"></a>Estensioni di linguaggio

> [!div class="mx-tableFixed"]
| **Estensione** | **Descrizione** |
|---|---|
| [plpgsql](https://www.postgresql.org/docs/9.6/static/plpgsql.html) | Linguaggio procedurale caricabile PL/pgSQL |

### <a name="miscellaneous-extensions"></a>Estensioni varie

> [!div class="mx-tableFixed"]
| **Estensione** | **Descrizione** |
|---|---|
| [pg\_buffercache](https://www.postgresql.org/docs/9.6/static/pgbuffercache.html) | Fornisce un mezzo per l'esame di ciò che avviene nella cache buffer condiviso hello in tempo reale. |
| [pg\_prewarm](https://www.postgresql.org/docs/9.6/static/pgprewarm.html) | Fornisce dati di relazione tooload un modo nella cache buffer hello. |
| [pg\_stat\_statements](https://www.postgresql.org/docs/9.6/static/pgstatstatements.html) | Fornisce un modo per tenere traccia delle statistiche di esecuzione di tutte le istruzioni SQL eseguite da un server. |
| [postgres\_fdw](https://www.postgresql.org/docs/9.6/static/postgres-fdw.html) | Wrapper di dati esterno utilizzato tooaccess dati archiviati nel server PostgreSQL esterni |

### <a name="postgis"></a>PostGIS

> [!div class="mx-tableFixed"]
| **Estensione** | **Descrizione** |
|---|---|
| [PostGIS](http://www.postgis.net/), postgis\_topology, postgis\_tiger\_geocoder, postgis\_sfcgal | Oggetti spaziali e geografici per PostgreSQL. |
| address\_standardizer, address\_standardizer\_data\_us | Tooparse usato un indirizzo in elementi costitutivi. Utilizzare passaggio di normalizzazione toosupport geocodifica indirizzo. |
| [pgrouting](http://pgrouting.org/) | Estende hello PostGIS / PostgreSQL geospatial database tooprovide geospatial funzionalità di routing. |

## <a name="next-steps"></a>Passaggi successivi
Non è presente un'estensione che si desidera toouse? È possibile comunicarlo. Votare per le richieste esistenti o creare nuovi commenti e richieste nel [forum dei commenti di clienti](https://feedback.azure.com/forums/597976-azure-database-for-postgresql).
