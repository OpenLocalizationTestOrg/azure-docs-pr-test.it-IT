---
title: concetti di aaaServer nel Database di Azure per MySQL | Documenti Microsoft
description: Questo argomento fornisce considerazioni e linee guida per l'uso del database di Azure per server MySQL.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 4d994cbdbde93ac5af3f4a2a7375b5851bebb1cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="server-concepts-in-azure-database-for-mysql"></a>Concetti relativi ai server nel database di Azure per MySQL
Questo argomento fornisce considerazioni e linee guida per l'uso del database di Azure per server MySQL.

## <a name="what-is-an-azure-database-for-mysql-server"></a>Che cos'è un database di Azure per il server MySQL?

Un database di Azure per il server MySQL funge da punto di gestione centrale per più database. È hello stesso costrutto di server MySQL che potrebbero avere familiarità con in HelloWorld locale. In particolare, hello Azure Database per il servizio MySQL è gestita, garantisce prestazioni, espone funzionalità di accesso e a livello di server.

Un database di Azure per il server MySQL:

- Viene creato all'interno di una sottoscrizione di Azure.
- È una risorsa padre hello per i database.
- Fornisce uno spazio dei nomi per i database.
- È un contenitore con la semantica di durata sicuro - eliminare un server ed elimina i database contenuto hello.
- Colloca risorse in un'area.
- Fornisce un endpoint di connessione per l'accesso a server e database.
- Fornisce l'ambito di hello per i criteri di gestione che si applicano a database tooits: account di accesso, firewall, gli utenti, ruoli, le configurazioni e così via.
- È disponibile in più versioni. Per altre informazioni, vedere [Supported Azure Database for MySQL database versions](./concepts-supported-versions.md) (Database di Azure supportato per le diverse versioni del database MySQL).

In un database di Azure per il server MySQL è possibile creare uno o più database. È possibile rifiutare un singolo database per ogni server tooutilize toocreate tutte le risorse di hello o creare più database tooshare risorse hello. prezzi Hello è strutturato per ogni server, in base alla configurazione di hello del piano tariffario, unità, archiviazione (GB) di calcolo. Per altre informazioni, vedere i [piani tariffari](./concepts-service-tiers.md).

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-mysql-server"></a>Come connettersi e autenticare tooan Database di Azure per il server MySQL

Hello gli elementi seguenti consentono di assicurare database tooyour accesso sicuro.

|||
| :-- | :-- |
| **Autenticazione e autorizzazione** | Il database di Azure per il server MySQL supporta l'autenticazione nativa a MySQL. È possibile connettersi e autenticare tooserver con account di accesso amministratore del server hello. |
| **Protocollo** | servizio Hello supporta un protocollo basato su messaggi utilizzato da MySQL. |
| **TCP/IP** | protocollo Hello è supportato su TCP/IP e tramite socket dominio Unix. |
| **Firewall** | toohelp proteggere i dati, una regola del firewall impedisce a tutti i server di database di access tooyour o tooits database, finché non si specifica i computer che dispone dell'autorizzazione. Vedere [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md) (Database di Azure per le regole firewall del server MySQL). |
| **SSL** | servizio Hello supporta l'applicazione connessioni SSL tra le applicazioni e il server di database.  Vedere [connettività configurare SSL in toosecurely l'applicazione connessione tooAzure Database MySQL](./howto-configure-ssl.md). |
|||

## <a name="how-do-i-manage-a-server"></a>Gestione di un server
È possibile gestire i Database di Azure per i server MySQL mediante hello portale di Azure o hello CLI di Azure.

## <a name="next-steps"></a>Passaggi successivi
- Per una panoramica del servizio di hello, vedere [Database di Azure per una panoramica di MySQL](./overview.md)
- Per informazioni sulle quote specifiche di risorse e sulle limitazioni in base al **livello di servizio**, vedere [Livelli di servizio](./concepts-service-tiers.md)
- Per informazioni sul servizio toohello connessione, vedere [raccolte di connessioni per il Database di Azure per MySQL](./concepts-connection-libraries.md).
