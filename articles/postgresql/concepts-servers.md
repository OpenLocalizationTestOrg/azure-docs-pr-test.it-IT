---
title: concetti di aaaServer nel Database di Azure per PostgreSQL | Documenti Microsoft
description: Questo argomento fornisce considerazioni e linee guida per l'uso del database di Azure per server PostgreSQL.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 9cc7816992f2ddedd76fdf906075a723b97720a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-servers"></a>Database di Azure per server PostgreSQL
Questo argomento fornisce considerazioni e linee guida per l'uso del database di Azure per server PostgreSQL.

## <a name="what-is-an-azure-database-for-postgresql-server"></a>Che cos'è un database di Azure per il server PostgreSQL?
Un database di Azure per il server PostgreSQL funge da punto di gestione centrale per più database. È hello stesso costrutto server PostgreSQL che potrebbero avere familiarità con in HelloWorld locale. In particolare, hello PostgreSQL servizio gestito, garantisce prestazioni, espone funzionalità di accesso e a livello di server.

Un database di Azure per il server PostgreSQL:

- Viene creato all'interno di una sottoscrizione di Azure.
- È una risorsa padre hello per i database.
- Fornisce uno spazio dei nomi per i database.
- È un contenitore con la semantica di durata sicuro - eliminare un server ed elimina i database contenuto hello.
- Colloca risorse in un'area.
- Fornisce un endpoint di connessione per l'accesso a server e database (.postgresql.database.azure.com).
- Fornisce l'ambito di hello per i criteri di gestione che si applicano a database tooits: account di accesso, firewall, gli utenti, ruoli, le configurazioni e così via.
- È disponibile in più versioni. Per altre informazioni, vedere [Versioni supportate del database PostgreSQL](concepts-supported-versions.md).
- È estensibile dagli utenti. Per altre informazioni, vedere [Estensioni di PostgreSQL](concepts-extensions.md).

In un database di Azure per il server PostgreSQL è possibile creare uno o più database. È possibile rifiutare un singolo database per ogni server tooutilize toocreate tutte le risorse di hello o creare più database tooshare risorse hello. prezzi Hello è strutturato per ogni server, in base alla configurazione di hello del piano tariffario, unità, archiviazione (GB) di calcolo. Per altre informazioni, vedere i [piani tariffari](./concepts-service-tiers.md).

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-postgresql-server"></a>Come connettersi e autenticare tooan Database di Azure per server PostgreSQL?
Hello gli elementi seguenti consentono di assicurare database tooyour accesso sicuro.

|||
| :-- | :-- |
| **Autenticazione e autorizzazione** | Il database di Azure per il server PostgreSQL supporta l'autenticazione nativa a PostgreSQL. È possibile connettersi e autenticare tooserver con account di accesso amministratore del server hello. |
| **Protocollo** | servizio Hello supporta un protocollo di basata sul messaggio utilizzato dai PostgreSQL. |
| **TCP/IP** | protocollo Hello è supportato su TCP/IP e tramite socket dominio Unix. |
| **Firewall** | toohelp proteggere i dati, una regola del firewall impedisce a tutti i server di database di access tooyour o tooits database, finché non si specifica i computer che dispone dell'autorizzazione. Vedere [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md) (Database di Azure per le regole firewall del server PostgreSQL). |
|||

## <a name="how-do-i-manage-a-server"></a>Gestione di un server
È possibile gestire i Database di Azure per i server PostgreSQL utilizzando hello portale di Azure o hello [CLI di Azure](/cli/azure/postgres).

## <a name="next-steps"></a>Passaggi successivi
- Per una panoramica del servizio di hello, vedere [Database di Azure per PostgreSQL Panoramica](overview.md)
- Per informazioni sulle quote specifiche di risorse e sulle limitazioni in base al **livello di servizio**, vedere [Livelli di servizio](concepts-service-tiers.md)
- Per informazioni sul servizio toohello connessione, vedere [raccolte di connessioni per il Database di Azure per PostgreSQL](concepts-connection-libraries.md).
