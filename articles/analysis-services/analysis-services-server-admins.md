---
title: amministratori di server aaaManage in Azure Analysis Services | Documenti Microsoft
description: Informazioni su come amministratori di server toomanage per un server Analysis Services in Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: e04387e48e9b9483c382ee5cc9fd65f8331fb2a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-server-administrators"></a>Gestire gli amministratori del server
Gli amministratori del server devono essere un utente valido o un gruppo in hello Azure Active Directory (Azure AD) per tenant hello in cui hello risiede server. È possibile utilizzare **gli amministratori di Analysis Services** nel Pannello di controllo hello per il server nel portale di Azure, o proprietà del Server negli amministratori del server di SQL Server Management Studio toomanage. 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a>amministratori del server tooadd tramite il portale di Azure
1. Nel Pannello di controllo hello del server, fare clic su **gli amministratori di Analysis Services**.
2. In hello  **\<nomeserver >-gli amministratori di Analysis Services** pannello, fare clic su **Aggiungi**.
3. In hello **aggiungere gli amministratori del Server** pannello selezionare gli account utente di Azure AD o invitare gli utenti esterni dall'indirizzo di posta elettronica.

    ![Amministratori del server nel portale di Azure](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a>amministratori del server tooadd utilizzando SQL Server Management Studio
1. Server hello rapida > **proprietà**.
2. In **Proprietà computer Analysis Server** fare clic su **Sicurezza**.
3. Fare clic su **Aggiungi**e quindi immettere l'indirizzo di posta elettronica hello per un utente o gruppo in Azure AD.
   
    ![Aggiungere gli amministratori del server in SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a>Passaggi successivi 
[Autenticazione e autorizzazioni utente](analysis-services-manage-users.md)  
[Gestire ruoli e utenti del database](analysis-services-database-users.md)  
[Controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-what-is.md)  

