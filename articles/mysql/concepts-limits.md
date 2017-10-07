---
title: nel Database di Azure per MySQL aaaLimitations | Documenti Microsoft
description: Descrive i limiti dell'anteprima del Database di Azure per MySQL.
services: mysql
author: jasonh
ms.author: kamathsun
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 9c877c592bf640f62182d8761c9c51363882d706
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-mysql-preview"></a>Limiti del Database di Azure per MySQL (anteprima)
Hello Azure Database per il servizio MySQL è in anteprima pubblica. Hello nelle sezioni seguenti vengono descritti la capacità e i limiti funzionali nel servizio di database hello.

## <a name="service-tier-maximums"></a>Valori massimi del livello di servizio
Il Database di Azure per MySQL dispone di più livelli di servizio tra cui è possibile scegliere durante la creazione di un server. Per altre informazioni vedere [Opzioni e prestazioni disponibili in ogni livello di servizio](concepts-service-tiers.md).  

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
> ERROR 1040 (08004): Too many connections (ERRORE 1040 (08004): numero eccessivo di connessioni)

## <a name="preview-functional-limitations"></a>Limiti funzionali dell'anteprima:
### <a name="scale-operations"></a>Operazioni di scalabilità:
1.  La scalabilità dinamica dei server tra i livelli di servizio non è attualmente supportata, vale a dire il passaggio tra i livelli di servizio Base e Standard.
2.  L'aumento dinamico su richiesta dell'archiviazione sul server creato in precedenza non è attualmente supportato.
3.  La riduzione delle dimensioni di archiviazione del server non è supportato.

### <a name="server-version-upgrades"></a>Aggiornamenti della versione dei server:
- La migrazione automatica tra le versioni del motore del database principale non è attualmente supportata.

### <a name="subscription-management"></a>Gestione sottoscrizioni:
- Lo spostamento dinamico di server creati in precedenza tra le sottoscrizioni e il gruppo di risorse non è attualmente supportato.

### <a name="point-in-time-restore"></a>Ripristino temporizzato:
1.  Non è consentito il ripristino a livello di servizio toodifferent e/o dimensioni unità di calcolo e archiviazione.
2.  Il ripristino di un server eliminato non è supportato.

## <a name="next-steps"></a>Passaggi successivi:
[Opzioni disponibili in ogni livello di servizio](concepts-service-tiers.md)
[Versioni del Database MySQL supportate](concepts-supported-versions.md)
