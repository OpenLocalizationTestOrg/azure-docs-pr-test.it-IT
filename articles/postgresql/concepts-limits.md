---
title: nel Database di Azure per PostgreSQL aaaLimitations | Documenti Microsoft
description: Descrive i limiti del Database di Azure per PostgreSQL.
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.topic: article
ms.date: 06/01/2017
ms.openlocfilehash: f53dd240e55e0633bc1dfb8ad25e1818fa8ae18c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-postgresql"></a>Limiti del Database di Azure per PostgreSQL
Hello Azure Database PostgreSQL servizio è in anteprima pubblica. Hello nelle sezioni seguenti vengono descritti la capacità e i limiti funzionali nel servizio di database hello.

## <a name="service-tier-maximums"></a>Valori massimi del livello di servizio
Il Database di Azure per PostgreSQL dispone di più livelli di servizio tra cui è possibile scegliere durante la creazione di un server. Per altre informazioni vedere [Opzioni e prestazioni disponibili in ogni livello di servizio](concepts-service-tiers.md).  

È un numero massimo di connessioni, unità di calcolo e archiviazione in ogni livello di servizio durante l'anteprima del servizio hello, come indicato di seguito: 

|                            |                   |
| :------------------------- | :---------------- |
| **Numero massimo di connessioni**        |                   |
| Base con 50 unità di calcolo     | 50 connessioni    |
| Base con 100 unità di calcolo    | 100 connessioni   |
| Standard con 100 unità di calcolo | 200 connessioni   |
| Standard con 200 unità di calcolo | 300 connessioni   |
| Standard con 400 unità di calcolo | 400 connessioni   |
| Standard con 800 unità di calcolo | 500 connessioni   |
| **Unità di calcolo massime**      |                   |
| Livello di servizio Basic         | 100 unità di calcolo |
| Livello di servizio Standard      | 800 unità di calcolo |
| **Spazio di archiviazione massimo**            |                   |
| Livello di servizio Basic         | 1 TB              |
| Livello di servizio Standard      | 1 TB              |

Quando vengono raggiunte numero eccessivo di connessioni, potrebbe essere visualizzato il seguente errore hello:
> FATAL: sorry, too many clients already (ERRORE IRREVERSIBILE: ci sono già troppi client)

## <a name="preview-functional-limitations"></a>Limiti funzionali dell'anteprima
### <a name="scale-operations"></a>Operazioni di scalabilità
1.  La scalabilità dinamica dei server tra i livelli di servizio non è attualmente supportata, vale a dire il passaggio tra i livelli di servizio Base e Standard.
2.  L'aumento dinamico su richiesta dell'archiviazione sul server creato in precedenza non è attualmente supportato.
3.  La riduzione delle dimensioni di archiviazione del server non è supportato.

### <a name="server-version-upgrades"></a>Aggiornamenti della versione dei server
- La migrazione automatica tra le versioni del motore del database principale non è attualmente supportata.

### <a name="subscription-management"></a>Gestione sottoscrizioni
- Lo spostamento dinamico di server creati in precedenza tra le sottoscrizioni e il gruppo di risorse non è attualmente supportato.

### <a name="point-in-time-restore"></a>Ripristino temporizzato
1.  Non è consentito il ripristino a livello di servizio toodifferent e/o dimensioni unità di calcolo e archiviazione.
2.  Il ripristino di un server eliminato non è supportato.

## <a name="next-steps"></a>Passaggi successivi
- Informazioni sulle [opzioni e prestazioni disponibili in ogni piano tariffario](concepts-service-tiers.md)
- Informazione sulle [Supported PostgreSQL Database Versions](concepts-supported-versions.md) (Versioni supportate del Database PostgreSQL)
- Revisione [come tooBack backup e ripristino di un server di Database di Azure per l'utilizzo di PostgreSQL hello portale di Azure](howto-restore-server-portal.md)
