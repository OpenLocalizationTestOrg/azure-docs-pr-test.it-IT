---
title: Data Factory di Azure con SQL Data Warehouse aaaUse | Documenti Microsoft
description: Suggerimenti per l'uso di Data factory di Azure con Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 492de762-c7a2-4cdb-943f-3135230e94f1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d40a547830f9681504253d39ae3066800a955c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a>Usare Data factory di Azure con SQL Data Warehouse
Data Factory di Azure fornisce un metodo completamente gestito per l'orchestrazione trasferimento hello dei dati e l'esecuzione di stored procedure in SQL Data Warehouse.  In questo modo si toomore facilmente installazione e pianificazione estrarre trasformazione e caricamento (ETL) procedure complesse con SQL Data Warehouse. Per una panoramica più completa di Azure Data Factory, vedere hello [documentazione di Azure Data Factory][Azure Data Factory documentation].

## <a name="data-movement"></a>Spostamento dei dati
Data factory di Azure consente lo spostamento di dati tra origini locali e diversi servizi di Azure.  In generale, corrente integrazione con Data Factory di Azure supporta tooand lo spostamento dei dati da hello posizioni seguenti:

* Archivio BLOB di Azure
* Database SQL di Azure
* Server SQL locale
* SQL Server in IaaS

Per informazioni su come attività di copia tooset backup di un tipo di dati, vedere [copiare i dati con Data Factory di Azure][Copy data with Azure Data Factory]

## <a name="stored-procedures"></a>Stored procedure
 In hello stesso modo è possibile utilizzare tooschedule trasferimento dei dati, può essere Data Factory di Azure anche essere utilizzati tooorchestrate hello esecuzione di stored procedure.  In questo modo più complesso toobe pipeline creato e si estende possibilità tooleverage hello la potenza di calcolo della Data Factory di Azure di SQL Data Warehouse.

## <a name="next-steps"></a>Passaggi successivi
Per una panoramica dell'integrazione, vedere [Panoramica dell'integrazione di SQL Data Warehouse][SQL Data Warehouse integration overview].
Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

