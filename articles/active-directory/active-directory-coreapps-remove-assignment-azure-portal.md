---
title: assegnazione di un utente o gruppo da un'applicazione aziendale in Azure Active Directory aaaRemove | Documenti Microsoft
description: "Modalità hello tooremove assegnazione di un utente o gruppo di accesso da un'applicazione aziendale in Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: c067ecf59b4dedfe8f848357ca8bd545bdc610eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a>Rimuovere l'assegnazione di un utente o un gruppo da un'app aziendale in Azure Active Directory
È facile tooremove un utente o un gruppo viene assegnato l'accesso tooone delle applicazioni dell'organizzazione in Azure Active Directory (Azure AD). È necessario hello delle autorizzazioni appropriate toomanage hello enterprise app, che è necessario essere amministratore globale per la directory di hello.

## <a name="how-do-i-remove-a-user-or-group-assignment"></a>Come è possibile rimuovere l'assegnazione di un utente o un gruppo?
1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.
2. Selezionare **più servizi**, immettere **Azure Active Directory** nella casella di testo hello e quindi selezionare **invio**.
3. In hello **Azure Active Directory - *nomedirectory***  blade (vale a dire hello Azure AD pannello per directory hello gestiti), selezionare **applicazioni aziendali**.

    ![Apertura di app aziendali](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. In hello **applicazioni aziendali** pannello seleziona **tutte le applicazioni**. Verrà visualizzato un elenco di App hello che è possibile gestire.
5. In hello **applicazioni aziendali - tutte le applicazioni** pannello, selezionare un'app.
6. In hello ***appname*** blade (vale a dire hello pannello con il nome di hello di hello app selezionata nel titolo hello), selezionare **utenti e gruppi**.

    ![Selezione di utenti o gruppi](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. In hello ***appname*** **-assegnazione al gruppo & utente** pannello, selezionare uno degli altri utenti o gruppi e quindi selezionare hello **rimuovere** comando. Confermare la decisione al prompt dei comandi hello.

    ![Comando Remove hello](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a>Passaggi successivi
* [Visualizzare tutti i gruppi personali](active-directory-groups-view-azure-portal.md)
* [Assegnare un'applicazione aziendale tooan utente o gruppo](active-directory-coreapps-assign-user-azure-portal.md)
* [Disabilitare l'accesso degli utenti per un'app aziendale](active-directory-coreapps-disable-app-azure-portal.md)
* [Modificare il nome di hello o logo di un'applicazione aziendale](active-directory-coreapps-change-app-logo-user-azure-portal.md)
