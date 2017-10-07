---
title: Cenni preliminari sullo sviluppo di applicazioni di Database aaaSQL | Documenti Microsoft
description: "Informazioni sulle librerie di connettività disponibili e procedure consigliate per applicazioni che si connettono tooSQL Database."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: genemi
ms.assetid: 67c02204-d1bd-4622-acce-92115a7cde03
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: 17f04db600828f90c42c750c9abdb92cfa4ca817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-application-development-overview"></a>Panoramica dello sviluppo di applicazioni del database SQL
Questo articolo descrive considerazioni di base hello che uno sviluppatore da tenere in considerazione durante la scrittura di codice tooconnect tooAzure Database SQL.

> [!TIP]
> Per visualizzare un'esercitazione come toocreate un server, creare un firewall basato su server, è possibile visualizzare le proprietà di server di connettersi tramite SQL Server Management Studio, Esegui query sul database master hello, creare un database di esempio e un database vuoto, eseguire query su proprietà di database, la connessione uso di SQL Server Management Studio e database di esempio hello query, vedere [ottenere esercitazione introduttiva](sql-database-get-started-portal.md).
>

## <a name="language-and-platform"></a>Linguaggio e piattaforma
Sono disponibili esempi di codice per svariati linguaggi di programmazione e piattaforme. È possibile trovare esempi di codice toohello collegamenti in: 

* Altre informazioni: [Librerie di connessioni per database SQL e SQL Server](sql-database-libraries.md)

## <a name="tools"></a>Strumenti 
È possibile sfruttare strumenti open source come [cheetah](https://github.com/wunderlist/cheetah), [sql-cli](https://www.npmjs.com/package/sql-cli) e [Visual Studio Code](https://code.visualstudio.com/). Inoltre, il database SQL di Azure interagisce con gli strumenti Microsoft come [Visual Studio](https://www.visualstudio.com/downloads/) e [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).  È inoltre possibile utilizzare hello portale di gestione di Azure, PowerShell e API REST consentono di aumentare la produttività aggiuntiva.

## <a name="resource-limitations"></a>Limiti delle risorse
Database SQL di Azure gestisce i database delle risorse hello tooa disponibili tramite due meccanismi diversi: la governance delle risorse e imposizione dei limiti.

* Altre informazioni: [Limiti delle risorse del database SQL di Azure](sql-database-resource-limits.md)

## <a name="security"></a>Sicurezza
Il database SQL di Azure fornisce risorse per limitare l'accesso, proteggere i dati e monitorare le attività in un database SQL.

* Altre informazioni: [Protezione del database SQL](sql-database-security-overview.md)

## <a name="authentication"></a>Autenticazione
* Il database SQL di Azure supporta utenti e account di accesso per l'autenticazione di SQL Server e utenti e account di accesso per l' [autenticazione di Azure Active Directory](sql-database-aad-authentication.md) .
* È necessario un determinato database, anziché l'impostazione toohello toospecify *master* database.
* Non è possibile usare Transact-SQL hello **utilizzare NomeDatabase;** istruzione sul Database SQL tooswitch tooanother database.
* Altre informazioni: [Protezione del database SQL: gestire l'accesso al database e la sicurezza degli account di accesso](sql-database-manage-logins.md)

## <a name="resiliency"></a>Resilienza
Quando un errore temporaneo si verifica durante la connessione tooSQL Database, il codice deve ripetere chiamata hello.  È consigliabile utilizzare la logica di backoff logica di tentativi, in modo che non sovraccarica hello Database SQL con più client contemporaneamente con nuovo tentativo in corso.

* Esempi di codice: per gli esempi di codice che illustrano la logica di riesecuzione, vedere gli esempi per la lingua di hello di propria scelta nel: [raccolte di connessioni per il Database SQL e SQL Server](sql-database-libraries.md)
* Altre informazioni: [Messaggi di errore per programmi client di Database SQL](sql-database-develop-error-messages.md)

## <a name="managing-connections"></a>Gestione delle connessioni
* Logica di connessione del client, eseguire l'override toobe di timeout predefinito di hello 30 secondi.  valore predefinito di Hello di 15 secondi è troppo breve per le connessioni che dipendono da hello internet.
* Se si utilizza un [pool di connessioni](http://msdn.microsoft.com/library/8xx3tyca.aspx), che tooclose prova connessione prova immediata del programma non utilizza attivamente e non si sta preparando tooreuse è.

## <a name="network-considerations"></a>Considerazioni sulla rete
* Nel computer di hello che ospita il programma client, verificare hello firewall consenta la comunicazione TCP in uscita sulla porta 1433.  Altre informazioni: [Configurazione del firewall di un database SQL di Azure](sql-database-configure-firewall-settings.md)
* Se il programma client si connette tooSQL Database mentre è in esecuzione il client in una macchina virtuale di Azure (VM), è necessario aprire determinati intervalli di porta nella macchina virtuale hello. Altre informazioni: [Porte superiori a 1433 per ADO.NET 4.5 e database SQL](sql-database-develop-direct-route-ports-adonet-v12.md)
* A volte, tooAzure le connessioni client SQL Database Ignora proxy hello e interagire direttamente con il database di hello. Le porte diverse da 1433 diventano importanti. Per altre informazioni, vedere [Architettura della connettività del database SQL di Azure](sql-database-connectivity-architecture.md) e [Porte successive alla 1433 per ADO.NET 4.5 e database SQL](sql-database-develop-direct-route-ports-adonet-v12.md).

## <a name="data-sharding-with-elastic-scale"></a>Partizionamento orizzontale dei dati con la scalabilità elastica
Scalabilità elastica semplifica il processo di hello di scalabilità orizzontale (). 

* [Schemi progettuali per applicazioni SaaS multi-tenant con il database SQL di Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [Routing dipendente dei dati](sql-database-elastic-scale-data-dependent-routing.md)
* [Introduzione alla funzionalità di scalabilità elastica del database SQL di Azure (anteprima)](sql-database-elastic-scale-get-started.md)

## <a name="next-steps"></a>Passaggi successivi
Esplorare tutti hello [funzionalità del Database SQL](sql-database-technical-overview.md)
