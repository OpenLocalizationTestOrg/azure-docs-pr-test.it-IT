---
title: gruppi di hello aaaManage il gruppo appartiene tooin Azure Active Directory | Documenti Microsoft
description: I gruppi possono contenere altri gruppi in Azure Active Directory. Ecco come toomanage tali appartenenze.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0a0a1967084de0968e1e802559f9cdfd7ca6ae4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-toowhich-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a>Gestire i gruppi di toowhich che appartiene un gruppo nel tenant di Azure Active Directory
I gruppi possono contenere altri gruppi in Azure Active Directory. Ecco come toomanage tali appartenenze.

## <a name="how-do-i-find-hello-groups-my-group-is-a-member-of"></a>Ricerca di gruppi di hello di che al gruppo dell'utente è membro
1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.
2. Selezionare **più servizi**, immettere **utenti e gruppi** nella casella di testo hello e quindi selezionare **invio**.

   ![Apertura di Gestione utenti](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. In hello **utenti e gruppi** pannello seleziona **tutti i gruppi di**.

   ![Pannello gruppi hello di apertura](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. In hello **utenti e gruppi - tutti i gruppi** pannello, selezionare un gruppo.
5. In hello **gruppo - *groupname***  pannello seleziona **appartenenze**.

   ![Pannello di appartenenza al gruppo di apertura hello](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. tooadd il gruppo come membro del gruppo di un altro, in hello **gruppo - appartenenze** blade, seleziona hello **Aggiungi** comando.
7. Selezionare un gruppo hello **Seleziona gruppo** blade e quindi seleziona hello **selezionare** pulsante nella parte inferiore di hello del pannello hello. È possibile aggiungere il gruppo tooonly uno alla volta. Hello **utente** filtri casella hello in base alla corrispondenza parte dell'utente tooany voce di un nome utente o un dispositivo di visualizzazione. I caratteri jolly non sono consentiti nella casella.

   ![Aggiungere l'appartenenza a un gruppo](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. tooremove il gruppo come membro del gruppo di un altro, in hello **gruppo - appartenenze** pannello, selezionare un gruppo.
9. In hello ***groupname*** blade, seleziona hello **rimuovere** comandi e confermare la scelta al prompt dei comandi hello.

   ![Comando Rimuovi appartenenza](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. Al termine della modifica delle appartenenze dei gruppi per il proprio gruppo, selezionare **Salva**.

## <a name="additional-information"></a>Informazioni aggiuntive
Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.

* [Vedere i gruppi esistenti](active-directory-groups-view-azure-portal.md)
* [Creare un nuovo gruppo e aggiunta di membri](active-directory-groups-create-azure-portal.md)
* [Gestire le impostazioni di un gruppo](active-directory-groups-settings-azure-portal.md)
* [Gestire i membri di un gruppo](active-directory-groups-members-azure-portal.md)
* [Gestire le regole dinamiche per gli utenti in un gruppo](active-directory-groups-dynamic-membership-azure-portal.md)
