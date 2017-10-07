---
title: aaaServer log nel Database di Azure per PostgreSQL | Documenti Microsoft
description: Genera registri errori e log di query nel database di Azure per PostgreSQL.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 22575f3882ce67fe640952f0a8dbfd8dcb4b16fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="server-logs-in-azure-database-for-postgresql"></a>Registri server nel database di Azure per PostgreSQL 
Il database di Azure per PostgreSQL genera log di query e registri errori. Tuttavia, i registri tootransaction di accesso non è supportata. Questi registri possono essere tooidentify utilizzato, risolvere i problemi e ripristinare gli errori di configurazione e delle prestazioni non ottimali. Per altre informazioni, vedere [Error Reporting and Logging](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html) (Segnalazione e registrazione degli errori).

## <a name="access-server-logs"></a>Accesso ai registri server
È possibile elencare e scaricare i log degli errori di server PostgreSQL Azure tramite il portale di Azure, hello [CLI di Azure](howto-configure-server-logs-using-cli.md) e API REST di Azure.

## <a name="log-retention"></a>Conservazione dei log
È possibile impostare il periodo di memorizzazione hello per i log di sistema usando il **log\_conservazione\_periodo** parametro associato al server. unità di Hello per questo parametro è giorni (necessario tooconfirm). valore predefinito di Hello è tre giorni. valore massimo Hello è 7 giorni. Si noti che il server deve disporre di file di log sufficiente spazio di archiviazione allocato toocontain hello mantenuto.
file di log Hello ruoterà ogni 1 ora o le dimensioni di 100MB, verifica per primo.

## <a name="configure-logging-for-azure-postgresql-server"></a>Configurare la registrazione per il server PostgreSQL di Azure
È possibile abilitare la registrazione delle query e degli errori per il server. I registri errori possono contenere informazioni su checkpoint, connessioni e vuoto automatico.

È possibile abilitare la registrazione delle query per l'istanza del database PostgreSQL impostando due parametri del server: log\_statement (istruzione log) e log\_min\_duration\_statement (istruzione durata registrazione min).

Hello **log\_istruzione** parametro consente di controllare quali istruzioni SQL vengono registrate. È consigliabile impostare questo parametro troppo***tutti*** toolog tutte le istruzioni; il valore predefinito di hello è none (necessario tooconfirm).

Hello **log\_min\_durata\_istruzione** parametro imposta il limite di hello in millisecondi, di un'istruzione di toobe registrati. Vengono registrate tutte le istruzioni SQL eseguite più di impostazione del parametro hello. Questo parametro è disabilitato e impostato toominus 1 (-1) per impostazione predefinita (necessario tooconfirm). L'attivazione di questo parametro può essere utile per rilevare query non ottimizzate nelle applicazioni.

Hello **log\_min\_messaggi** consente di determinare quali livelli di messaggio vengono scritti i log del server toohello toocontrol. valore predefinito di Hello è di avviso. (necessario tooconfirm)

Per altre informazioni su queste impostazioni, vedere la documentazione [Error Reporting and Logging](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html) (segnalazione e registrazione degli errori). Per una configurazione particolare del database di Azure per i parametri del server PostgreSQL, vedere [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md) (Registri server nel database di Azure per PostgreSQL).

## <a name="next-steps"></a>Passaggi successivi
- i log di tooaccess tramite l'interfaccia della riga di comando CLI di Azure, vedere [accesso e configurare i log di server tramite CLI di Azure](howto-configure-server-logs-using-cli.md)
- Per altre informazioni sui parametri del server, vedere [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md) (Personalizzare i parametri di configurazione del server tramite l'interfaccia della riga di comando di Azure).