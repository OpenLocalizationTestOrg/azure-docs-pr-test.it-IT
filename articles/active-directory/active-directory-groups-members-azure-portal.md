---
title: membri di hello aaaManage per un gruppo in Azure Active Directory | Documenti Microsoft
description: Come tooadd o rimuovere utenti e dispositivi da un gruppo in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4cb16ee63828003da251423a04736f7174dd4896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a>Gestire l'appartenenza al gruppo per gli utenti nel tenant di Azure Active Directory
Questo articolo spiega come toomanage hello membri per un gruppo in Azure Active Directory (Azure AD).

## <a name="how-do-i-find-hello-members-and-manage-them"></a>Come trovare i membri di hello e gestirli?
1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.
2. Selezionare **più servizi**, immettere **utenti e gruppi** nella casella di testo hello e quindi selezionare **invio**.

   ![Apertura di Gestione utenti](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. In hello **utenti e gruppi** pannello seleziona **tutti i gruppi di**.

   ![Pannello gruppi hello di apertura](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. In hello **utenti e gruppi - tutti i gruppi** pannello, selezionare un gruppo.
5. In hello **gruppo - *groupname***  pannello seleziona **membri**.

   ![Pannello membri hello di apertura](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. tooadd membri toohello gruppo hello **gruppo - membri** pannello seleziona **Aggiungi membri**.

   ![Comando Aggiungi membri](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. In hello **membri** pannello, selezionare uno o più utenti o dispositivi gruppo toohello tooadd e seleziona hello **selezionare** pulsante nella parte inferiore di hello di hello pannello tooadd li toohello gruppo. Hello **utente** filtri casella hello in base alla corrispondenza parte dell'utente tooany voce di un nome utente o un dispositivo di visualizzazione. I caratteri jolly non sono consentiti nella casella.
8. tooremove membri dal gruppo di hello, su hello **gruppo - membri** pannello, selezionare un membro.
9. In hello ***membername*** blade, seleziona hello **rimuovere** comandi e confermare la scelta al prompt dei comandi hello.

   ![Comando Rimuovi membri](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. Al termine della modifica dei membri per il gruppo di hello, selezionare **salvare**.

## <a name="additional-information"></a>Informazioni aggiuntive
Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.

* [Vedere i gruppi esistenti](active-directory-groups-view-azure-portal.md)
* [Creare un nuovo gruppo e aggiunta di membri](active-directory-groups-create-azure-portal.md)
* [Gestire le impostazioni di un gruppo](active-directory-groups-settings-azure-portal.md)
* [Gestire le appartenenze di un gruppo](active-directory-groups-membership-azure-portal.md)
* [Gestire le regole dinamiche per gli utenti in un gruppo](active-directory-groups-dynamic-membership-azure-portal.md)
