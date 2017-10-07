---
title: database cloud scalabili aaaBuilding | Documenti Microsoft
description: Compilazione di applicazioni di database scalabili .NET alla libreria client di database elastico hello
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 1f11c52d-13c1-4994-b9b1-5b1ae2f9255f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: ca34eff2078c0700dee1bc587f264bbfca979eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="building-scalable-cloud-databases"></a>Creazione di database cloud scalabili
La scalabilità orizzontale dei database può essere ottenuta facilmente con gli strumenti e le funzionalità scalabili per il database SQL di Azure. In particolare, è possibile utilizzare hello **libreria client di Database elastico** toocreate e gestire i database di scalabilità orizzontale. Questa funzionalità consente di sviluppare con facilità applicazioni partizionate usando centinaia o anche migliaia di database SQL Azure. [I processi elastici](sql-database-elastic-jobs-powershell.md) può quindi essere utilizzato toohelp semplificano la gestione di questi database.

libreria di hello tooinstall, andare troppo[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). 

## <a name="documentation"></a>Documentazione
1. [Iniziare a utilizzare gli strumenti di database elastici](sql-database-elastic-scale-get-started.md)
2. [Funzionalità di database elastico](sql-database-elastic-scale-introduction.md)
3. [Gestione mappe partizioni](sql-database-elastic-scale-shard-map-management.md)
4. [Eseguire la migrazione di database esistente tooscale-out](sql-database-elastic-convert-to-use-elastic-tools.md)
5. [Routing dipendente dei dati](sql-database-elastic-scale-data-dependent-routing.md)
6. [Query su più partizioni](sql-database-elastic-scale-multishard-querying.md)
7. [Aggiunta di una partizione utilizzando gli strumenti di database elastici](sql-database-elastic-scale-add-a-shard.md)
8. [Applicazioni multi-tenant con strumenti di database elastici e sicurezza a livello di riga](sql-database-elastic-tools-multi-tenant-row-level-security.md)
9. [Aggiornare le app della libreria client](sql-database-elastic-scale-upgrade-client-library.md) 
10. [Panoramica sulle query di database elastico](sql-database-elastic-query-overview.md)
11. [Glossario sugli strumenti di database elastici](sql-database-elastic-scale-glossary.md)
12. [Libreria client dei database elastici con Entity Framework](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md)
13. [Uso della libreria client dei database elastici con Dapper](sql-database-elastic-scale-working-with-dapper.md)
14. [Strumento di divisione-unione](sql-database-elastic-scale-overview-split-and-merge.md)
15. [Contatori delle prestazioni per Gestore mappe partizioni](sql-database-elastic-database-client-library.md) 
16. [Domande frequenti sugli strumenti di database elastici](sql-database-elastic-scale-faq.md)

## <a name="client-capabilities"></a>Funzionalità client
Scalabilità orizzontale di applicazioni utilizzando *partizionamento orizzontale* presenta difficoltà per sviluppatori di hello nonché a messaggio per l'amministratore. libreria client Hello semplifica le attività di gestione di hello fornendo strumenti che consentono sia agli sviluppatori e amministratori di gestiscono i database di scalabilità orizzontale. In un tipico esempio sono presenti numerosi database, noti come "partizioni," toomanage. I clienti sono posizionati hello stesso database ed è presente un database per ogni cliente (una combinazione di single-tenant). libreria client Hello aggiunge le funzionalità seguenti:

- **Gestione di mappa partizioni**: viene creato un database speciale denominato hello "gestore mappe partizioni". Gestione di mappa partizioni è il possibilità hello un metadati dell'applicazione toomanage sulle relative partizioni. Gli sviluppatori possono utilizzare questo database tooregister funzionalità come partizioni, vengono descritti i mapping delle chiavi di partizionamento orizzontale singoli o database toothose intervalli di chiavi e mantenere i metadati come numero hello e composizione di database si evolve tooreflect modifiche di capacità. Senza libreria client di database elastico hello, sarebbe necessario toospend molto tempo scrittura di codice di gestione di hello quando l'implementazione del partizionamento orizzontale. Per informazioni dettagliate, vedere [Gestione mappe partizioni](sql-database-elastic-scale-shard-map-management.md).

- **Routing dipendente dai dati**: immaginare una richiesta in arrivo in un'applicazione hello. Basata sul valore chiave di partizionamento orizzontale hello della richiesta di hello, un'applicazione hello deve hello toodetermine database basato sul valore della chiave hello corretto. Quindi apre una richiesta di connessione toohello database tooprocess hello. Routing dipendente dai dati consente hello tooopen connessioni con una singola chiamata semplice in una mappa partizioni hello di un'applicazione hello. Routing dipendente dai dati è un'altra area del codice dell'infrastruttura che ora è coperto dalla funzionalità nella libreria client di database elastico hello. Per informazioni dettagliate, vedere [Routing dipendente dai dati](sql-database-elastic-scale-data-dependent-routing.md).
- **Query su più partizioni**: l'esecuzione di query su più partizioni opera quando una richiesta include più partizioni o tutte le partizioni. Una query su più partizioni esegue hello stesso codice T-SQL in tutte le partizioni o un set di partizioni. risultati Hello hello che fanno parte delle partizioni vengono uniti in un risultato complessivo impostato utilizzando la semantica di UNION ALL. funzionalità esposto tramite la libreria client di hello Hello gestisce molte attività, tra cui: gestione della connessione, la gestione dei thread, la gestione degli errori e i risultati intermedi di elaborazione. MSQ possibile eseguire una query di toohundreds di partizioni. Per informazioni dettagliate, vedere [Esecuzione di query su più partizioni](sql-database-elastic-scale-multishard-querying.md).

In generale, i clienti che utilizzano gli strumenti di database elastico aspettarsi tooget funzionalità T-SQL durante l'invio di partizioni locali operazioni come operazioni partizioni toocross anziché con i propri semantica.

## <a name="next-steps"></a>Passaggi successivi
Provare a hello [app di esempio](sql-database-elastic-scale-get-started.md) che illustra le funzioni client hello. 

libreria di hello tooinstall, andare troppo[libreria Client di Database elastico](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).

Per istruzioni sull'utilizzo dello strumento di unione di menu combinato hello, vedere hello [panoramica dello strumento di unione di menu combinato](sql-database-elastic-scale-overview-split-and-merge.md).

[La libreria client dei database elastici è ora open source!](https://azure.microsoft.com/blog/elastic-database-client-library-is-now-open-sourced/)

Usare le [query del database elastico](sql-database-elastic-query-overview.md).

Hello libreria è disponibile come software open source in [GitHub](https://github.com/Azure/elastic-db-tools). 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-database-client-library/glossary.png

