---
title: aaaAuthentication tooAzure SQL Data Warehouse | Documenti Microsoft
description: Azure Active Directory (AAD) e SQL Server authentication tooAzure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a>TooAzure l'autenticazione SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Proteggere un database in SQL Data Warehouse](sql-data-warehouse-overview-manage-security.md)
> * [Autenticazione](sql-data-warehouse-authentication.md)
> * [Introduzione a Transparent Data Encryption (TDE) di SQL Data Warehouse](sql-data-warehouse-encryption-tde.md)
> * [Introduzione a Transparent Data Encryption (TDE)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

tooconnect tooSQL Data Warehouse, è necessario passare le credenziali di sicurezza per l'autenticazione. Al momento di stabilire una connessione, alcune impostazioni di connessione sono configurate come parte della creazione della sessione di query.  

Per ulteriori informazioni sulla sicurezza e come data warehouse di tooenable connessioni tooyour, vedere [proteggere un database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].

## <a name="sql-authentication"></a>Autenticazione in SQL
tooconnect tooSQL Data Warehouse, è necessario fornire hello le seguenti informazioni:

* Nome del server completo
* Specificare l'autenticazione di SQL
* Nome utente
* Password
* Database predefinito (facoltativo)

Per impostazione predefinita, la connessione si connette toohello *master* database e non il database utente. tooconnect tooyour i database utente, è possibile scegliere toodo una delle seguenti operazioni:

* Specificare il database predefinito hello durante la registrazione del server con Esplora oggetti di SQL Server in SSDT, SQL Server Management Studio, o nella stringa di connessione dell'applicazione hello. Ad esempio, includere il parametro InitialCatalog hello per una connessione ODBC.
* Evidenziare i database utente hello prima di creare una sessione in SSDT.

> [!NOTE]
> istruzione Transact-SQL Hello **utilizzare MyDatabase;** non è supportata per la modifica hello database per una connessione. Per informazioni di connessione tooSQL Data Warehouse con SSDT, vedere l'articolo toohello [Query con Visual Studio] [ Query with Visual Studio] articolo.
> 
> 

## <a name="azure-active-directory-aad-authentication"></a>Autenticazione di Azure Active Directory (AAD)
[Azure Active Directory] [ What is Azure Active Directory] l'autenticazione è un meccanismo di connessione tooMicrosoft Azure SQL Data Warehouse usando le identità in Azure Active Directory (Azure AD). Con l'autenticazione di Azure Active Directory, è possibile gestire centralmente le identità hello di utenti del database e altri servizi Microsoft in un'unica posizione centrale. Gestione degli ID centrale fornisce un'unica posizione toomanage agli utenti di SQL Data Warehouse e semplifica la gestione delle autorizzazioni. 

### <a name="benefits"></a>Vantaggi
I vantaggi di Azure Active Directory includono i seguenti:

* Fornisce l'autenticazione Server tooSQL alternativo.
* Consente di arrestare la proliferazione di hello delle identità tra server di database.
* Consente la rotazione delle password in un'unica posizione.
* Consente di gestire le autorizzazioni del database tramite gruppi (AAD) esterni.
* Consente di eliminare l'archiviazione delle password abilitando l'autenticazione integrata di Windows e altre forme di autenticazione supportate da Azure Active Directory.
* Usa contenuti identità tooauthenticate utenti di database a livello di database hello.
* Supporta l'autenticazione basata su token per applicazioni che si connettono tooSQL Data Warehouse.
* Supporta la Multi-Factor Authentication tramite l'autenticazione universale di Active Directory per SQL Server Management Studio. Per una descrizione di Multi-Factor Authentication, vedere [Il supporto SSMS per l'MFA di Azure Active Directory con database SQL e SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).

> [!NOTE]
> Azure Active Directory è ancora relativamente nuovo e presenta alcune limitazioni. tooensure che Azure Active Directory è una scelta ottimale per l'ambiente, vedere [funzionalità Azure AD e limitazioni][Azure AD features and limitations], in particolare hello considerazioni aggiuntive.
> 
> 

### <a name="configuration-steps"></a>Procedura di configurazione
Seguire questi passaggi tooconfigure Azure Active Directory authentication.

1. Creare e popolare un'istanza di Azure Active Directory
2. Facoltativo: Associare o modificare hello active directory a cui è attualmente associato alla sottoscrizione di Azure
3. Creare un amministratore di Azure Active Directory per Azure SQL Data Warehouse.
4. Configurare i computer client
5. Creare utenti del database indipendente in tooAzure del database eseguito il mapping delle identità di Active Directory
6. La connessione di data warehouse di tooyour usando le identità di Azure AD

Gli utenti di Azure Active Directory non sono attualmente visualizzati in Esplora oggetti di SSDT. In alternativa, consente di visualizzare gli utenti di hello [Sys. database_principals](https://msdn.microsoft.com/library/ms187328.aspx).

### <a name="find-hello-details"></a>Trovare i dettagli di hello
* Hello passaggi tooconfigure usare Azure Active Directory l'autenticazione e sono quasi identici per Database SQL di Azure e Azure SQL Data Warehouse. Seguire passaggi nell'argomento hello dettagliati di hello [tooSQL connessione Database o Data Warehouse da usando Azure Active Directory l'autenticazione di SQL](../sql-database/sql-database-aad-authentication.md).
* Creare ruoli personalizzati del database e aggiungere utenti toohello ruoli. Concedere quindi autorizzazioni granulari toohello ruoli. Per altre informazioni, vedere [Introduzione alle autorizzazioni del motore di database](https://msdn.microsoft.com/library/mt667986.aspx).

## <a name="next-steps"></a>Passaggi successivi
toostart l'esecuzione di query del data warehouse con Visual Studio e altre applicazioni, vedere [Query con Visual Studio][Query with Visual Studio].

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
