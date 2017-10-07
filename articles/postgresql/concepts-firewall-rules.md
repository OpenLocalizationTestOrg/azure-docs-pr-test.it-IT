---
title: Regole firewall per Database di Azure per il server PostgreSQL | Microsoft Docs
description: Descrive le regole firewall per il Database di Azure per il server PostgreSQL.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 1d46a4434c483c3612a9a7b4cdef718d6dc3e765
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-server-firewall-rules"></a>Regole firewall per Database di Azure per PostgreSQL
I firewall impediscono tutti i server di database di access tooyour finché non si specifica quali computer dispongono di autorizzazioni. firewall Hello concede server toohello accesso in base a hello provenienti dall'indirizzo IP di ogni richiesta.
tooconfigure il firewall, creare regole del firewall che specificano intervalli di indirizzi IP accettabili. È possibile creare regole del firewall a livello di server hello.

**Regole del firewall:** queste regole abilitare tooaccess client l'intero Database di Azure per PostgreSQL Server, vale a dire tutti i database all'interno di hello hello stesso server logico. Regole del firewall a livello di server possono essere configurate usando hello portale di Azure o i comandi CLI di Azure. le regole firewall di livello server toocreate, è necessario essere proprietario della sottoscrizione hello o un collaboratore alla sottoscrizione.

## <a name="firewall-overview"></a>Panoramica del firewall
Per impostazione predefinita, tutti i database access tooyour Database di Azure per server PostgreSQL è bloccato dal firewall hello. toobegin utilizzando il server da un altro computer, è necessario toospecify uno o più a livello di server firewall regole tooenable accesso tooyour server. Utilizzare toospecify di regole firewall hello quale indirizzo IP compreso tra tooallow Internet hello. Accesso toohello sito Web del portale Azure stesso non è interessata da regole del firewall hello.
Hello di tentativi di connessione da Internet e Azure deve superare il firewall hello prima di poter raggiungere il PostgreSQL Database, come illustrato nel seguente diagramma hello:

![Flusso di esempio del funzionamento di firewall hello](media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-hello-internet"></a>Connessione da Internet hello
Le regole del firewall a livello di server applicano tooall database hello Azure Database per server PostgreSQL. Se l'indirizzo IP hello della richiesta di hello è in uno degli intervalli di hello specificati nelle regole del firewall a livello di server hello, connessione hello viene concessa.
Se l'indirizzo IP hello della richiesta di hello non è presente all'interno di intervalli hello specificata in una delle hello a livello di database o delle regole del firewall a livello di server, hello richiesta di connessione ha esito negativo.
Ad esempio, se l'applicazione si connette con il driver JDBC per PostgreSQL, è possibile riscontrare questo errore durante il tentativo di tooconnect quando hello firewall blocchi la connessione hello.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: nessuna voce pg\_hba.conf per l'host "123.45.67.890", utente "adminuser", database "postgresql", SSL

## <a name="programmatically-managing-firewall-rules"></a>Gestione di regole del firewall a livello di programmazione
Inoltre toohello portale di Azure, firewall, le regole possono essere gestiti a livello di programmazione utilizzando CLI di Azure.
Vedere anche [Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md) (Creare e gestire regole firewall per il Database di Azure per PostgreSQL tramite l'interfaccia della riga di comando di Azure)

## <a name="troubleshooting-hello-database-firewall"></a>Risoluzione dei problemi di firewall del database hello
Considerare i seguenti punti di accesso toohello Database di Microsoft Azure per il servizio PostgreSQL Server non comportarsi come previsto hello:

* **Elenco Consenti toohello le modifiche non sono state applicate ancora:** potrebbero essere presenti in quanto un ritardo di cinque minuti per la modifica toohello Database di Azure per effetto di tootake configurazione firewall PostgreSQL Server.

* **account di accesso Hello non è autorizzato o è stata utilizzata una password errata:** se un account di accesso non dispone di autorizzazioni sul Database Azure hello per PostgreSQL server o hello password utilizzata non è corretta, hello toohello connessione Database di Azure per server PostgreSQL è negato. Creazione di un'impostazione del firewall fornisce solo i client con un'opportunità tooattempt connessione server tooyour; ogni client dovrà fornire le credenziali di sicurezza necessarie hello.

Ad esempio, un client di JDBC hello il seguente errore ammesso.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: autenticazione della password non riuscita per l'utente "yourusername"

* **Indirizzo IP dinamico:** se si dispone di una connessione Internet con impostazione di indirizzi IP dinamici e si verificano problemi di comunicazione attraverso il firewall hello, è possibile provare una delle seguenti soluzioni hello:

* Richiedere il Provider di servizi Internet (ISP) per l'intervallo di indirizzi IP hello assegnato tooyour i computer client che hello di accesso ai Database di Azure per PostgreSQL Server e quindi aggiungere l'intervallo di indirizzi IP hello come una regola del firewall.

* Ottenere indirizzi IP statici per i computer client e quindi aggiungere gli indirizzi IP hello come regole del firewall.

## <a name="next-steps"></a>Passaggi successivi
Per informazioni sulla creazione di regole del firewall a livello di server e di database, vedere:
* [Creare e gestire i Database di Azure per le regole firewall PostgreSQL utilizzando hello portale di Azure](howto-manage-firewall-using-portal.md)
* [Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md) (Creare e gestire regole firewall del Database di Azure per PostgreSQL tramite l'interfaccia della riga di comando di Azure)