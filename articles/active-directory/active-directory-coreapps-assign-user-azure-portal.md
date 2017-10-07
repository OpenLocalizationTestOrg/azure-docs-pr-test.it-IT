---
title: un'app aziendale tooan utente o gruppo in Azure Active Directory aaaAssign | Documenti Microsoft
description: Come tooselect un tooassign app enterprise un utente o gruppo tooit in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a>Assegnare un'applicazione aziendale tooan utente o gruppo in Azure Active Directory
È facile tooassign un utente o un gruppo tooyour enterprise in Azure Active Directory (Azure AD). È necessario hello delle autorizzazioni appropriate toomanage hello enterprise app, che è necessario essere amministratore globale per la directory di hello.

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a>Come assegnare utente accesso tooan enterprise app?
1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.
2. Selezionare **più servizi**, immettere Azure Active Directory nella casella di testo hello e quindi selezionare **invio**.
3. In hello **Azure Active Directory - *nomedirectory***  blade (vale a dire hello Azure AD pannello per directory hello gestiti), selezionare **applicazioni aziendali**.

    ![Apertura di app aziendali](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. In hello **applicazioni aziendali** pannello seleziona **tutte le applicazioni**. Verrà visualizzato un elenco di App hello che è possibile gestire.
5. In hello **applicazioni aziendali - tutte le applicazioni** pannello, selezionare un'app.
6. In hello ***appname*** blade (vale a dire hello pannello con il nome di hello di hello app selezionata nel titolo hello), selezionare **utenti e gruppi**.

    ![Selezione di hello tutti i comandi di applicazioni](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. In hello ***appname*** **-assegnazione al gruppo & utente** blade, seleziona hello **Aggiungi** comando.
8. In hello **Aggiungi** pannello seleziona **utenti e gruppi**.

    ![Assegnare un'app toohello utente o gruppo](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. In hello **utenti e gruppi** pannello, selezionare uno o più utenti o gruppi da hello elenco e quindi selezionare hello **selezionare** pulsante nella parte inferiore di hello del pannello hello.
10. In hello **Aggiungi** pannello seleziona **ruolo**. Quindi, nella hello **selezionare il ruolo** blade, selezionare un toohello tooapply ruolo selezionato di utenti o gruppi e quindi selezionare hello **OK** pulsante nella parte inferiore di hello del pannello hello.
11. In hello **Aggiungi** blade, seleziona hello **assegnare** pulsante nella parte inferiore di hello del pannello hello. Hello assegnato agli utenti o gruppi disporranno delle autorizzazioni di hello definite dal hello ruolo selezionato per questa applicazione enterprise.

## <a name="next-steps"></a>Passaggi successivi
* [Visualizzare tutti i gruppi personali](active-directory-groups-view-azure-portal.md)
* [Rimuovere l'assegnazione di un utente o un gruppo da un'app aziendale](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Disabilitare l'accesso degli utenti per un'app aziendale](active-directory-coreapps-disable-app-azure-portal.md)
* [Modificare il nome di hello o logo di un'applicazione aziendale](active-directory-coreapps-change-app-logo-user-azure-portal.md)
