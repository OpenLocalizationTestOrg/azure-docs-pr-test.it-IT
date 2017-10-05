---
title: Concetti relativi ai server nel database di Azure per PostgreSQL | Microsoft Docs
description: Questo argomento fornisce considerazioni e linee guida per l'uso del database di Azure per server PostgreSQL.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: c79603a11fa23ad775783157675c07ab67102057
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-servers"></a>Database di Azure per server PostgreSQL
Questo argomento fornisce considerazioni e linee guida per l'uso del database di Azure per server PostgreSQL.

## <a name="what-is-an-azure-database-for-postgresql-server"></a>Che cos'è un database di Azure per il server PostgreSQL?
Un database di Azure per il server PostgreSQL funge da punto di gestione centrale per più database. È lo stesso costrutto di server PostgreSQL con cui probabilmente si ha familiarità nell'ambiente locale. In particolare, il servizio PostgreSQL è gestito, assicura le prestazioni garantite, espone accesso e funzionalità a livello di server.

Un database di Azure per il server PostgreSQL:

- Viene creato all'interno di una sottoscrizione di Azure.
- È la risorsa madre per i database.
- Fornisce uno spazio dei nomi per i database.
- È un contenitore con semantica di lunga durata: l'eliminazione di un server comporta l'eliminazione dei database in esso contenuti.
- Colloca risorse in un'area.
- Fornisce un endpoint di connessione per l'accesso a server e database (.postgresql.database.azure.com).
- Fornisce l'ambito per i criteri di gestione applicati ai database: account di accesso, firewall, utenti, ruoli, configurazioni e così via.
- È disponibile in più versioni. Per altre informazioni, vedere [Versioni supportate del database PostgreSQL](concepts-supported-versions.md).
- È estensibile dagli utenti. Per altre informazioni, vedere [Estensioni di PostgreSQL](concepts-extensions.md).

In un database di Azure per il server PostgreSQL è possibile creare uno o più database. È possibile scegliere di creare un singolo database per ogni server per usare tutte le risorse o creare più database per condividere le risorse. I prezzi sono strutturati per server, in base alla configurazione del piano tariffario, delle unità di calcolo e dell'archiviazione (GB). Per altre informazioni, vedere i [piani tariffari](./concepts-service-tiers.md).

## <a name="how-do-i-connect-and-authenticate-to-an-azure-database-for-postgresql-server"></a>Come connettersi ed eseguire l'autenticazione a un database di Azure per il server PostgreSQL?
I seguenti elementi contribuiscono a garantire un accesso sicuro al database.

|||
| :-- | :-- |
| **Autenticazione e autorizzazione** | Il database di Azure per il server PostgreSQL supporta l'autenticazione nativa a PostgreSQL. È possibile connettersi ed eseguire l'autenticazione al server tramite l'account amministratore del server. |
| **Protocollo** | Il servizio supporta un protocollo basato su messaggi usato da PostgreSQLL. |
| **TCP/IP** | Il protocollo è supportato su TCP/IP e sui socket di dominio Unix. |
| **Firewall** | Per proteggere i dati, le regole del firewall impediscono qualsiasi accesso al server del database o ai database finché non si specificano i computer autorizzati. Vedere [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md) (Database di Azure per le regole firewall del server PostgreSQL). |
|||

## <a name="how-do-i-manage-a-server"></a>Gestione di un server
È possibile gestire il database di Azure per i server PostgreSQL mediante il portale o l'[interfaccia della riga di comando di Azure](/cli/azure/postgres).

## <a name="next-steps"></a>Passaggi successivi
- Per una panoramica del servizio, vedere [Azure Database for PostgreSQL Overview](overview.md) (Database di Azure per una panoramica di PostgreSQL)
- Per informazioni sulle quote specifiche di risorse e sulle limitazioni in base al **livello di servizio**, vedere [Livelli di servizio](concepts-service-tiers.md)
- Per informazioni sulla connessione al servizio, vedere [Raccolte connessioni per il database di Azure per PostgreSQL](concepts-connection-libraries.md).
