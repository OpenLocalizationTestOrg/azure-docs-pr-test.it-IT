---
title: Azure Analysis Services aaaManage | Documenti Microsoft
description: Informazioni su come toomanage un Analysis Services server in Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a>Gestire Analysis Services
Dopo aver creato un server Analysis Services in Azure, vi possono essere alcune attività di gestione e amministrazione è necessario tooperform immediatamente o verso il basso un po' hello strada. Ad esempio, eseguire l'elaborazione dei dati di aggiornamento toohello, controllare chi può accedere ai modelli di hello del server o monitorare l'integrità del server. Alcune attività di gestione possono essere eseguite solo nel portale di Azure, altre in SQL Server Management Studio (SSMS) e altre ancora possono essere eseguite in entrambi gli ambienti.

## <a name="azure-portal"></a>Portale di Azure
[Portale di Azure](http://portal.azure.com/) è in cui è possibile creare ed eliminare i server, monitoraggio delle risorse di server, modificare dimensioni e gestire chi ha accesso tooyour server.  Se si verificano problemi, è inoltre possibile inviare una richiesta di supporto.

![Ottenere il nome del server in Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a>SQL Server Management Studio
Connessione server tooyour in Azure è simile a connessione tooa istanza del server dell'organizzazione. Da SQL Server Management Studio, è possibile eseguire molte delle hello stessa attività, ad esempio l'elaborazione dei dati o creare uno script di elaborazione, la gestione dei ruoli e utilizzare PowerShell.
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a>Scaricare e installare SSMS
tooget tutti hello funzionalità più recenti e più esperienza di hello quando ci si connette il server di Azure Analysis Services tooyour, assicurarsi che si utilizza una versione più recente di hello di SQL Server Management Studio. 

[Scaricare SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).


### <a name="tooconnect-with-ssms"></a>tooconnect con SQL Server Management Studio
 Quando si utilizza SQL Server Management Studio, prima della connessione messaggi hello del server tooyour prima volta, assicurarsi che il nome utente è incluso nel gruppo di amministratori di Analysis Services hello. vedere, più toolearn [gli amministratori del Server](#server-administrators) più avanti in questo articolo.

1. Prima di connettersi, è necessario il nome di server hello tooget. In **portale di Azure** > server > **Panoramica** > **nome Server**, nome del server hello copia.
   
    ![Ottenere il nome del server in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. In SSMS > **Esplora oggetti** fare clic su **Connetti** > **Analysis Services**.
3. In hello **connettersi tooServer** nella finestra di dialogo Incolla in nome server hello, quindi in **autenticazione**, scegliere uno dei seguenti tipi di autenticazione hello:
   
    **L'autenticazione di Windows** toouse le credenziali di dominio omeutente e la password di Windows.

    **L'autenticazione di Password di Active Directory** toouse un account aziendale. Ad esempio, per la connessione da un computer non incluso nel dominio.

    **Autenticazione universale di Active Directory** toouse [interattivo o multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md). 
   
    ![Connessione in SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a>Amministratori del server e utenti del database
In Azure Analysis Services ci sono due tipi di utenti, gli amministratori del server e gli utenti del database. Entrambi i tipi di utenti devono essere in Azure Active Directory ed essere specificati dal nome UPN o dall'indirizzo di posta elettronica dell'organizzazione. vedere, più toolearn [l'autenticazione e le autorizzazioni utente](analysis-services-manage-users.md).


## <a name="troubleshooting-connection-problems"></a>Risoluzione dei problemi di connessione
Quando ci si connette tramite SSMS, se si verificano problemi, potrebbe essere necessario cache di account di accesso tooclear hello. Non è toodisc memorizzati nella cache. cache hello tooclear, chiudere e riavviare hello connettere processo. 

## <a name="next-steps"></a>Passaggi successivi
Se è già stato ancora distribuito un nuovo server tooyour di modello tabulare, ora è il momento opportuno. vedere, più toolearn [distribuire tooAzure Analysis Services](analysis-services-deploy.md).

Se è già distribuito un server tooyour modello, si è pronti tooconnect tooit utilizzando un client o browser. vedere, più toolearn [ottenere dati dal server Azure Analysis Services](analysis-services-connect.md).

