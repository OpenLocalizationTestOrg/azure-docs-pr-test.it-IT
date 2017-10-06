---
title: i client di Data Warehouse aaaSQL supportano per il controllo dati | Documenti Microsoft
description: Informazioni sul supporto di client di livello inferiore di SQL Data Warehouse per il controllo dati
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: dfe29ff3-dfeb-4309-83c0-c1a300f4f44e
ms.service: sql-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 377488680eb297c3e9b1dc754c003c5b19b47996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a>SQL Data Warehouse - Supporto client di livello inferiore per controllo e maschera dati dinamica
[Controllo](sql-data-warehouse-auditing-overview.md) funziona con i client SQL che supportano il reindirizzamento TDS.

Qualsiasi client che implementa TDS 7.4 deve supportare anche il reindirizzamento. Eccezioni toothis includono JDBC 4.0 non è supportato completamente le funzionalità di reindirizzamento di hello e Tedious per Node.JS in cui non è stato implementato il reindirizzamento.

Per "I client legacy", vale a dire che supporta TDS versione 7.3 e hello seguito - nome FQDN del server nella stringa di connessione hello deve essere modificati:

FQDN server originale nella stringa di connessione hello: <*nome server*>. database.windows.net

FQDN server modificato nella stringa di connessione hello: <*nome server*> database. **protezione**. windows.net

Un elenco parziale di "client di livello inferiore" include:

* .NET 4.0 e versioni precedenti,
* ODBC 10.0 e versioni precedenti.
* JDBC (mentre JDBC supporta TDS 7.4, hello funzionalità di reindirizzamento TDS non è completamente supportata)
* Tedious (per Node.JS)

**Nota:** hello sopra Modifica nome FDQN di server può essere utile anche per applicare un criterio di controllo a livello di Server SQL senza la necessità di una configurazione passaggio in ogni database (attenuazione temporaneo).     

