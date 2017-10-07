---
title: aaaConditional Access - Database SQL di Azure e Data Warehouse | Documento di Microsoft
description: Informazioni su come tooconfigure accesso condizionale per i Database di SQL Azure e Data Warehouse.
services: sql-database
author: BYHAM
manager: jhubbard
ms.custom: security
ms.service: sql-database
ms.topic: article
ms.date: 06/07/2017
ms.author: rickbyh
ms.openlocfilehash: f49f4708c0f1b3cad1539d630c2efd919f8ece68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-mfa-with-azure-sql-database-and-data-warehouse"></a>Accesso condizionale (MFA) con il database SQL di Azure e Azure SQL Data Warehouse  

Sia il database SQL che SQL Data Warehouse supportano l'accesso condizionale Microsoft. Hello seguente procedura mostra come Database SQL di tooconfigure tooenforce un criterio di accesso condizionale.  

## <a name="prerequisites"></a>Prerequisiti  
- È necessario configurare l'autenticazione di Azure Active Directory toosupport Database SQL o SQL Data Warehouse. Per informazioni sulla procedura specifica, vedere [Configurare e gestire l'autenticazione di Azure Active Directory con il database SQL oppure con SQL Data Warehouse](sql-database-aad-authentication-configure.md).  
- Quando è abilitata l'autenticazione a più fattori, è necessario connettersi con strumento supportato, ad esempio hello SSMS più recente. Per altre informazioni, vedere [Configurare Multi-Factor Authentication con database SQL di Azure per SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).  

## <a name="configure-ca-for-azure-sql-dbdw"></a>Configurare l'autorità di certificazione per il database SQL di Azure o Azure SQL Data Warehouse  
1.  Selezionare Accedi toohello portale **Azure Active Directory**, quindi selezionare **accesso condizionale**. Per altre informazioni, vedere [Documentazione tecnica sull'accesso condizionale di Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access-technical-reference).  
  ![pannello dell'accesso condizionale](./media/sql-database-conditional-access/conditional-access-blade.png) 
     
2.  In hello **criteri di accesso condizionale** pannello, fare clic su **nuovi criteri**, specificare un nome e quindi fare clic su **configurare le regole di**.  
3.  In **assegnazioni**selezionare **utenti e gruppi**, controllare **selezionare utenti e gruppi**e quindi selezionare utente hello o un gruppo per l'accesso condizionale. Fare clic su **selezionare**, quindi fare clic su **eseguita** tooaccept la selezione.  
  ![seleziona utenti e gruppi](./media/sql-database-conditional-access/select-users-and-groups.png)  

4.  Selezionare **App cloud** e fare clic su **Seleziona app**. Verranno visualizzate tutte le app disponibili per l'accesso condizionale. Selezionare **Database SQL di Azure**, nella parte inferiore di hello fare clic su **selezionare**, quindi fare clic su **eseguita**.  
  ![selezionare il database SQL](./media/sql-database-conditional-access/select-sql-database.png)  
  Se non si trova **Database SQL di Azure** elencati nella seguente cattura di schermata terzo hello, completare hello alla procedura seguente:   
  - Eseguire l'accesso nell'istanza SQL di Azure DB/DW tooyour utilizzando SQL Server Management Studio con un account amministratore AAD.  
  - Eseguire `CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`.  
  - Accedi tooAAD e verificare che il Database di SQL Azure e Data Warehouse sono elencati nelle applicazioni hello in AAD.  

5.  Selezionare **accedere ai controlli**selezionare **Grant**e quindi controllare i criteri di hello da tooapply. Per questo esempio, selezionare **Richiedi autenticazione a più fattori**.  
  ![selezionare l'opzione per concedere l'accesso](./media/sql-database-conditional-access/grant-access.png)  

## <a name="summary"></a>Riepilogo  
un'applicazione Hello selezionata (Database SQL di Azure) consentendo tooconnect tooAzure SQL DB/DW utilizzando Azure AD Premium, ora Applica criteri di accesso condizionale hello selezionato **necessaria autenticazione a più fattori.**  
Per domande sul database SQL di Azure o su Azure SQL Data Warehouse in relazione all'autenticazione a più fattori, contattare MFAforSQLDB@microsoft.com.  

## <a name="next-steps"></a>Passaggi successivi  

Per un'esercitazione, vedere [Proteggere il database SQL di Azure](sql-database-security-tutorial.md).
