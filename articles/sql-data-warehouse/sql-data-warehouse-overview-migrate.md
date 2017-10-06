---
title: aaaMigrate il Data Warehouse di tooSQL soluzione | Documenti Microsoft
description: Materiale sussidiario di migrazione per portare la piattaforma di soluzione tooAzure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a>Eseguire la migrazione del tooAzure soluzione SQL Data Warehouse
Che cosa comporta la migrazione di un tooAzure di soluzioni di database SQL Data Warehouse esistente, vedere. 

## <a name="profile-your-workload"></a>Profilatura del carico di lavoro
Prima della migrazione, si desidera toobe determinati che SQL Data Warehouse è una soluzione più adeguata hello per il carico di lavoro. SQL Data Warehouse è un analitica tooperform sistema distribuito progettato su dati di grandi dimensioni.  Migrazione tooSQL Data Warehouse richiede alcune modifiche di progettazione che non sono troppo difficile toounderstand ma potrebbero richiedere alcuni tooimplement ora. Se l'azienda richiede un data warehouse di classe enterprise, i vantaggi di hello si ritiene opportuno sforzo hello. Tuttavia, se non è necessario power hello di SQL Data Warehouse, è più conveniente toouse SQL Server o Database SQL di Azure.

Prendere in considerazione l'uso di SQL Data Warehouse nei casi seguenti:
- Si devono gestire uno o più terabyte di dati
- Piano toorun analitica su grandi quantità di dati
- È necessario hello archiviazione e calcolo tooscale possibilità 
- Desidera toosave costi sospendendo quando non sono necessarie risorse di calcolo.

Non usare SQL Data Warehouse per carichi di lavoro operativi (OLTP) con queste esigenze:
- Operazioni di lettura e scrittura molto frequenti
- Numeri elevati di selezioni singleton
- Volumi elevati di inserimenti di righe singole
- Elaborazioni riga per riga
- Formati non compatibili (JSON, XML)


## <a name="plan-hello-migration"></a>Migrazione del piano di hello

Dopo aver scelto toomigrate un tooSQL soluzione esistente, Data Warehouse, è importante tooplan la migrazione di hello prima di iniziare. 

Uno degli obiettivi di pianificazione è tooensure dei dati, gli schemi di tabella, e il codice sono compatibili con SQL Data Warehouse. Esistono alcuni toowork differenze compatibilità intorno tra il sistema corrente e SQL Data Warehouse. Inoltre, la migrazione di grandi quantità di dati tooAzure richiede tempo. Una pianificazione attenta consente di accelerare recupero tooAzure i dati. 

Un altro obiettivo della pianificazione è la progettazione di toomake tooensure regolazioni che la soluzione sfrutta hello prestazioni elevate delle query che SQL Data Warehouse è progettata tooprovide. Progettazione data warehouse per la scala introduce i modelli di progettazione e gli approcci tradizionali pertanto non sono sempre hello meglio. Anche se è possibile apportare alcune modifiche di progettazione dopo la migrazione, apportare modifiche prima nel processo di hello consentirà di risparmiare tempo in un secondo momento.

tooperform correttamente una migrazione, è necessario toomigrate gli schemi di tabella, il codice e i dati. Per linee guida su questi aspetti della migrazione, vedere:

-  [Eseguire la migrazione degli schemi](sql-data-warehouse-migrate-schema.md)
-  [Eseguire la migrazione del codice](sql-data-warehouse-migrate-code.md)
-  [Eseguire la migrazione dei dati](sql-data-warehouse-migrate-data.md). 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a>Passaggi successivi
Hello CAT (Customer Advisory Team) dispone anche di alcuni un'ottima guida di SQL Data Warehouse, pubblicano tramite blog.  Dare un'occhiata loro articolo [tooAzure di migrazione dei dati SQL Data Warehouse in pratica] [ Migrating data tooAzure SQL Data Warehouse in practice] per altro materiale sussidiario sulla migrazione.

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
