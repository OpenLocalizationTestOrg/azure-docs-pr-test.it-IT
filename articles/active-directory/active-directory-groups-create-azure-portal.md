---
title: un gruppo di utenti in Azure Active Directory aaaCreate | Documenti Microsoft
description: Come toocreate un gruppo in Azure Active Directory e aggiungere membri toohello gruppo
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a>Creare un gruppo e aggiungere membri in Azure Active Directory
> [!div class="op_single_selector"]
> * [Portale di Azure](active-directory-groups-create-azure-portal.md)
> * [Portale di Azure classico](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Questo articolo viene illustrato come toocreate e popolare un nuovo gruppo in Azure Active Directory. Utilizzare un'attività di gestione gruppo tooperform, ad esempio l'assegnazione di licenze o autorizzazioni tooa numero di utenti o dispositivi in una sola volta.

## <a name="how-do-i-create-a-group"></a>Come si crea un gruppo?
1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.
2. Selezionare **più servizi**, immettere **utenti e gruppi** nella casella di testo hello e quindi selezionare **invio**.

   ![Apertura di Gestione utenti](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. In hello **utenti e gruppi** pannello seleziona **tutti i gruppi di**.

   ![Pannello gruppi hello di apertura](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. In hello **utenti e gruppi - tutti i gruppi di** blade, seleziona hello **Aggiungi** comando.

   ![Comando Aggiungi hello](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. In hello **gruppo** pannello, aggiungere un nome e una descrizione per il gruppo di hello.
6. tooselect tooadd toohello gruppo membri, seleziona **assegnato** in hello **tipo di appartenenza** e quindi selezionare **membri**. Per ulteriori informazioni su come toomanage hello appartenenza di un gruppo in modo dinamico, vedere [utilizzando attributi toocreate regole per l'appartenenza al gruppo avanzate](active-directory-groups-dynamic-membership-azure-portal.md).

   ![Selezione di membri tooadd](./media/active-directory-groups-create-azure-portal/select-members.png)
7. In hello **membri** pannello, selezionare uno o più utenti o dispositivi gruppo toohello tooadd e seleziona hello **selezionare** pulsante nella parte inferiore di hello di hello pannello tooadd li toohello gruppo. Hello **utente** filtri casella hello in base alla corrispondenza parte dell'utente tooany voce di un nome utente o un dispositivo di visualizzazione. I caratteri jolly non sono consentiti nella casella.
8. Al termine dell'aggiunta di membri toohello gruppo, selezionare **crea** su hello **gruppo** blade.    

   ![Creare una conferma del gruppo](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a>Passaggi successivi
Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.

* [Vedere i gruppi esistenti](active-directory-groups-view-azure-portal.md)
* [Gestire le impostazioni di un gruppo](active-directory-groups-settings-azure-portal.md)
* [Gestire i membri di un gruppo](active-directory-groups-members-azure-portal.md)
* [Gestire le appartenenze di un gruppo](active-directory-groups-membership-azure-portal.md)
* [Gestire le regole dinamiche per gli utenti in un gruppo](active-directory-groups-dynamic-membership-azure-portal.md)
